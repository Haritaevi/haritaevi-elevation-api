# Changelog

All notable changes to this project will be documented in this file.

---

### Version 1.0.0

- Ability to retrieve elevation data using the **GET** method.
- Accepts latitude and longitude as parameters.

### Version 1.2.0

- Extended functionality to fetch elevation for **multiple latitude and longitude** pairs using the **GET** method with pipe-separated coordinates.

### Version 2.0.0

- Added support for **POST** method to retrieve elevations for multiple latitude and longitude pairs in **JSON format**.
- Introduced **caching** for faster response times.
- Implemented **concurrent request handling** to improve API performance.

### Version 3.0.0

- Introduced the ability to **update bounding boxes (bboxes)** automatically from the database.
- Added functionality to dynamically fetch bboxes during API operations.
- Enhanced the API to support elevation data retrieval from models **other than SRTM**, such as DSM (if available).
- Introduced the ability to query elevation data based on country codes, improving precision for multi-region requests.
- Optimized the API to reduce load on GeoServer, ensuring efficient performance and preventing server overload.

### Version 3.1.0

- **Compatible with `"W"` wildcard**, which includes all countries for automatic detection.
- **Country codes are now case-insensitive** (e.g., "tr", "Tr", "tR" will be treated the same as "TR").
- **Improved error handling** for cases when no country is found
- **Updated API documentation** to reflect the new functionality.

### Version 3.2.0

- **Added support for multiple `country_code` values** using the pipe (`|`) separator (e.g., `TR|QA`) in both **`GET`** and **`POST`** requests.
- **Each coordinate is evaluated against all matching country bounding boxes**. If the coordinate falls into more than one:
  - **If any bounding box has a child**, the API attempts to get elevation from the child first.
  - **If no child is present**, it uses the first matching bounding box.
  - If elevation is not found in that box, the API **falls back to the next candidate** in order.
- **Improved prioritization and fallback logic** to ensure better elevation coverage across regions.
- **Cleaner and more maintainable code structure** with clearer logic separation and better error handling.
- **Elevation values are now rounded to 2 decimal places** (e.g., `951.60`) for consistency and readability in API responses.
- **Structured and self-documented API schema added** (includes parameter types, authentication headers, and response formats for every endpoint — improving clarity and integration support)
- **Integrated interactive API testing environment** (allows developers to send live requests, inspect real-time responses, and validate parameters directly in the browser — improving development and debugging efficiency)
- **Added multilingual support (English & Turkish)** and redesigned the homepage with enhanced features and improved user experience.
- **Updated API documentation and usage examples** to reflect multi-country and fallback behavior.

### Version 3.3.0

- **Introduced pricing plans** with **Free** and **Professional** packages, allowing users to choose usage levels based on their needs.
- Added **API key–based authentication and authorization**:
  - Each request now requires a valid `apiKey`.
  - The system validates and grants access according to the user’s plan (**Free** or **Professional**).
  - Some legacy or test keys are supported **without full access control** for backward compatibility.
- Implemented **automated email notifications**:
  - Users receive confirmation emails upon registration.
  - If a registered user attempts to register again, the system informs them that the account is already registered.
- Updated backend logic to integrate **API key validation** and **pricing plan checks** seamlessly within existing API workflows.
- Enhanced the API documentation to include **authentication details**, **pricing tiers**, and **example usage** for both Free and Professional packages.
- Improved **system logging and monitoring** to track API usage and user activity for better transparency and support.

---
