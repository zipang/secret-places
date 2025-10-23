# Agent Coding Guidelines

This document summarizes the essential coding guidelines and principles for the **silent-places** project, as defined in the project constitution. The full set of rules are inside the [constitution](.specify/memory/constitution.md) file.

## 1. Core Philosophy

- **Mobile-First PWA:** Design and build for a mobile experience first.
- **Performance and adhesion to best practices:** Achieve a perfect 100 score across all Lighthouse categories (Performance, Accessibility, Best Practices, SEO).
- **KISS (Keep It Stupid Simple):** Prioritize simplicity and avoid over-engineering. This is a solo project, and the workflow should be fast and lean _but without compromise on maintanability_ : separation of concerns is key to allow refactoring every area.

## 2. Technical Stack

The following technologies are mandated. Do not introduce or use alternatives.

- **Language:** TypeScript for all frontend and backend code.
- **Runtime/Builder/Tester:** `bun` is the exclusive tool for running, building, and testing the application. All `package.json` scripts MUST use `bun`.
- **Linter & Formatter:** BiomeJS is the sole tool for linting and formatting.
- **Content Management:** `content-collections` is used to load all application content from local Markdown files.
- **Schema Validation:** `arktype` is the standard library for all data validation.

## 3. Architecture & Code Style

### Directory Structure

- The project uses a unified `src` directory for all source code (isomorphic approach).
- Key directories (`components/base`, `components/ui`, `entities`, `routes`, etc.) SHOULD contain a `README.md` file explaining their purpose and usage.

### Atomic Design Principles

A strict, layered component hierarchy based on the Atomic Design principles from Brad Frost is enforced to ensure encapsulation and maintainability.

1.  **`src/components/base` (Atoms):**
    - Contains foundational layout and text components (e.g., `Container`, `HStack`, `VStack`, `Grid`, `Text`, `Heading`, ...).
    - This layer is allowed to directly use the underlying UI library and style engine (e.g., Chakra UI, Material UI, Tailwind, ..).
    - Responsible for applying the design system choices (colors, typography, sizes, ..).

2.  **`src/components/ui` (Molecules):**
    - Contains interactive UI elements (e.g., `Button`, `Card`, `Select`).
    - MUST be composed from components in the `base` layer.
    - This layer is allowed to directly use the underlying UI library (e.g., Chakra UI, Material UI, Tailwind, ..).

3.  **`src/components/app` (Organisms):**
    - Contains app specific block elements (e.g., `HeroSection`, `Testimony`, `MainHeader`, ..).
    - Is composed from components in the `base` and `ui` layer.
    - MUST **NEVER** directly use the underlying UI library components or style primitives (e.g., Chakra UI, Material UI, Tailwind, ..).

4.  **`src/components/layout` (Templates):**
    - Load data and render it in a specific page template using app blocks (e.g., `HeroSection`, `Testimony`, `MainHeader`, ..).
    - Is composed from components from the `app` layer.
    - MUST **NEVER** directly use the underlying UI library components or style primitives (e.g., Chakra UI, Material UI, Tailwind, ..).

5.  **`src/components/routes/pages` (Pages):**
    - MUST be built by composing components from the `base` and `ui` layers.
    - MUST **NEVER** directly use the underlying UI library components or style primitives (e.g., Chakra UI, Material UI, Tailwind, ..).

### Code Readability & Documentation

- **Usage of JSDoc:**
    - Every function or class method MUST have a JSDoc block explaining its purpose and parameters.
    - All component props MUST be defined in an interface, with each property having a clear JSDoc description.
- **Naming:** All variables and function names MUST be clear and self-explanatory.

## 4. Browser Support & Web Standards

- **Evergreen Browsers Only:** The project exclusively targets the latest versions of modern browsers (Chrome, Firefox, Safari, Edge).
- **No Polyfills:** Code MUST use modern, standardized web APIs (e.g., `fetch` instead of `XMLHttpRequest`) directly. Third-party libraries that rely on polyfills or deprecated features are forbidden.

## 5. Testing

- **Scope:** To maintain simplicity, unit tests are required **only for core business logic and utility functions** (e.g., code in a `src/lib` or `src/utils` directory).
- **Exclusions:** UI components (`base`, `ui`, pages, etc.) and entities do not require dedicated tests.
- **Tooling:** Tests MUST use the `bun test` API.
- **Location:** Test files MUST be co-located with the source file they are testing and use the `*.spec.ts` extension.

## 6. Content Management

- All application text content is managed as code.
- **Source:** Content is stored in local Markdown files with front-matter, located in `src/content`.
- **i18n:** Internationalization is handled via language-specific subfolders (e.g., `src/content/en`, `src/content/fr`).
