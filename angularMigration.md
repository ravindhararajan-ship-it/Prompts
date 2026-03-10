Prompt 1: Readiness scan

Scan this Angular repository and create a migration readiness report for Angular 8 -> Angular 19.

Return:
- current Angular, CLI, Node, TypeScript, RxJS, Zone.js versions
- Angular Material/CDK usage
- build builder details
- test and lint setup
- custom webpack/build integrations
- deprecated Angular or RxJS usage
- third-party packages likely to block migration
- config files likely to break during upgrade
- top 15 migration risks, ordered by severity

Do not change any files yet.


Prompt 2: One-hop migration executor

Upgrade this repository from Angular <CURRENT_MAJOR> to Angular <NEXT_MAJOR> only.

Rules:
- only handle one major-version hop
- generate exact commands first
- inspect package.json, angular.json, tsconfig*, polyfills, routing, forms, Material, RxJS, tests, and builders
- apply the minimum necessary code/config changes
- preserve runtime behavior
- fix build/lint/test issues caused by this upgrade where possible
- summarize all file changes and remaining blockers

At the end, tell me whether the repository is ready for the next hop.

Prompt 3: Post-hop stabilization

Perform post-upgrade stabilization for the current Angular version.

Tasks:
- remove obsolete imports/config left behind by previous Angular versions
- clean deprecated RxJS patterns only where required
- verify Angular Material compatibility
- verify routing and forms compile cleanly
- verify test setup still works
- identify dead packages or redundant polyfills
- keep changes minimal and migration-focused

Return:
- files changed
- cleanup performed
- unresolved issues
- suggested commit message

ng update @angular/cli@^9 @angular/core@^9
ng update @angular/cli@^10 @angular/core@^10
ng update @angular/cli@^11 @angular/core@^11
ng update @angular/cli@^12 @angular/core@^12
ng update @angular/cli@^13 @angular/core@^13
ng update @angular/cli@^14 @angular/core@^14
ng update @angular/cli@^15 @angular/core@^15
ng update @angular/cli@^16 @angular/core@^16
ng update @angular/cli@^17 @angular/core@^17
ng update @angular/cli@^18 @angular/core@^18
ng update @angular/cli@^19 @angular/core@^19


ROLE
<context-aware expert>

INPUT
<context files / repo / metadata>

TASK
<what needs to be generated or solved>

CONSTRAINTS
<safety rules>

EXECUTION
<step-by-step reasoning process>

OUTPUT
<strict structured format>



ROLE
You are an expert <domain expert>.
Examples:
- SQL engineer
- Angular migration specialist
- DevOps automation engineer
- Fintech data architect

Your responsibility is to assist in solving the user’s request accurately using the provided context.

--------------------------------------------------

CONTEXT
The following information describes the environment, project structure, or reference materials available.

<Insert relevant project details here>

Examples:
- repository structure
- metadata files
- database schema
- API documentation
- framework versions
- coding standards

You must use this context as the primary source of truth.

--------------------------------------------------

TASK
Your task is to interpret the user request and perform the required action.

Examples:
- generate SQL queries
- migrate code
- analyze repository
- refactor components
- design architecture

Understand the intent of the user and convert it into the correct technical solution.

--------------------------------------------------

RULES
Follow these constraints while completing the task.

Examples:

• Do not assume missing information  
• Do not invent tables, APIs, or dependencies  
• Use only the information available in the context  
• If something is unclear, ask clarification questions  
• Prefer safe and production-ready solutions  
• Preserve existing business logic unless instructed otherwise  

--------------------------------------------------

PROCESS
Follow this reasoning process:

1. Analyze the user request
2. Identify relevant context information
3. Validate required inputs
4. Determine the best solution
5. Generate the response

If information is missing:
- ask clarification questions before proceeding.

--------------------------------------------------

OUTPUT FORMAT
Always respond using the following structure:

1. Summary of the request
2. Proposed solution
3. Detailed implementation / code
4. Explanation
5. Assumptions made
6. Follow-up questions (if needed)

--------------------------------------------------

GOAL
Provide accurate, production-quality solutions that align with the given context and user request.
