# AI-Friendly Reformulated Development Instructions

## Objective

You are tasked with implementing the dashboard for the `nbg-business-insights` project. Before coding begins, you must follow this exact process:

## Step-by-Step Procedure (Mandatory Order)

1. **Read the Main Instructions**  
   Open and carefully read:  
   `instructions.md`  
   Understand the task as fully and accurately as possible.

2. **Read All Referenced Files**  
   Any file references within `instructions.md` must also be opened and fully read before proceeding.

3. **Resolve All Ambiguities**  
   If any information is missing or unclear, pause and ask the user for clarification. Do not make any assumptions.

4. **Based on the api samples and `instructions.md` create a techndial document for the redux store. Name it `store.md` and place it in the root directory.

5. **Create a New Technical Design Document**  
   A previous version of the technical design has been deleted.  
   You must create a detailed new one from scratch.

   - The technical design must include detailed explanations of:
     - How bespoke components will provide mock data to metric components.
     - How mock data will be replaced with real data when available.
   - Refer constantly to:  
     `TECHNICAL_DESIGN.md`  
     If any deviation from that file is required, consult the user before proceeding.

## Implementation Warnings

- Do not start coding until steps 1–4 above are fully completed.
- Do not modify the wording or descriptions in `instructions.md` to match sample HTML.
- Only use `html_samples/simple-dashboard.html` for look and feel. Do not copy its text or structure.

## Tailwind CSS Integration Instructions

Follow these instructions as needed in order to install Tailwind CSS:

1. Install Tailwind CSS and the Vite plugin:
   ```
   npm install tailwindcss @tailwindcss/vite
   ```

2. Configure `vite.config.ts`:
   ```ts
   import { defineConfig } from 'vite'
   import tailwindcss from '@tailwindcss/vite'

   export default defineConfig({
     plugins: [
       tailwindcss(),
     ],
   })
   ```

3. Import Tailwind in your CSS file:
   ```css
   @import "tailwindcss";
   ```

## TypeScript Note

- `verbatimModuleSyntax` is enabled. Ensure import/export syntax is compatible.

## Project Setup Instructions

- You will provide scaffolding and bootstrapping commands (e.g. for project creation, library installation, and folder structure).
- These commands will be executed manually by the user.
- Consult tool Context 7 for library information

## Next Step

We are beginning with the dashboard implementation.

Before proceeding:
- Confirm that steps 1–4 are completed.
- Confirm that the technical design document is prepared.
