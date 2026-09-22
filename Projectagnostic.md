You are analyzing the codebase in the current working directory (folder-agnostic — do not assume any specific project type or structure). Perform a full recursive scan and produce a PROJECT_STRUCTURE.md file with the following:

1. FULL DIRECTORY TREE
   - Every folder and file, nested correctly
   - Skip only: .git, node_modules, __pycache__, venv/.venv, dist/build artifacts

2. FILE INVENTORY TABLE
   For every source file (code, config, requirements, Dockerfiles, notebooks, etc.), list:
   - File path
   - File type/language
   - One-line inferred purpose (based on filename, imports, and a quick read)
   - Tier: entrypoint / core logic / utility / config / test / data / infra

3. TECH STACK SUMMARY
   - Languages detected
   - Frameworks/libraries (from requirements.txt, package.json, pyproject.toml, etc. — read these files directly)
   - Databases, vector stores, external APIs referenced anywhere in code
   - Build/deploy tooling (Docker, CI configs, etc.)

4. TABLE OF CONTENTS FOR DEEP DOCUMENTATION
   - Group files into logical modules/subsystems (e.g. "ingestion", "agents", "API layer")
   - This grouping will drive the deep-dive pass next

Output ONLY the PROJECT_STRUCTURE.md file. Do not summarize in chat — write it to disk. Do not skip any file due to size; if a file is very large, still list it and note "large file — deep dive in pass 2."






# part 2



Using PROJECT_STRUCTURE.md as your map, go through EVERY file listed and produce a single PROJECT_DOCUMENTATION.md (folder-agnostic — works for any project). For EACH file, open it and extract:

- File path & role (why it exists, what problem it solves in this project)
- All imports/dependencies used, and why each is needed
- Every function/class:
  - Name, parameters, return type
  - Purpose in plain text (what it does and why, not just what the code says)
  - Which other files/functions call it or are called by it
- Key variables/config values defined at module level
- Any external service/API/DB it talks to

Then produce these sections at the top of the document, before the file-by-file detail:

1. PROJECT OVERVIEW (learner-friendly)
   - What the project does, end to end, in plain language
   - Why it's built this way (design rationale)

2. TECH STACK
   - Full list with versions where available (pull from requirements.txt/package.json etc.)
   - One line per item: what it's used for in THIS project specifically

3. ARCHITECTURE & DATA FLOW (as a Mermaid diagram + textual walkthrough)
   - How folders/modules connect
   - How a request/input flows through the system start to finish
   - Textually describe the same flow in numbered steps, referencing exact file names and function names

4. HOW FILES ARE INTERCONNECTED
   - For each module/subsystem, describe which files import/call which, in plain text
   - Call out the "entry point" and trace the execution path from it

5. SETUP/REPRODUCTION NOTES
   - requirements.txt / dependency install
   - Environment variables/config needed
   - How to run it

Formatting rules:
- Plain text explanations throughout, not just code dumps
- Use consistent headers per file: ## <path> so the doc is navigable
- This file should be detailed enough that an AI coding assistant reading ONLY this document (with no access to the original code) could reconstruct the project's architecture and logic

Output ONLY PROJECT_DOCUMENTATION.md, written to disk.
