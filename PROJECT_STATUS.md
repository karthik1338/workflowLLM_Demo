# WorkflowLLM Project Status

## Stage 1: Planner

### Objective

Train a model to generate Task Plans from:

Input:

* User Query
* Available APIs

Output:

* Task Plan

### Model

* Base Model: Qwen2.5-3B-Instruct
* Training Method: LoRA via Unsloth
* Hardware: Google Colab T4

### Dataset

* Samples: 50
* Fields:

  * query
  * apis
  * task_plan
  * annotated_code

### Training Results

* Epochs: 20
* Final Loss: ~0.56
* Adapter Size: 115 MB

### Output

workflow_planner_lora/

### Status

Completed and producing reasonable task plans.

---

## Storage

### GitHub

Stores:

* notebooks
* scripts
* datasets
* documentation

### Hugging Face

Stores:

* workflow_planner_lora
* future GGUF exports

---

## Stage 2: Workflow Generation

### New Dataset

Fields:

* query
* task_plan
* workflow_code
* apis_used

### Goal

Input:

* Task Plan
* APIs

Output:

* Workflow Graph (Intermediate Representation)

Example:

{
"steps": [
{
"tool": "weather_currentconditions",
"output": "current_weather_conditions"
},
{
"tool": "text_replace",
"output": "formatted_temperature"
}
]
}

### Plan

1. Parse workflow_code.
2. Extract API calls.
3. Build workflow_graph.json labels.
4. Train Stage 2 model:
   Task Plan + APIs → Workflow Graph.

---

## Future Stages

Stage 3:
Workflow Graph → Python Code

Stage 4:
Python Code → Execution Engine

---

## Current Priority

Build workflow_code → workflow_graph parser and generate Stage 2 training data.
