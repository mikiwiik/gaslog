# ADR-002: OCR Engine Selection

- **Status:** Accepted
- **Context:** The core function requires extracting numbers from images of odometers and gas pumps. Options included:
  1.  Native Tesseract engine (requires specific server environment or Docker, difficult in standard serverless).
  2.  Cloud OCR APIs (e.g., Google Vision; external dependency, potential cost).
  3.  Lighter JavaScript/WASM OCR engines (e.g., Ocrad.js; potentially lower accuracy).
  4.  Tesseract.js (WASM port of Tesseract; runs in Node.js/browser).
      The primary deployment target (Vercel serverless functions, see ADR-004) heavily restricts the execution of arbitrary native binaries.
- **Decision:** Implement OCR using **Tesseract.js**, running **server-side** within the Next.js API routes. Configure Tesseract.js specifically for digits and relevant characters (`tessedit_char_whitelist: '0123456789.,€'`) to optimize for the specific use case.
- **Consequences:**
  - **(+) Pro:** Enables OCR processing within the standard Vercel Node.js serverless environment without needing custom runtimes or external binaries.
  - **(+) Pro:** Keeps the OCR logic self-contained within the application's codebase.
  - **(+) Pro:** Leverages the power of the underlying Tesseract engine via WebAssembly.
  - **(-) Con:** Performance (execution time, CPU, memory usage) and package size (Tesseract.js core + language data) must be carefully evaluated against Vercel's function limits. Potential for timeouts or memory issues with complex images or high load.
  - **(-) Con:** May exhibit different performance or accuracy characteristics compared to a native Tesseract installation. Requires testing.
