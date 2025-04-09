## User Stories for OCR Mileage App

Based on the application design, here are the user stories outlining the core functionalities:

**Photo Upload & Preview:**

- As a user, I want to select or capture an odometer photo using my device so that I can input the mileage image for processing.
- As a user, I want to select or capture a gas pump photo using my device so that I can input the refueling details image for processing.
- As a user, I want to see a preview/thumbnail of the selected odometer photo so that I can verify I uploaded the correct image.
- As a user, I want to see a preview/thumbnail of the selected gas pump photo so that I can verify I uploaded the correct image.

**Data Processing & Confirmation:**

- As a user, I want to initiate the processing of both uploaded photos with a single button click so that the system starts extracting data.
- As a user, I want the system to automatically perform OCR on the odometer photo to extract the mileage reading so that I don't have to enter it manually.
- As a user, I want the system to automatically perform OCR on the gas pump photo to extract the volume (L), total price (€), and price per litre (€/L) so that I don't have to enter them manually.
- As a user, I want the extracted numbers (Odometer, Volume, Total Price, Price/Litre) to be displayed clearly in editable fields after processing so that I can review them for accuracy.
- As a user, I want the ability to edit the numbers displayed after OCR so that I can correct any potential extraction errors.

**Data Saving & Feedback:**

- As a user, I want to confirm the (potentially corrected) data and save it with a single button click so that the refueling record is stored.
- As a user (implicitly wanting persistent storage), I want the confirmed data along with a timestamp to be saved as a new entry in my designated Google Sheet so that I have a historical log of my refueling stops.
- As a user, I want to see visual feedback (like status messages: "Processing...", "Saved!", "Error") so that I know the current state of the operation.
