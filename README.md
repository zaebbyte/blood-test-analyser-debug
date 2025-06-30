# blood-test-analyser-debug
A comically overconfident AI-powered blood test report analyzer, built using CrewAI agents powered by GPT-based LLMs. This system includes multiple agents—Doctor, Verifier, Nutritionist, and Fitness Coach—each offering wildly opinionated "insights" from your uploaded blood report.

Bugs: 
Bug #1: `LLM` object not defined
**Problem**: `llm = LLM(model="gpt-4o-mini")` caused an error due to missing import.
**Fix**: Added `from crewai import LLM`

Bug #2: Improper import of `crewai_tools`
**Problem**: `import crewai_tools` used incorrectly.
**Fix**: Changed to correct module import: `from crewai_tools.tools.serper_dev_tool import SerperDevTool`

Bug #3: Missing import for `PDFLoader`
**Problem**: `PDFLoader` was undefined.
**Fix**: Added: `from langchain.document_loaders import PDFLoader`

Bug #4: Invalid `async def` methods inside class
**Problem**: Used `async def` without proper coroutine context or decorators.
**Fix**: Converted them to synchronous `def` methods (or wrap them with async support if needed in future).

Bug #5: Tools not returning correctly formatted strings
**Fix**: Ensured all tool methods return cleaned and concatenated string data.


# API DOUMENTAION
BloodTestReportTool

class BloodTestReportTool:
    def read_data_tool(self, path: str = 'data/sample.pdf') -> str
Description:
Reads and cleans text from a blood test PDF file using LangChain's PDFLoader.

Parameters:

path (str): Path to the PDF file (default: 'data/sample.pdf')

Returns:

(str): Full cleaned text content extracted from the PDF

NutritionTool

class NutritionTool:
    def analyze_nutrition_tool(self, blood_report_data: str) -> str
Description:
Processes blood report text and will analyze nutritional insights. Currently a placeholder with basic cleanup.

Parameters:

blood_report_data (str): Raw text content of the blood report

Returns:

(str): Nutrition analysis summary (mock output for now)

ExerciseTool

class ExerciseTool:
    def create_exercise_plan_tool(self, blood_report_data: str) -> str
Description:
Plans an exercise routine based on blood report insights (placeholder logic).

Parameters:

blood_report_data (str): Raw text content of the blood report

Returns:

(str): Exercise plan suggestion (mock output for now)


LLM

from crewai import LLM

llm = LLM(
    model="gpt-4o-mini",  # or "gpt-4", "gpt-3.5-turbo", etc.
    temperature=0.8
)
Description:
Initializes the Large Language Model used by all CrewAI agents.

Parameters:

model (str): OpenAI model ID

temperature (float): Creativity level (0 = deterministic, 1 = very creative)
