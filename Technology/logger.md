### 🔍 Logging Enhancement Prompt
Your mission is to **add comprehensive, human-readable logging** to the code you are about to modify or generate so that the entire user flow—from initial trigger to final outcome—is traceable in a single run.

**Requirements**

1. **Destination**
   - Log exclusively to STDOUT for back-end languages (e.g., `puts` in Ruby, `print()` in Python, `System.out.println` in Java) or to the JavaScript/TypeScript console (`console.log`, `console.warn`, `console.error`).
   - **Do NOT** add or configure external logging libraries unless I explicitly ask for them.

2. **Coverage**
   - Emit a log entry at every significant step:
     - Entry and exit of major functions/methods, including parameter values and return data.
     - External-system boundaries (HTTP requests/responses, DB queries, file I/O, third-party API calls).
     - Branching decisions, retries, and error-handling paths.
   - Include at least one high-level “START <task-name>” and “END <task-name>” marker so the whole journey is bracketed in the logs.

3. **Content**
   - Prefix each line with a timestamp in ISO-8601 format and the smallest useful unit of context (e.g., request ID, user ID, or correlation token if available).
   - Compose clear, sentence-style messages that explain **what** is happening and **why** it matters, not just variable dumps.
   - For errors or exceptions, log both the message and stack trace (or language equivalent).

4. **Performance**
   - Keep the logging lightweight—simple string interpolation only. No JSON serialization, structured log frameworks, or colorized output unless asked.

5. **Consistency**
   - Apply the same style and level of detail throughout the file/module so that a maintainer can skim the logs and reconstruct the end-to-end flow without referencing the code.

> **Remember:** The goal is observability, not noise. Strike the balance: enough data to replay and debug the scenario, but not so much that the signal is buried.
