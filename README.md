Highlights & Key Findings

• AI successfully analyzed regression repositories and identified core execution flows with minimal manual guidance.

• Copilot demonstrated the ability to reconstruct automation scripts by interpreting existing test logic and navigation steps.

• Rapid prototyping capability observed — new automation scripts can be generated significantly faster compared to manual development.

• Automation dependencies were partially detected, including configuration files, input data sources, and external utilities.

• Execution sequence understanding was possible when repository structure and naming conventions were reasonably consistent.

• Standalone automation generation is achievable, but requires sufficient context such as sample inputs, configuration files, and execution flow hints.

• Regression suites today are not fully AI-ready, primarily due to missing structured input/output capture mechanisms.

• Manual validations and user inputs still exist in several flows, which limits end-to-end automation reconstruction.

• Lack of descriptive comments and documentation reduces AI interpretation accuracy when analyzing complex automation logic.

• Model capability significantly impacts results — advanced code models demonstrated stronger contextual reasoning and more reliable code generation.


FACT CHECK

1. VS Code Copilot supports custom agents defined as .agent.md files.
2. These agents can store reusable context such as previous findings, bug fixes, and instructions.
3. Workspace instructions can be stored in .github/copilot-instructions.md.
4. Reusable prompts can be stored in .github/prompts/ to standardize workflows.
5. This allows building a learning loop where Copilot remembers previous findings and improves generation.

------------------------------------------------------------

COMPLETE WORKFLOW (AI AUTOMATION RECONSTRUCTION WITH LEARNING LOOP)

+---------------------------------------------+
| (A) Setup: Learning Context in VS Code IDE  |
|---------------------------------------------|
| - Custom Agent (.github/agents/*.agent.md)  |
| - Repo Instructions (.github/copilot-...)   |
| - Prompt files (.github/prompts/*.prompt.md)|
| - References to prior findings / bug fixes  |
+---------------------------+-----------------+
                            |
                            v
+---------------------------------------------+
| Step 1: DISCOVER (Discover Prompt)          |
|---------------------------------------------|
| Input: Repository                           |
|                                             |
| Actions:                                    |
| - Scan repository structure                 |
| - Detect automation entry points            |
| - Identify execution chains                 |
| - Detect dependencies and inputs            |
|                                             |
| Output:                                     |
| JSON catalog containing all execution flows |
| with entry points                           |
+---------------------------+-----------------+
                            |
                            v
+---------------------------------------------+
| User Selection                              |
|---------------------------------------------|
| - User reviews execution flows              |
| - User selects one or more flows            |
+---------------------------+-----------------+
                            |
                            v
+---------------------------------------------+
| Step 2: RECONSTRUCT (CreateWF Prompt)       |
|---------------------------------------------|
| Input: Selected Flow JSON + same repo       |
|                                             |
| Actions:                                    |
| - Rebuild selected execution flow           |
| - Generate standalone automation runner     |
| - Map dependencies                          |
| - Parameterize input data                   |
| - Create setup and run scripts              |
|                                             |
| Tooling: Selenium Agent                     |
| - Reduce manual user interaction            |
| - Reuse browser session/cookies             |
| - Maintain context across iterations        |
|                                             |
| Output:                                     |
| Standalone automation application           |
| (runner + setup + run scripts)              |
+---------------------------+-----------------+
                            |
                            v
+---------------------------------------------+
| Execute + Validate                          |
|---------------------------------------------|
| - Run generated automation                  |
| - Capture logs and execution results        |
| - Compare expected vs actual outputs        |
| - Record PASS / FAIL status                 |
+---------------------------+-----------------+
                            |
          +-----------------+------------------+
          |                                    |
          v                                    v
+------------------------------+     +--------------------------------+
| If FAIL / gaps               |     | If PASS / stable               |
|------------------------------|     |--------------------------------|
| - Missing dependencies       |     | - Promote to reusable template |
| - Manual steps detected      |     | - Add to automation library    |
| - Incorrect execution chain  |     | - Enable faster regression     |
| - Missing documentation      |     | - Scale automation generation  |
+---------------+--------------+     +--------------------------------+
                |
                v
+---------------------------------------------+
| Learning Loop                               |
|---------------------------------------------|
| - Update custom agent with findings         |
| - Add bug fixes and solutions               |
| - Record manual interactions needed         |
| - Improve prompts and documentation         |
|                                             |
| Result:                                     |
| AI becomes better at reconstructing flows   |
| over time with minimal human interaction    |
+---------------------------+-----------------+
                            |
                            +-----> Iterate

------------------------------------------------------------

DISCOVER PROMPT OUTPUT (JSON STRUCTURE)

{
  "repo": "repository-name",
  "generatedAt": "YYYY-MM-DD",
  "flows": [
    {
      "flowId": "FLOW_1",
      "flowName": "Login -> Search -> Submit",
      "entryPoint": {
        "file": "tests/login_test.py",
        "function": "test_login"
      },
      "chain": [
        {
          "step": 1,
          "action": "open_url",
          "ref": "config.BASE_URL"
        },
        {
          "step": 2,
          "action": "login",
          "ref": "pages/login.py::login()"
        },
        {
          "step": 3,
          "action": "search",
          "ref": "pages/search.py::search()"
        }
      ],
      "inputs": [
        "credentials",
        "search_term"
      ],
      "outputs": [
        "status",
        "screenshot_on_fail"
      ],
      "dependencies": [
        "config.yml",
        ".env",
        "testdata.xlsx"
      ]
    }
  ]
}

------------------------------------------------------------

CREATEWF OUTPUT STRUCTURE

Generated standalone automation package:

runner.py
requirements.txt
setup.bat / setup.sh
run.bat / run.sh
results.csv
input_template.xlsx (if required)

results.csv structure:

test_case_id
test_case_name
status (PASS / FAIL)
error_message

------------------------------------------------------------

KEY BENEFIT OF THE LEARNING LOOP

Each iteration improves Copilot's ability to:

- understand repository structures
- detect automation flows
- reduce manual intervention
- generate stable standalone automation scripts

Over time this creates a self-improving automation generation system.
