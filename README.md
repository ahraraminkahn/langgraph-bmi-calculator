langgraph-bmi-calculator

A minimal LangGraph example that builds a two-step workflow to calculate Body Mass Index (BMI) and classify the result into a weight category.

It's a small, beginner-friendly demo of the core LangGraph concepts: state, nodes, edges, and compiling/invoking a graph.

How it works

The workflow is a simple linear graph:

START → calculate_bmi → tell_condition → END
Node	Description
calculate_bmi	Reads height (m) and weight (kg) from state and computes bmi = weight / height²
tell_condition	Reads bmi and sets condition based on the ranges below
BMI categories
BMI	Condition
< 18.5	underweight
18.5 – 24.9	normal weight
25 – 29.9	overweight
≥ 30	obese
State schema
python
class MyState(TypedDict):
    height: float     # in meters
    weight: float     # in kilograms
    bmi: float
    condition: str
Getting started
Prerequisites
Python 3.10+
Jupyter (or VS Code with the Jupyter extension)
Installation
bash
git clone https://github.com/<your-username>/langgraph-bmi-calculator.git
cd langgraph-bmi-calculator

python -m venv .venv
source .venv/bin/activate   # Windows: .venv\Scripts\activate

pip install langgraph langchain-core ipython jupyter
Run

Open main.ipynb and run all cells in order.

Example
python
workflow.invoke({"height": 1.75, "weight": 70})

Output:

python
{
  'height': 1.75,
  'weight': 70,
  'bmi': 22.857142857142858,
  'condition': 'normal weight'
}
Visualizing the graph

The notebook renders the workflow as a Mermaid diagram:

python
from IPython.display import Image, display

display(Image(workflow.get_graph().draw_mermaid_png()))

Note: draw_mermaid_png() calls an external rendering service by default, so an internet connection is required. Run the cell that compiles the graph (workflow = graph.compile()) before the cell that displays it.

Project structure
.
├── main.ipynb    # Graph definition, nodes, and example run
└── README.md
Possible extensions
Add conditional edges to route to different nodes per BMI category
Add input validation (e.g., height > 0)
Add an LLM node that generates personalized health advice
Support imperial units
