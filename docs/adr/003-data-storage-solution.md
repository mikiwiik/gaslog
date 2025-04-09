# ADR-003: Data Storage Solution

- **Status:** Accepted
- **Context:** The application needs to persistently store the extracted and confirmed refueling data (Timestamp, Odometer, Volume, Price, Price/Litre). Options ranged from browser `localStorage` (not persistent/shareable), deploying a traditional database (SQL/NoSQL, adds complexity/cost), or using a simpler cloud-based solution. User indicated Google Sheets was acceptable.
- **Decision:** Utilize **Google Sheets** as the primary data store for refueling records. Access will be handled programmatically from the Next.js API route using a Node.js library (e.g., `google-spreadsheet`) and authenticated via Google Cloud Service Account credentials.
- **Consequences:**
  - **(+) Pro:** Simple setup and management compared to a dedicated database.
  - **(+) Pro:** Data is easily viewable, editable, and exportable using the familiar Google Sheets interface.
  - **(+) Pro:** Leverages existing, reliable infrastructure with a generous free tier suitable for this application's scale.
  - **(-) Con:** Not a relational database; lacks features like enforced schemas, indexing, complex queries, and transactional integrity. Performance may degrade with very large datasets.
  - **(-) Con:** Dependent on Google Sheets API availability, quotas, and terms of service.
  - **(-) Con:** Requires secure management and storage of Service Account credentials.
