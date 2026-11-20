# Project Pulse Implementation Plan

## Summary and goal

Build a small, polished static **Project Pulse** dashboard for Mona's contributors. The dashboard must quickly show project name, owner, status, recent activity, priority, and a concise contributor-friendly summary. It will use plain HTML, CSS, and JSON, run locally through VS Code, and open the dashboard page rather than a directory listing.

## Ordered implementation phases

1. **Confirm the static-app contract**
   - Review the repository brief and existing agent guidance.
   - Agree on a plain HTML/CSS/JavaScript implementation that fetches `app/project-data.json`.
   - Establish the project-card DOM and status/priority presentation before implementation.

2. **Prepare data and presentation structure**
   - Create `app/project-data.json` with a top-level `projects` array.
   - Give every project `name`, `owner`, `status`, `recentActivity`, and `priority`.
   - Define the semantic structure in `app/index.html`, with the exact visible title **Project Pulse** and a class for the dashboard plus cards.

3. **Build the polished frontend**
   - Have the Designer guide visual hierarchy, accessible markup, status badges, responsive layout, contrast, spacing, and card treatment.
   - Have the Coder implement the HTML/JavaScript integration and data loading in `app/index.html`.
   - Apply the Designer's visual direction in `app/styles.css`, including `.dashboard`, `.project-card`, `border-radius`, `box-shadow`, and responsive behavior.

4. **Create the launch configuration**
   - Add `.vscode/launch.json` as strict JSON with no comments.
   - Configure a launch named **Run Project Pulse Dashboard** to run `python3 -m http.server 5500` from `${workspaceFolder}/app`.
   - Use `serverReadyAction` to open `http://localhost:%s/index.html`, ensuring the dashboard index is opened instead of the server directory.

5. **Integrate, validate, and hand off**
   - Confirm the HTML, CSS, JSON, and launch configuration work together.
   - Exercise the dashboard through the VS Code launch command and review desktop/mobile appearance and project-card content.
   - Report the final result, validation evidence, and any remaining limitations.

## File assignments

- `app/index.html` — Coder implementation, informed by Designer decisions: page title **Project Pulse**, stylesheet/data references, semantic dashboard structure, fetch of `project-data.json`, and rendering of project cards with the `project-card` class. Display owner, status, recent activity, and priority for each project.
- `app/styles.css` — Designer owns visual decisions and Coder applies them: polished `.dashboard` and `.project-card` styling, status and priority affordances, readable typography and spacing, rounded corners, shadows, and responsive layouts.
- `app/project-data.json` — Coder creates and validates the static data: strict JSON with top-level `"projects"` and complete project objects.
- `.vscode/launch.json` — Coder creates and validates the support configuration: exact name **Run Project Pulse Dashboard**, working directory `${workspaceFolder}/app`, command `python3 -m http.server 5500`, and a `serverReadyAction` targeting `http://localhost:%s/index.html`.

## Designer responsibilities

- Define the information hierarchy and contributor-friendly card layout.
- Create visible status and priority treatments, clear typography, contrast, rounded cards, shadows, and readable spacing.
- Ensure keyboard/accessibility-friendly semantics, useful labels, and responsive behavior without relying on hover alone.
- Avoid decorative changes that reduce clarity or create implementation conflicts.
- Report design decisions and validation recommendations.

## Coder responsibilities

- Implement the static app in `app/index.html`, `app/styles.css`, and `app/project-data.json` within the assigned file scopes.
- Use a deterministic, simple fetch/render implementation and explicit handling for invalid or unavailable data.
- Add `.vscode/launch.json` because the runnable app requires preview support.
- Keep `.vscode/launch.json` strict JSON with no comments and test the exact launch behavior.
- Validate changes and report risks or unresolved issues.

## Dependencies

- The HTML structure depends on the final JSON field names and card contract.
- CSS styling depends on stable hooks in the HTML, especially `.dashboard` and `.project-card`.
- The launch configuration depends on `app/index.html`, `styles.css`, and `project-data.json` being present.
- Final browser validation depends on the integrated app files and a working static HTTP server.

## Work that can run in parallel

- Designer can define layout, spacing, colors, badges, accessibility, and responsive rules.
- Coder can establish the JSON data shape and the launch configuration.
- The HTML structure and CSS can be drafted together only after the card field contract is agreed; they should otherwise be coordinated through the shared file assignments.

## Work that must run sequentially

1. Define and confirm the JSON fields and card structure.
2. Create or update `project-data.json` and `index.html` around that contract.
3. Apply or integrate CSS styling and verify the DOM hooks.
4. Add the launch configuration.
5. Run the launch and perform the final browser and JSON validation.

## Edge cases

- Empty or missing project data should not leave a blank, unexplained page; show an explicit state if the fetch fails or the array is empty.
- Project fields may contain punctuation or varied text lengths; cards must wrap cleanly and remain readable.
- Status and priority values should be normalized visually through labels rather than assuming fixed class names.
- Long recent-activity text should not overflow cards or break the responsive grid.
- Small screens and reduced-width panels require a single-column or comfortably wrapping layout.
- Fetching JSON via `file://` may fail; the launch's HTTP server is required for reliable loading.
- The launch server must use port 5500 and open `index.html`; it must not open a directory listing or another HTML page.

## Validation expectations

- `app/index.html` exists and contains the exact title **Project Pulse**.
- `app/index.html` references `styles.css` and `project-data.json`, renders project cards, and uses `project-card`.
- `app/styles.css` exists and includes `.dashboard`, `.project-card`, `border-radius`, `box-shadow`, and responsive rules.
- `python3 -m json.tool app/project-data.json` succeeds.
- `app/project-data.json` has a top-level `projects` array; every project includes `name`, `owner`, `status`, `recentActivity`, and `priority`.
- `python3 -m json.tool .vscode/launch.json` succeeds with strict JSON.
- `.vscode/launch.json` contains **Run Project Pulse Dashboard**, `${workspaceFolder}/app`, `python3 -m http.server 5500`, and `http://localhost:%s/index.html`.
- Running **Run Project Pulse Dashboard** opens in the browser and displays visible cards and their status, recent activity, and priority values.
- Check the first view at a normal desktop width and a narrow/mobile width.
- Stop the preview server after validation.

## Open questions

- What sample project count and names should represent Mona's team if the repository brief does not prescribe exact values?
- Are priority labels expected to use fixed vocabulary (for example Low/Medium/High) or free-form text?
- Are status labels expected to use fixed vocabulary (for example Active/At Risk/Complete) or free-form text?
- Should the UI include filtering, sorting, or detail interactions now, or remain a read-only contributor overview for this exercise?
