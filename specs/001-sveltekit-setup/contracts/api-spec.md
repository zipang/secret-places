# API Specification

## Base URL
`/api`

## Authentication
Currently public API - authentication to be implemented in future iterations.

## Endpoints

### Submit Place

**POST** `/places/submit`

Submit a new secret place for verification.

**Request Body**:
```typescript
{
  name: string
  description: string
  location: {
    latitude: number
    longitude: number
    address: string
    city: string
    country: string
  }
  category: string
  images?: string[]
  tags?: string[]
}
```

**Response**:
```typescript
{
  success: boolean
  submissionId: string
  message: string
}
```

**Status Codes**:
- `201 Created`: Submission accepted
- `400 Bad Request`: Invalid data
- `500 Internal Server Error`: Server error

### Search Places

**GET** `/places/search`

Search for secret places near a location.

**Query Parameters**:
- `latitude` (required): Center latitude for search
- `longitude` (required): Center longitude for search
- `radius` (optional): Search radius in meters (default: 5000)
- `category` (optional): Filter by category
- `query` (optional): Text search query

**Response**:
```typescript
{
  places: Array<{
    id: string
    name: string
    description: string
    location: {
      latitude: number
      longitude: number
      address: string
      city: string
      country: string
    }
    category: string
    tags: string[]
  }>
  total: number
}
```

**Status Codes**:
- `200 OK`: Search successful
- `400 Bad Request`: Invalid parameters
- `500 Internal Server Error`: Server error

### Get Place Details

**GET** `/places/{id}`

Get detailed information about a specific place.

**Response**:
```typescript
{
  id: string
  name: string
  description: string
  location: {
    latitude: number
    longitude: number
    address: string
    city: string
    country: string
  }
  category: string
  submittedBy: string
  submittedAt: string
  verified: boolean
  images: string[]
  tags: string[]
}
```

**Status Codes**:
- `200 OK`: Place found
- `404 Not Found`: Place not found
- `500 Internal Server Error`: Server error

## Error Response Format

```typescript
{
  error: {
    code: string
    message: string
    details?: any
  }
}
```

## Rate Limiting
To be implemented in future iterations.

## CORS
API supports CORS for cross-origin requests.