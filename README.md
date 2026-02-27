====================================================
PROMPT A — PACKAGE INVENTORY (NO CHANGES ALLOWED)
====================================================

You are performing PACKAGE ANALYSIS ONLY for this .NET Framework 4.8 solution.

SOLUTION STRUCTURE:
- 1 Web API project
- 2 Class Library projects

STRICT RULES:
- Do NOT modify any code.
- Do NOT upgrade any package.
- Do NOT edit csproj or packages.config.
- Do NOT convert to PackageReference.
- Analysis only.

TASK:
1) For each project, identify:
   - Target framework
   - packages.config or PackageReference usage
   - All direct NuGet packages (name + version)
   - Any visible transitive dependencies (if determinable)
2) For each package, identify:
   - Which project uses it
   - Best-effort usage detection (namespaces/types)
   - Key files where used (best effort)
3) Flag:
   - System.Web dependencies
   - Microsoft.AspNet.WebApi.*
   - OWIN/Katana packages
   - Unity.WebApi resolver packages
   - Any .NET Framework-only libraries

OUTPUT FORMAT (THREE TABLES):
package | current version | project | usage (namespace/types) | net8 compatible? | notes



====================================================
PROMPT B — .NET 8 COMPATIBILITY + REPLACEMENT MAP
====================================================

Now perform compatibility classification for all discovered packages.

STRICT RULES:
- Do NOT change code.
- Do NOT upgrade packages yet.
- If uncertain, mark as UNKNOWN.

TASK:
For each project (WebApi, ClassLib1, ClassLib2):

Classify each package as:
- OK (works on .NET 8)
- Needs Upgrade (newer version supports .NET 8)
- Replace (no .NET 8 support)
- Remove (obsolete in .NET 8 / built-in alternative exists)
- UNKNOWN (needs manual validation)

For packages marked Replace:
- Suggest minimal-change replacement
- Estimate code impact (LOW / MED / HIGH)

Call out specifically:
- System.Web dependencies
- ASP.NET WebApi 2 packages
- OWIN/Katana
- Unity.WebApi resolver extensions
- Configuration-related legacy packages
- Old JSON libraries
- WCF packages
- Authentication libraries

OUTPUT:
1) Three per-project tables:
   package | old version | classification | replacement | impact | reason
2) Top migration blockers list
3) Minimal-change replacement set summary



====================================================
PROMPT C — COMMAND-BASED EXTRACTION (SAFE MODE)
====================================================

Perform package extraction using safe read-only methods.

STRICT RULES:
- Do NOT modify files.
- Do NOT restore or upgrade packages.
- Do NOT change target framework.

TASK:
1) Detect and parse:
   - packages.config files
   - csproj files (PackageReference entries)
2) If safe to run:
   - dotnet --info
   - dotnet list <project> package (if supported)
3) If dotnet list fails (due to .NET Framework project),
   fallback to parsing packages.config manually.
4) Produce consolidated package inventory per project.

OUTPUT:
Three tables:
package | version | project | package source file



====================================================
PROMPT D — FINAL PACKAGE RISK SUMMARY
====================================================

Generate a final risk summary before migration.

TASK:
1) Identify which packages BLOCK:
   - Class library upgrade
   - Web API upgrade
2) Identify:
   - Any packages tied to System.Web
   - Any Unity extensions incompatible with .NET 8
   - Any serialization packages that may change output behavior
3) Categorize risks:
   - Build risk
   - Runtime behavior risk
   - Serialization risk
   - DI lifetime risk

OUTPUT:
- Critical blockers list
- Moderate risk list
- Safe-to-upgrade list
- Migration order recommendation (libs first, Web API last)

DO NOT MODIFY CODE.

===============================
PROMPT 1 — DISCOVERY + PLAN
===============================

You are a .NET modernization agent.

GOAL:
Convert this multi-project solution from .NET Framework 4.8 to .NET 8.

SOLUTION:
- 1 Web API project (multiple controllers)
- 2 Class Library projects
- Shared Factory pattern
- Unity resolver for DI
- Interface-only usage (no direct implementation usage)

