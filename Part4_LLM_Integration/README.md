# Part 4 - LLM-Powered Feature: Model Prediction Explanation Pipeline
# Project Description
**Chosen Track: Track C - Model Prediction Explanation Pipeline.**
In this part, i integrated a Large Language Model (LLM) with the machine learning model developed in part 3.
The best performing model saved in part 3 ("best_model.pkl") is loaded and used to predict the class and probabilityfor three differenthouse records.
These predictions are then passed to an LLM through the OpenRouter API, which generates a structure JSON explanation describing the prediction.
To make the system more reliable , i validated every LLM response using a JSON schema and addeda PII (Personally Identifiable Information) guardrail before every API call.

# Dataset
I continued using the **"Ames Housing Dataset"**
The cleaned datset created in part and the processed features from part 2 were reused without any modifications.

# Step performed
1.Load the best model:
The best model saved in part 3 was loaded using Joblib - **"best_model.pkl"**
This avoids training the model again and allows direct prediction.
2.Load the dataset:
The cleaned dataset - **"cleaned_data.csv"** was loaded.
The target variable was converted into a binary classification problem: 
  1 - SalePrice greater than the median 
  0 - SalePrice less than or equal to the median
Categorical variables were converted using one-hot encoding before prediction.
3.Store the API key securely:
Instead of hardcoding the API key it was stored as an environment variable - **os.environ["LLM-API-KEY"]**
This improves security and follows good development practices.
4.Create the LLM API function:
A resuable function named **call_llm()** was created.
The function:

  - Accepts system prompt
  - Accept user prompt
  - Supports temperature
  - Supports max_tokens
  - Sends an HTTP POST request
  - Checks API response
  - Returns only the generated content
5.Test the API
The API connection was verified using a single prompt.
  System prompt : "You are a helpful assistant"
  User prompt : "Reply with only the word:hello"
  Output : "hello"
This confirmed that the API connection was working  correctly.

# Prompt Design
**System Prompt:**
system_prompt="""
you are an AI assistant that explains machine learning predictions.
Return ONLY valid JSON.
The JSON must contain exactly these fields:
{
"prediction_label":"string,
"confidence_level":"low|medium|high",
"top_reason":"string",
"second_reason":"string",
"next_step":"string"
}
Do not include any extra text.
"""
**User Prompt Template:**
"""
Feature values:{feature_values}
Predicted class:{prediction}
Prediction Probability:{probability}
Return only valid JSON
"""

# Temperature
**Why i used temperature = 0**
Because this project requires structured and deterministic JSON outputs.
A low temperature makes the model choose the highest-probability token at every step, producing more consistent responses.
This is important because every response must match the JSON schema before validation.
  **I observed between 0 and 0.7:**
    Temperature=0 always produce more deterministic and repeatable outputs.
    Temperature=0.7 introduces rabdomness by sampling from a boarder probability distribution.
    
# Structured Output Validation
A JSON schema was defined containing five required fields.
Required fields:  - prediction_label
                  - confidence_level
                  - top_reason
                  - second_reason
                  - next_step
After every LLM response: 1.Remove extra whitespace.
                          2.Parse using **json.loads()**.
                          3.Validate using **jsonschema.validate()**.
                          4.If validation fails return a fallback dictionary where every field is **None**.
                          
# PII Guardrail
Before every LLM request the input is checked for Personally Identifiable Information (PII).
The following patterns are detected: - Email Addresses.
                                     - Phone numbers.
If PII is detected the API call is blocked.
Example:
Input: My email is abc@gmail.com      | My house has 1 bedroom
output: Input blocked: PII detected   | The request is sent successfully to the LLM, This protects sensitive user information

# Model Prediction Pipeline
Three house records were selected from the test dataset.
For every sample:
1.Predict the class using - predict()
2.Predict probability using - predict_proba()
3.Create the user prompt.
4.Check for PII.
5.Send the prompt to the LLM.
6.Recieve Structures JSON.
7.Validate the JSON schema.

# All the results are shown in the part4.ipynb file
# End-to-End Demonstration
| Sample | Prediction | LLM Output | Valid JSON | Guardrail |
|----------|------------|------------|------------|-----------|
| Sample 1 | 1 | JSON explanation generated | PASS | Allowed |
| Sample 2 | 1 | JSON explanation generated | PASS | Allowed |
| Sample 3 | 1 | JSON explanation generated | PASS | Allowed |

# Why i used OpenRouter/Auto
I selected the model **"openrouter/auto"** because OpenRouter automatically routes requests to the most suitable available language model.
And i tried many model thay all send 429 error because of too busy and too many request so i choose this.

# Conclusion
In this part i successfully integrated an LLM with the machine learning model developed in part3.
The trained model generated predictions while the LLM produced structured JSON explanations for each prediction.
JSON schema validation ensured consistent outputs andthe PII guardrail protected sensitive information before every API  call.
This project demonstrates how traditional machine learning models and large language models can be combined to build reliable and explainable AI applications.
