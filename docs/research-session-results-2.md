### Best Practice Summary

*   **Define Structured Models with Nested Fields:** Use Pydantic's `BaseModel` to create a clear, hierarchical structure for your desired AI output. This makes the data predictable and easy to work with. For the study planner, this would involve a main `StudyPlan` model that contains a list of `Module` models, which in turn contain a list of `Lesson` models.

*   **Handle Retries and Validation Errors Gracefully:**
    *   **Retries:** Use `pydantic-ai`'s built-in retry mechanism (powered by `tenacity`) to handle transient network errors or temporary API issues. Configure it with a limited number of attempts and exponential backoff to avoid overwhelming the service.
    *   **Validation Errors:** When `pydantic-ai` fails to parse the LLM's response into your Pydantic model, it will raise a `ValidationError`. Catch this specific error in your FastAPI endpoint to prevent sending a malformed response to the user. Log the error for debugging and return a user-friendly error message.

*   **Avoid Blocking Async FastAPI Routes:**
    *   Always use `async def` for your FastAPI endpoints that perform I/O operations (like calling the Gemini API).
    *   Ensure that all libraries used within these async routes are also async-compatible. `pydantic-ai` is designed to work asynchronously.
    *   If you need to perform any CPU-bound work, use FastAPI's `run_in_threadpool` to avoid blocking the main event loop.

### Implementation Examples

Here are concrete examples to guide the implementation:

**1. Defining a Nested Pydantic Model for the Study Plan**

```python
from pydantic import BaseModel, Field
from typing import List

class Lesson(BaseModel):
    title: str = Field(..., description="The title of the lesson.")
    duration_minutes: int = Field(..., description="The estimated duration of the lesson in minutes.")
    description: str = Field(..., description="A brief description of the lesson.")

class Module(BaseModel):
    title: str = Field(..., description="The title of the module.")
    lessons: List[Lesson] = Field(..., description="A list of lessons in the module.")

class StudyPlan(BaseModel):
    student_name: str = Field(..., description="The name of the student.")
    topic: str = Field(..., description="The topic of the study plan.")
    modules: List[Module] = Field(..., description="A list of modules in the study plan.")
```

**2. FastAPI Endpoint with `pydantic-ai`, Gemini, Retries, and Error Handling**

```python
from fastapi import FastAPI, HTTPException
from pydantic import ValidationError
from pydantic_ai import pydantic_ai
from pydantic_ai.llms import Gemini
from tenacity import stop_after_attempt, wait_exponential
# from my_models import StudyPlan  # Import the models from the previous example

# It's recommended to load the API key from environment variables
import os
GEMINI_API_KEY = os.getenv("GEMINI_API_KEY")

# Configure the Gemini LLM
gemini_llm = Gemini(api_key=GEMINI_API_KEY)

@app.post("/generate_study_plan/", response_model=StudyPlan)
async def generate_study_plan(prompt: str):
    """
    Generates a study plan based on a user's prompt.
    This endpoint demonstrates schema validation, retries, and error handling.
    """
    try:
        study_plan = await pydantic_ai.async_run(
            llm=gemini_llm,
            prompt=prompt,
            output_model=StudyPlan,
            retry_config={
                "stop": stop_after_attempt(3),
                "wait": wait_exponential(multiplier=1, min=4, max=10),
            },
        )
        return study_plan
    except ValidationError as e:
        # Log the validation error for debugging
        print(f"Validation Error from LLM response: {e}")
        # Inform the user that the AI's response was not valid
        raise HTTPException(
            status_code=500,
            detail="The AI returned a response that could not be validated. Please try again."
        )
    except Exception as e:
        # Handle other potential errors (e.g., API connection errors)
        print(f"An unexpected error occurred: {e}")
        raise HTTPException(
            status_code=500,
            detail="An unexpected error occurred while generating the study plan."
        )
```

**3. Security Note for GDPR**

*   **Data Minimization:** When sending data to the Gemini API, only include the necessary information from the user's syllabus. Avoid sending any personally identifiable information (PII) that is not essential for generating the study plan.
*   **Pydantic for Input Validation:** Use Pydantic to validate and sanitize the incoming user syllabus data before it's even sent to the LLM. This can help prevent prompt injection attacks and ensure the data is in the expected format.
