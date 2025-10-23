# Secret Places Application Specifications

## Feature Description

This application allows users of a community to share their secret places based on a common interest. The application has two main features:

1. **Search for Secret Places**: Users can search for secret places around their current location or a location they plan to visit. Results are displayed on an interactive map with markers and in a carousel with detailed information about each place.
2. **Submit a New Place**: Users can submit a new secret place to the community. Submissions include basic information (retrieved from the Google Places API) and user-provided details (e.g., reviews, comments). Submissions are verified before being added to the database.

---

## User Scenarios

### Scenario 1: Search for Secret Places
- **Actor**: A user looking for secret places.
- **Action**: The user sets their current location or a planned location. The user can choose to be geo-located through their device, and the app will request permission to access their location. Alternatively, the user can choose a location they intend to visit using a Google Places Autocomplete field. This field will be restricted to locations such as cities, neighborhoods, and postal codes.
- **Outcome**: The application displays an interactive map with markers for secret places and a carousel with detailed information about each place.

### Scenario 2: Submit a New Place
- **Actor**: A user who wants to share a secret place.
- **Action**: The user fills out a submission form with the place's name, location, and additional details. Basic information is retrieved from the Google Places API.
- **Outcome**: The submission is stored in the backend for verification. Once verified, the place is added to the database and displayed in the search results.

---

## Functional Requirements

### Frontend
1. The application must allow users to set their current location or a planned location.
2. The application must fetch and display secret places near the selected location.
3. The application must display results on an interactive map with markers.
4. The application must display results in a carousel with detailed information about each place.
5. The application must provide a form for users to submit a new place.
6. The form must allow users to input the place's name, location, and additional details.
7. The application must retrieve basic information about the place from the Google Places API.
8. The application must use a typed API client to interact with the backend.

### Backend
1. The backend must provide an API endpoint to query places based on location and search criteria.
2. The backend must provide an API endpoint to submit a new place.
3. The backend must validate incoming data.
4. The backend must store places in a database optimized for geo queries and full-text search.
5. The backend must use a lightweight and efficient server framework.

---

## API Endpoints

### GET /places
- **Description**: Retrieve a list of secret places based on location and search criteria.
- **Query Parameters**:
  - `lat` (number): Latitude of the location.
  - `lng` (number): Longitude of the location.
  - `radius` (number): Search radius in kilometers.
  - `query` (string, optional): Full-text search query.
- **Response**:
  - `200 OK`: Returns a list of places matching the criteria.
  - `400 Bad Request`: Invalid query parameters.
  - `500 Internal Server Error`: Server error.

### POST /places
- **Description**: Submit a new secret place.
- **Request Body**:
  - `name` (string): Name of the place.
  - `type` (park | restaurant | bar | coworking) One of the accepted type of places.
  - `location` (object):
    - `lat` (number): Latitude of the place.
    - `lng` (number): Longitude of the place.
  - `description` (string): Description of the place.
  - `rating` (0-5): Number on a scale from 0 to 5 stars.
  - `picture` (string): Path (URL) to an external picture or a locally uploaded picture.
- **Response**:
  - `201 Created`: Place submitted successfully.
  - `400 Bad Request`: Invalid request body.
  - `500 Internal Server Error`: Server error.

---

## Success Criteria

1. Users can find secret places within 1 seconds of setting their location.
2. The map and carousel are updated dynamically without page reloads.
3. Users can submit a new place with an auto-completed form from a Google Place search.
4. Submissions are validated and stored in the backend without errors.
5. Verified places are added to the database and displayed in the search results.
6. The application achieves a perfect Lighthouse score for performance, accessibility, best practices, and SEO.

---

## Key Entities

1. **Place**:
   - Attributes: `id`, `name`, `location`, `description`, `rating`, `picture`, `verified`
   - Relationships: Linked to user submissions and Google Places API data.

2. **Submission**:
   - Attributes: `id`, `place_id`, `user_id`, `status` (e.g., pending, verified, rejected), `timestamp`

---

## Assumptions

1. The backend service will handle geo queries and full-text search.
2. The Google Places API will provide reliable and accurate data for place submissions.
3. Verification of submissions will be a manual or automated process handled outside the application.
4. The typed API client will ensure all requests and responses conform to the expected schema.