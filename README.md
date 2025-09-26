## Design and Implementation of LangChain Expression Language (LCEL) Expressions

### AIM:
To design and implement a LangChain Expression Language (LCEL) expression that utilizes at least two prompt parameters and three key components (prompt, model, and output parser), and to evaluate its functionality by analyzing relevant examples of its application in real-world scenarios.

### PROBLEM STATEMENT:

Modern AI applications require structured, reusable, and parameterized pipelines to generate consistent outputs. LangChain Expression Language (LCEL) facilitates this by chaining together prompts, models, and parsers. This project focuses on designing a prompt that accepts two parameters (topic, tone), integrates a language model, and parses responses into a structured JSON format using Pydantic. The project demonstrates practical use cases in education, cloud computing, and healthcare.

### DESIGN STEPS:

STEP 1: Import required libraries from LangChain and Pydantic.

STEP 2: Define an output schema using PydanticOutputParser to ensure structured JSON responses.

STEP 3: Create a ChatPromptTemplate with two parameters: topic and tone.

STEP 4: Initialize the ChatOpenAI model (GPT-3.5-turbo).

STEP 5: Build the chain using LLMChain, connecting prompt → model → parser.

STEP 6: Run the chain with multiple input combinations and analyze structured outputs.

### PROGRAM:
```
from langchain.prompts import ChatPromptTemplate
from langchain.chat_models import ChatOpenAI
from langchain.output_parsers import PydanticOutputParser
from pydantic import BaseModel, Field

class Explanation(BaseModel):
    summary: str = Field(description="Beginner-friendly explanation of the topic")
    length: str = Field(description="Length of explanation: short, medium, or long")

parser = PydanticOutputParser(pydantic_object=Explanation)

prompt = ChatPromptTemplate.from_template(
    "Write a {tone} explanation about {topic} for a beginner audience. "
    "Respond in JSON with fields 'summary' and 'length'."
)

model = ChatOpenAI(model="gpt-3.5-turbo")

chain = prompt | model | parser

output1 = chain.invoke({"tone": "funny", "topic": "quantum computing"})
output2 = chain.invoke({"tone": "simple", "topic": "artificial intelligence"})
output3 = chain.invoke({"tone": "professional", "topic": "internet of things"})

print("Funny Quantum Computing:\n", output1, "\n")
print("Simple Artificial Intelligence:\n", output2, "\n")
print("Professional IoT:\n", output3)

```
### OUTPUT:

<img width="1330" height="445" alt="Screenshot 2025-09-26 082037" src="https://github.com/user-attachments/assets/e6ef2bae-b473-4806-8faf-57910f7ce13c" />


### RESULT:

The LCEL chain was successfully implemented and executed.
