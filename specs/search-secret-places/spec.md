# Search for Secret Places

## Feature Description

Users can search for secret places around their current location or a location they plan to visit. Results are displayed on an interactive map with markers and in a carousel with detailed information about each place.

---

## User Scenarios

### Scenario 1: Search for Secret Places
- **Actor**: A user looking for secret places.
- **Action**: The user sets their current location or a planned location. The user can choose to be geo-located through their device, and the app will request permission to access their location. Alternatively, the user can choose a location they intend to visit using a Google Places Autocomplete field. This field will be restricted to locations such as cities, neighborhoods, and postal codes.
- **Outcome**: The application displays an interactive map with markers for secret places and a carousel with detailed information about each place.

---

## Functional Requirements

### Frontend
1. The application must allow users to set their current location or a planned location.
2. The application must fetch and display secret places near the selected location.
3. The application must display results on an interactive map with markers.
4. The application must display results in a carousel with detailed information about each place.

### Backend
1. The backend must provide an API endpoint to query places based on location and search criteria.
2. The backend must validate incoming data.
3. The backend must store places in a database optimized for geo queries and full-text search.

---

## Success Criteria

1. Users can find secret places within 5 seconds of setting their location.
2. The map and carousel are updated dynamically without page reloads.
3. The application achieves a perfect Lighthouse score for performance, accessibility, best practices, and SEO.

---

## Assumptions

1. The backend service will handle geo queries and full-text search.
2. The Google Places API will provide reliable and accurate data for location-based searches.