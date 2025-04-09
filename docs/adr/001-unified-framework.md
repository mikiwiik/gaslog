# ADR-001: Unified Frontend/Backend Framework

- **Status:** Accepted
- **Context:** The application requires both a user interface (for photo upload, confirmation) and backend logic (API handling, OCR processing, data storage interaction). Initial options considered separating frontend (e.g., Vue) and backend (e.g., Python) technologies versus using a full-stack framework. The goal was to potentially simplify the development stack and deployment.
- **Decision:** Utilize the **Next.js** framework (React-based) to handle both frontend rendering (using Pages or App Router) and backend API logic (using API Routes).
- **Consequences:**
  - **(+) Pro:** Single codebase, language (JavaScript/TypeScript), and development environment simplifies context switching and project management.
  - **(+) Pro:** Tight integration between frontend components and backend API calls within the same framework.
  - **(+) Pro:** Leverages Next.js features like file-based routing, optimized builds, serverless function deployment for APIs, and image optimization.
  - **(-) Con:** Backend technology choice is inherently tied to the frontend framework's ecosystem (Node.js).
  - **(-) Con:** All server-side logic must operate within the capabilities and constraints of the Node.js environment chosen for Next.js.
