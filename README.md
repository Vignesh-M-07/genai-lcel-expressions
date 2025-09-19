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
# 1. Import required libraries
from langchain.prompts import ChatPromptTemplate
from langchain.chat_models import ChatOpenAI
from langchain.output_parsers import PydanticOutputParser
from pydantic import BaseModel, Field

# 2. Define output schema (Pydantic model)
class Explanation(BaseModel):
    summary: str = Field(description="Beginner-friendly explanation of the topic")
    length: str = Field(description="Length of explanation: short, medium, or long")

parser = PydanticOutputParser(pydantic_object=Explanation)

# 3. Define the prompt template with two parameters: topic, tone
prompt = ChatPromptTemplate.from_template(
    "Write a {tone} explanation about {topic} for a beginner audience. "
    "Respond in JSON with fields 'summary' and 'length'."
)

# 4. Choose the model
model = ChatOpenAI(model="gpt-3.5-turbo")

# 5. Build the chain with LLMChain (classic style)
from langchain.chains import LLMChain

chain = LLMChain(
    prompt=prompt,
    llm=model,
    output_parser=parser
)

# 6. Run the chain with different inputs
output1 = chain.run({"tone": "motivational", "topic": "blockchain"})
output2 = chain.run({"tone": "casual", "topic": "cloud computing"})
output3 = chain.run({"tone": "formal", "topic": "cybersecurity in healthcare"})

print("Motivational Blockchain:\n", output1, "\n")
print("Casual Cloud Computing:\n", output2, "\n")
print("Formal Cybersecurity:\n", output3)
```
### OUTPUT:

<img width="1382" height="356" alt="image" src="https://github.com/user-attachments/assets/7678bb37-b33e-4d1f-8cf4-27f92227a3a5" />


### RESULT:

The LCEL chain was successfully implemented and executed.
