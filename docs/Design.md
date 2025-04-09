# Application Design Summary

This document outlines the design for a web application to capture odometer and gas pump data from photos, using Next.js, Tesseract.js for OCR, Google Sheets for storage, and deploying on Vercel.

**1. Overall Architecture:**

- A single **Next.js** application will manage both the frontend user interface (React components) and the backend API logic (API Routes).
- The entire application will be deployed to **Vercel**.

**2. Frontend (Next.js Pages/Components):**

- **UI:** Built with React components within the Next.js framework.
- **Input:** Two file input elements (`<input type="file" accept="image/*" capture="environment">`) for mobile camera access:
  - Odometer photo upload.
  - Gas Pump photo upload.
- **Previews:** Display thumbnails of selected images.
- **Action:** A "Process Photos" button to trigger backend processing.
- **Confirmation:** An area displaying OCR results in editable input fields for user review and correction:
  - Odometer
  - Volume (L)
  - Total Price (€)
  - Price/Litre (€/L)
- **Save Action:** A "Confirm & Save" button to submit the final data.
- **Feedback:** Status messages (Processing, Saved, Error).

**3. Backend (Next.js API Routes):**

- **`Route 1: /api/process-images`**
  - **Method:** `POST`
  - **Input:** Accepts image files (`FormData`).
  - **Processing:** Uses **Tesseract.js** server-side within the Vercel serverless function. Configured specifically for digits/relevant characters (`tessedit_char_whitelist: '0123456789.,€'`). Parses text output to identify numbers.
  - **Output:** JSON response with extracted numbers or an error message.
- **`Route 2: /api/save-entry`**
  - **Method:** `POST`
  - **Input:** JSON data with user-confirmed numbers.
  - **Processing:** Adds a timestamp. Uses a Node.js library (e.g., **`google-spreadsheet`**) to authenticate with Google Sheets API (using Service Account credentials) and append a new row with the data.
  - **Output:** JSON response indicating success or failure.

**4. OCR Implementation:**

- **Engine:** Tesseract.js (via WASM) running server-side in Node.js.
- **Configuration:** Whitelist relevant characters (`0123456789.,€`) for optimal performance and accuracy on numeric displays.
- **Key Consideration:** Performance (speed, memory) and package size must be tested against Vercel's serverless function limits.

**5. Data Storage:**

- **Backend:** Google Sheets.
- **Access:** Via Node.js library (e.g., `google-spreadsheet`) from the `/api/save-entry` route.
- **Authentication:** Google Cloud Service Account. Credentials (JSON key) stored securely as **Vercel Environment Variables**.

**6. Deployment:**

- **Platform:** Vercel.
- **Process:** Connect Git repository (containing the Next.js project) to Vercel for automated builds and deployments. Configure necessary environment variables in Vercel project settings.

This design aims for a streamlined development experience within the Next.js ecosystem while tackling the OCR challenge using Tesseract.js within the constraints of the Vercel platform.
