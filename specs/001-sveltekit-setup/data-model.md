# Data Model: Secret Places Application

## Core Entities

### Place Entity
Represents a secret place submitted by users.

```typescript
interface Place {
  id: string
  name: string
  description: string
  location: Location
  category: string
  submittedBy: string
  submittedAt: Date
  verified: boolean
  verificationDate?: Date
  images: string[]
  tags: string[]
}

interface Location {
  latitude: number
  longitude: number
  address: string
  city: string
  country: string
}
```

### User Entity
Represents application users (for future authentication).

```typescript
interface User {
  id: string
  username: string
  email: string
  createdAt: Date
  role: 'user' | 'admin'
}
```

### Submission Entity
Tracks place submissions for verification workflow.

```typescript
interface Submission {
  id: string
  place: Place
  submittedBy: string
  submittedAt: Date
  status: 'pending' | 'approved' | 'rejected'
  reviewedBy?: string
  reviewedAt?: Date
  reviewNotes?: string
}
```

## Validation Schemas (arktype)

### Place Schema
```typescript
const placeSchema = type({
  id: 'string',
  name: 'string > 0',
  description: 'string > 10',
  location: type({
    latitude: 'number',
    longitude: 'number',
    address: 'string > 0',
    city: 'string > 0',
    country: 'string > 0'
  }),
  category: 'string > 0',
  submittedBy: 'string',
  submittedAt: 'Date',
  verified: 'boolean',
  verificationDate: 'Date?',
  images: 'string[]',
  tags: 'string[]'
})
```

### Location Schema
```typescript
const locationSchema = type({
  latitude: 'number',
  longitude: 'number',
  address: 'string > 0',
  city: 'string > 0',
  country: 'string > 0'
})
```

### Submission Schema
```typescript
const submissionSchema = type({
  id: 'string',
  place: placeSchema,
  submittedBy: 'string',
  submittedAt: 'Date',
  status: type('pending', 'approved', 'rejected'),
  reviewedBy: 'string?',
  reviewedAt: 'Date?',
  reviewNotes: 'string?'
})
```

## Content Collections

### Static Content Structure
```
src/content/
├── en/
│   ├── pages/
│   ├── components/
│   └── navigation/
├── fr/
└── jp/
```

### Page Content Example
```markdown
---
title: "Submit a Secret Place"
description: "Share your favorite hidden spots with the community"
---

# Submit a Secret Place

Share your favorite hidden gems...
```

## API Contracts

### Submit Place Endpoint
```typescript
POST /api/places/submit
Body: {
  name: string
  description: string
  location: Location
  category: string
  images?: string[]
  tags?: string[]
}

Response: {
  success: boolean
  submissionId: string
  message: string
}
```

### Search Places Endpoint
```typescript
GET /api/places/search
Query: {
  latitude: number
  longitude: number
  radius?: number
  category?: string
  query?: string
}

Response: {
  places: Place[]
  total: number
}
```

## Data Flow

1. **User Input** → Google Places Autocomplete → Location data
2. **Form Submission** → arktype validation → API endpoint
3. **API Processing** → Data storage → Response
4. **Content Loading** → content-collections → Page rendering
5. **Search Query** → Geo filtering → Results display