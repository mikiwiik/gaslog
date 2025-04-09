# ADR-004: Deployment Platform

- **Status:** Accepted
- **Context:** The unified Next.js application, including the frontend, API routes, and the embedded Tesseract.js OCR logic, requires a hosting platform. Options included various PaaS providers, container platforms, or VPS solutions. The choice of Next.js makes platforms with first-class support for it attractive.
- **Decision:** Deploy the Next.js application to **Vercel**.
- **Consequences:**
  - **(+) Pro:** Offers a highly optimized and streamlined deployment experience specifically for Next.js applications (Git push-to-deploy).
  - **(+) Pro:** Automatically handles build processes, static asset hosting, CDN distribution, and deployment of API routes as serverless functions.
  - **(+) Pro:** Provides valuable platform features like preview deployments, analytics, integrated environment variable management, and HTTPS by default.
  - **(+) Pro:** Offers a generous free tier suitable for personal projects and scaling options if needed.
  - **(-) Con:** API routes execute as serverless functions, subject to platform limitations (execution time, memory, package size, cold starts) which directly influenced the OCR engine choice (ADR-002).
  - **(-) Con:** While Next.js itself is portable, deep integration relies on Vercel's specific build and runtime environment features.
