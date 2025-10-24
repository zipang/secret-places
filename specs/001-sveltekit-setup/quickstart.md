# Quick Start: SvelteKit Setup

## Prerequisites

- Bun runtime
- Google Maps API key

## Setup Commands

```bash
# Create SvelteKit project
bun create svelte@latest secret-places
cd secret-places

# Install dependencies
bun install

# Install required packages
bun add @googlemaps/js-api-loader content-collections arktype

# Install dev dependencies
bun add -d @types/google.maps

# Initialize BiomeJS
bunx @biomejs/biome init
```

## Project Structure Setup

```bash
# Create directory structure
mkdir -p src/components/{base,ui,app}
src/content
src/entities
src/services
src/routes/{api,pages}

# Create README files
echo "# Base Components\n\nFoundational layout and text components (Atoms)" > src/components/base/README.md
echo "# UI Components\n\nInteractive UI elements composed from base components (Molecules)" > src/components/ui/README.md
echo "# App Components\n\nApp-specific block elements composed from base/ui components (Organisms)" > src/components/app/README.md
```

## Configuration Files

### package.json Scripts
```json
{
  "scripts": {
    "dev": "bun run --bun vite dev",
    "build": "bun run --bun vite build", 
    "preview": "bun run --bun vite preview",
    "check": "svelte-kit sync && svelte-check --tsconfig ./tsconfig.json",
    "check:watch": "svelte-kit sync && svelte-check --tsconfig ./tsconfig.json --watch",
    "lint": "biome lint .",
    "format": "biome format --write .",
    "test": "bun test"
  }
}
```

### svelte.config.js
```javascript
import adapter from '@sveltejs/adapter-auto'
import { vitePreprocess } from '@sveltejs/kit/vite'

/** @type {import('@sveltejs/kit').Config} */
const config = {
  kit: {
    adapter: adapter()
  },
  preprocess: vitePreprocess()
}

export default config
```

### app.html (PWA configuration)
```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="utf-8" />
    <link rel="icon" href="%sveltekit.assets%/favicon.png" />
    <meta name="viewport" content="width=device-width, initial-scale=1" />
    <meta name="theme-color" content="#000000" />
    <meta name="description" content="Discover and share secret places" />
    
    <!-- PWA manifest -->
    <link rel="manifest" href="%sveltekit.assets%/manifest.json" />
    
    <!-- iOS meta tags -->
    <meta name="apple-mobile-web-app-capable" content="yes" />
    <meta name="apple-mobile-web-app-status-bar-style" content="black" />
    
    %sveltekit.head%
  </head>
  <body data-sveltekit-preload-data="hover">
    <div style="display: contents">%sveltekit.body%</div>
  </body>
</html>
```

## First Steps

1. **Set up environment variables**:
```bash
# .env.local
VITE_GOOGLE_MAPS_API_KEY=your_api_key_here
```

2. **Create base components**: Start with Container, Text, Heading atoms

3. **Set up content collections**: Configure content-collections in svelte.config.js

4. **Create Google Maps wrapper**: Implement GooglePlacesAutocomplete component

5. **Define data entities**: Create Place, Location, Submission types

## Development Workflow

```bash
# Start development server
bun run dev

# Run linting
bun run lint

# Format code
bun run format

# Build for production
bun run build
```

## Testing

```bash
# Run tests
bun test

# Watch mode for tests
bun test --watch
```

## Deployment

Build the project and deploy the contents of the `build` directory to your hosting service.