STRICT EXECUTION MODE:
- Do NOT modify business logic.
- Do NOT refactor.
- Do NOT optimize.
- Do NOT reorder execution steps.
- Do NOT change method signatures unless required for compilation.
- If uncertain, STOP and report file + line.

TASK:
1) Identify all projects and project references.
2) Identify target frameworks.
3) Inventory all NuGet packages per project.
4) Identify bootstrapping points (Global.asax, WebApiConfig, UnityConfig, Startup, etc.).
5) Produce migration order (libraries first, Web API last).
6) Produce per-project upgrade checklist.

OUTPUT:
- Project dependency graph
- Package compatibility report (per project)
- Bootstrapping migration plan
- Ordered migration checklist
- Risk list


===============================
PROMPT 2 — UPGRADE CLASS LIBRARIES FIRST
===============================

Focus ONLY on the two Class Library projects.

STRICT EXECUTION MODE:
- Do NOT change business logic.
- Do NOT change interfaces unless unavoidable.
- Do NOT refactor or optimize.
- Replace only framework-incompatible APIs.

TASK:
1) Upgrade both class libraries to net8.0.
2) Migrate packages to .NET 8 compatible versions.
3) Replace .NET Framework-only APIs with .NET 8 equivalents while preserving behavior.
4) Ensure both libraries build successfully before touching Web API.

DELIVER:
- List of changes per library
- Package replacements
- Any behavior-risk warnings


===============================
PROMPT 3 — MIGRATE WEB API HOST
===============================

Now migrate the Web API project to .NET 8 ASP.NET Core.

STRICT EXECUTION MODE:
- Do NOT modify business logic.
- Preserve routes, status codes, and response models.
- Preserve Factory pattern.
- Preserve interface-only access.
- Preserve DI lifetime behavior.

TASK:
1) Upgrade or create .NET 8 ASP.NET Core Web API host.
2) Reference upgraded class libraries.
3) Port controllers with minimal namespace/usings changes.
4) Identify routing differences and match behavior.
5) Match JSON serialization behavior (Newtonsoft if needed).
6) Ensure build + run success.

OUTPUT:
- File mapping (old → new)
- Routing parity mapping
- Serialization configuration
- Run instructions


===============================
PROMPT 4 — UNITY DI PRESERVATION
===============================

Focus on Unity container integration.

STRICT RULES:
- Do NOT change how dependencies are resolved.
- Do NOT change lifetimes.
- Do NOT remove factory pattern.
- Interface usage must remain intact.

TASK:
1) Locate all Unity registrations.
2) Produce full registration inventory:
   interface → implementation → lifetime → named registrations.
3) Choose approach:
   A) Keep Unity integrated into ASP.NET Core
   OR
   B) Map registrations to Microsoft DI ONLY if behavior remains identical.
4) Implement chosen approach.
5) Document any risk of behavior deviation.

OUTPUT:
- Registration inventory
- Chosen approach + reason
- Files changed
- Risk notes (if any)


===============================
PROMPT 5 — PACKAGE MIGRATION REPORT
===============================

Perform NuGet compatibility migration per project.

RULES:
- Same vendor if possible.
- Prefer stable/LTS versions.
- No behavioral changes.

TASK:
1) List packages for:
   - Web API
   - Class Library 1
   - Class Library 2
2) For each package:
   - current version
   - where used
   - .NET 8 support status
   - replacement (if required)
3) Update to PackageReference if needed.
4) Ensure solution builds.

OUTPUT:
Three tables (one per project):
package | old version | new version | compatible? | notes


===============================
PROMPT 6 — FINAL SAFETY VALIDATION
===============================

Perform strict diff review before finalizing migration.

TASK:
1) Identify any changes that could alter runtime behavior:
   - exception handling differences
   - serialization differences
   - DI lifetime differences
   - routing differences
2) If ANY behavior risk exists, STOP and list:
   - file
   - line
   - risk explanation
3) Confirm only if verified:
   "No business logic changed."

OUTPUT:
- Behavior risk report
- Final confirmation statement
Analysis only.
