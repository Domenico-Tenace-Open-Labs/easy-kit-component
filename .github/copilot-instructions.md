# Easy Kit Component - Copilot Instructions

Easy Kit Component is a lightweight, reusable Vue 3 component library designed for rapid UI development. This document provides comprehensive information about the project's architecture, technologies, design patterns, and development guidelines.

---

## Project Overview

**Easy Kit Component** is a modern, TypeScript-based component library built with Vue 3 and distributed as an npm package. It provides a set of essential, pre-built UI components that follow Vue 3 composition API patterns and best practices.

**Project Information:**
- **Name:** easy-kit-component
- **Description:** Simple component kit for Vue 3
- **Version:** 0.2.0
- **License:** MIT
- **Author:** Domenico Tenace
- **Repository:** https://github.com/Domenico-Tenace-Open-Labs/easy-kit-component
- **Package Type:** ESM Module (ES2015+)

**Key Characteristics:**
- Lightweight and tree-shakeable component library
- Zero runtime dependencies (apart from Vue 3)
- Full TypeScript support with strict type checking
- Comprehensive test coverage with Vitest
- Integrated documentation with VitePress
- Dual build outputs (ESM and UMD)

---

## Technology Stack

### Core Framework & Libraries
- **Vue 3** (^3.4.31) - Progressive JavaScript framework for building user interfaces
- **TypeScript** (^5.5.3) - Strongly typed programming language that builds on JavaScript
- **Vite** (^5.1.5) - Lightning-fast frontend build tool and dev server

### Build & Distribution
- **vite-plugin-dts** (^3.9.1) - Generates TypeScript declaration files (.d.ts) during build
- **@vitejs/plugin-vue** (^5.0.5) - Official Vite plugin for Vue 3 Single File Components
- **vue-tsc** (^2.0.26) - TypeScript compiler for Vue 3 components

### Testing Framework
- **Vitest** (^1.6.0) - Unit testing framework built on top of Vite
- **@vue/test-utils** (^2.4.6) - Official testing library for Vue 3 components
- **happy-dom** (^14.12.3) - Lightweight DOM implementation for testing environment

### Documentation
- **VitePress** (^1.2.3) - Static site generator built on Vite for documentation
- **@orama/orama** (^2.0.23) - Full-text search engine for documentation
- **@orama/plugin-vitepress** (^2.0.23) - VitePress integration for Orama search

---

## Project Structure

### Root Level Files

```
easy-kit-component/
├── package.json                    # Project metadata and dependencies
├── tsconfig.json                   # TypeScript compiler configuration
├── tsconfig.node.json              # TypeScript config for Node.js tools
├── vite.config.ts                  # Vite build and dev configuration
├── README.md                        # Project documentation
├── LICENSE                          # MIT License file
└── .github/
    └── copilot-instructions.md      # This file
```

### Source Directory (`src/`)

The `src/` directory contains all component source code organized by functionality.

#### `src/index.ts` - Main Entry Point
Central export file that re-exports all public components:
```typescript
export {
  EButton,
  ECheckbox,
  EColorPicker,
  EDatePicker,
  EText,
  ETextArea,
  ERadio,
  ESelect,
};
```

This file serves as the library's public API. All components are tree-shakeable through modern bundler support.

#### `src/components/` - Component Directory

Components are organized by functionality and type:

##### Button Component (`components/button/`)
- **`EButton.vue`** - Basic button component
  - Props:
    - `type?: "button" | "submit" | "reset"` - Button type (default: "button")
    - `disabled?: boolean` - Disable button
    - `formId?: string` - Associated form ID
    - `autoFocus?: boolean` - Auto-focus on mount
  - Slots: Default slot for button content
  - Features: Full form integration, multiple button types, proper accessibility

##### Input Components (`components/input/`)

###### Text Input (`input/text/`)
- **`EText.vue`** - Text input component
  - Props:
    - `placeHolder?: string` - Placeholder text
    - `maxLength?: number | null` - Maximum character length
    - `minLength?: number | null` - Minimum character length
    - `readOnly?: boolean` - Read-only mode
    - `disabled?: boolean` - Disable input
  - Emits: `update:modelValue` - v-model support
  - Features: Two-way binding, length validation, placeholder support

###### Checkbox Input (`input/checkbox/`)
- **`ECheckbox.vue`** - Checkbox input component
  - Props:
    - `disabled?: boolean` - Disable checkbox
  - Emits: `update:modelValue` - v-model support (boolean value)
  - Features: Two-way binding for boolean state, proper accessibility

###### Color Picker (`input/colorpicker/`)
- **`EColorPicker.vue`** - HTML5 color picker component
  - Props: Input-related props for color selection
  - Emits: `update:modelValue` - v-model support (hex color string)
  - Features: Native HTML5 color picker, cross-browser compatibility

###### Date Picker (`input/datepicker/`)
- **`EDatePicker.vue`** - HTML5 date picker component
  - Props: Date input-related props
  - Emits: `update:modelValue` - v-model support (date string)
  - Features: Native HTML5 date picker, proper date formatting

###### Text Area (`input/textarea/`)
- **`ETextArea.vue`** - Multi-line text input component
  - Props:
    - `placeHolder?: string` - Placeholder text
    - `maxLength?: number | null` - Maximum character length
    - `minLength?: number | null` - Minimum character length
    - `readOnly?: boolean` - Read-only mode
    - `disabled?: boolean` - Disable textarea
  - Emits: `update:modelValue` - v-model support
  - Features: Resizable, multi-line text input, length validation

##### Radio Component (`components/radio/`)
- **`ERadio.vue`** - Radio button component
  - Props:
    - `value: any` - Radio button value
    - `disabled?: boolean` - Disable radio button
  - Emits: `update:modelValue` - v-model support
  - Features: Grouped radio buttons, proper form integration, accessibility

##### Select Component (`components/select/`)
- **`ESelect.vue`** - Dropdown select component
  - Props:
    - `placeHolder?: string` - Placeholder option text
    - `multiple?: boolean` - Allow multiple selections
    - `required?: boolean` - Required field
    - `disabled?: boolean` - Disable select
    - `value?: any` - Initial/current value
  - Emits: `update:modelValue` - v-model support
  - Slots: Default slot for `<option>` elements
  - Features: Single/multiple selection, proper form support, reactive updates

#### `src/composables/` - Composition API Utilities

- **`useUpdateModelValue.ts`** - Utility composables for v-model handling
  - **`useUpdateModelText(event, emit)`** - Extract text value from input event and emit update
    - Usage: For text and textarea inputs
    - Extracts `HTMLInputElement.value` from event
  - **`useUpdateModelCheckbox(event, emit)`** - Extract checked state and emit update
    - Usage: For checkbox inputs
    - Extracts `HTMLInputElement.checked` from event
  - **`useUpdateModelRadiobox(value, emit)`** - Emit radio button value update
    - Usage: For radio button components
    - Direct value emission without event extraction

### Testing Directory

Tests are co-located with components using `.test.ts` extension:
```
src/components/
├── button/
│   ├── EButton.vue
│   └── EButton.test.ts
├── input/
│   ├── text/
│   │   ├── EText.vue
│   │   └── EText.test.ts
│   ├── checkbox/
│   │   ├── ECheckbox.vue
│   │   └── ECheckbox.test.ts
│   └── ... (other input types)
└── ...
```

### Documentation Directory (`docs/`)

- **`docs/index.md`** - Documentation homepage
- **`docs/guide/`** - User guides and tutorials
  - `getting-started/quick-start.md` - Quick start guide
  - `components/` - Individual component documentation
    - `ebutton.md` - EButton documentation
    - `echeckbox.md` - ECheckbox documentation
    - `ecolorpicker.md` - EColorPicker documentation
    - `edatepicker.md` - EDatePicker documentation
    - `eradio.md` - ERadio documentation
    - `eselect.md` - ESelect documentation
    - `etext.md` - EText documentation
    - `etextarea.md` - ETextArea documentation
- **`docs/public/`** - Static assets for documentation
- **`docs/utils/`** - Documentation utility components
  - `ExampleLayout.vue` - Layout wrapper for component examples

---

## Architecture & Design Patterns

### Component-Based Architecture
The library follows a **modular component-based architecture** where:
- Each UI component is self-contained and reusable
- Components are organized by functional category
- Clear separation of concerns between presentation and logic
- Components follow the Single Responsibility Principle
- No component dependencies on other components (except via slots)

### Composition API Pattern
All components use Vue 3's **Composition API** with `<script setup>` syntax:

**Advantages:**
- More readable and maintainable code
- Better TypeScript inference and support
- Improved code organization and reusability
- Smaller bundle sizes compared to Options API
- Easier code sharing through composables

**Pattern Structure:**
```vue
<script setup lang="ts">
// Import composables and types
interface ComponentProps {
  prop1?: string;
  prop2?: boolean;
}

// Define props with TypeScript interface
const props = defineProps<ComponentProps>();
const emit = defineEmits();

// Component logic here
</script>

<template>
  <!-- Template bindings -->
</template>

<script lang="ts">
export default {
  name: "ComponentName",
};
</script>
```

### v-model Integration Pattern
All input components implement Vue 3's **v-model binding** pattern:

**Implementation Details:**
- Props handle input properties and states
- Emits use `update:modelValue` event for two-way binding
- Compatible with parent component data binding
- Supports reactive updates through Vue's reactivity system

**Example:**
```vue
<!-- Parent component usage -->
<EText v-model="username" placeholder="Enter username" />

<!-- Component handles: -->
<!-- - Receives value via props (implicitly bound) -->
<!-- - Emits update:modelValue on input -->
```

### Utility Composable Pattern
Reusable logic is extracted into **utility composables** in `src/composables/`:

**Benefits:**
- Reduces code duplication across similar components
- Easier to test and maintain utility functions
- Clear separation of event handling logic
- Simple, focused functions with single responsibility

**Pattern:**
```typescript
export function useUpdateModelText(event: Event, emit: any) {
  const value = (event?.target as HTMLInputElement).value;
  emit("update:modelValue", value);
}
```

### TypeScript Interface Pattern
All components use **TypeScript interfaces** for props:

**Advantages:**
- Type safety and compile-time checking
- Better IDE autocomplete and documentation
- Easier refactoring with type support
- Clear prop documentation through types
- Strict null checking compatibility

**Pattern:**
```typescript
interface ButtonProps {
  type?: "button" | "submit" | "reset";
  disabled?: boolean;
  formId?: string;
  autoFocus?: boolean;
}

const props = defineProps<ButtonProps>();
```

### Slot-Based Composition
Components use **named and default slots** for content composition:

**Benefits:**
- Flexible content insertion
- Works naturally with Vue's slot system
- No prop drilling needed for content
- Clean, declarative syntax

**Example:**
```vue
<!-- Component -->
<template>
  <button><slot></slot></button>
</template>

<!-- Usage -->
<EButton>Click me</EButton>
```

---

## Configuration Details

### Vite Configuration (`vite.config.ts`)

**Build Configuration:**
```typescript
build: {
  lib: {
    entry: "./src/index.ts",        // Library entry point
    name: "EasyKit",                // Global variable name
    fileName: (format) => `index.${format}.js`  // Output file naming
  }
}
```

**Key Features:**
- Library mode build configuration
- Dual output format support (ESM and UMD)
- Vue plugin integration
- TypeScript declaration file generation
- Rollup options for external Vue dependency

**Plugin Configuration:**
- **Vue Plugin:** Enables Single File Component support
- **DTS Plugin:** Generates `.d.ts` files for TypeScript support

**Test Configuration:**
```typescript
test: {
  globals: true,           // Global test API (describe, it, expect)
  environment: "happy-dom" // Lightweight DOM environment
}
```

### TypeScript Configuration (`tsconfig.json`)

**Compiler Options:**
- **Target:** ES2015 - Modern JavaScript compatibility
- **Module:** ES2015 - ECMAScript module output
- **Module Resolution:** Node - Node.js module resolution
- **Strict Mode:** Enabled - Full type checking
- **JSX:** Preserve - Keep JSX as-is for Vue
- **Library Support:** ESNext and DOM APIs

**Key Settings:**
- `strict: true` - Full type safety
- `noEmit: true` - Only for type checking (Vite handles emission)
- `isolatedModules: true` - Each file can be transpiled independently
- `skipLibCheck: true` - Skip type checking for dependencies

### Package.json Configuration

**Module Exports:**
```json
{
  "main": "./dist/index.umd.js",        // UMD format (CommonJS)
  "module": "./dist/index.es.js",       // ESM format (modern)
  "types": "./dist/index.d.ts"          // TypeScript declarations
}
```

**Build Scripts:**
- `npm run build` - Compile TypeScript and build library
- `npm run test` - Run unit tests with Vitest
- `npm run docs:dev` - Start documentation dev server
- `npm run docs:build` - Build documentation for production
- `npm run docs:preview` - Preview built documentation

---

## Development Workflow

### Local Development Setup

**Installation:**
```bash
npm install
```

**Development Server:**
```bash
npm run dev  # Start Vite dev server with HMR
```

**Building Library:**
```bash
npm run build  # Compile TypeScript, build ESM and UMD outputs
```

### Testing Workflow

**Running Tests:**
```bash
npm run test  # Run all tests with Vitest
```

**Test Structure:**
- Test files use `.test.ts` extension
- Co-located with component files for easy navigation
- Happy-dom environment for lightweight testing
- Vue Test Utils for component testing utilities

**Testing Best Practices:**
- Test component props and their effects
- Test event emission (update:modelValue)
- Test slot rendering
- Test disabled states and form integration
- Test accessibility features

### Documentation Development

**Local Documentation:**
```bash
npm run docs:dev  # Start VitePress dev server
```

**Building Documentation:**
```bash
npm run docs:build  # Generate static documentation
npm run docs:preview  # Preview built documentation
```

**Documentation Structure:**
- VitePress markdown files in `docs/`
- Component examples in `docs/utils/ExampleLayout.vue`
- Search functionality via Orama integration
- Structured guides for getting started and component usage

---

## Styling & Theme System

### Component Styling Approach
- **No CSS Scoping:** Components do not use scoped styles
- **Semantic HTML:** Clean, accessible HTML structure
- **Framework Agnostic:** Styling can be applied by consuming applications
- **Minimal Default Styles:** Components rely on application-level styling

### Component Base Elements
- **Button:** `<button>` element with type and form support
- **Inputs:** Native HTML5 `<input>` elements (text, checkbox, radio, color, date)
- **TextArea:** `<textarea>` element for multi-line text
- **Select:** Native `<select>` element with option slots

### Styling in Consumer Applications
Applications consuming Easy Kit Component should implement styling through:
- Tailwind CSS utilities
- CSS-in-JS solutions
- Traditional CSS files
- CSS custom properties (variables)
- Any CSS framework compatible with Vue 3

---

## Key Features Implementation

### QR Code Generation
- Uses **qrcode.vue** library wrapping `qrcode.js`
- Supports multiple render types: canvas and image
- Customizable error correction levels (L, M, Q, H)
- Color customization for both foreground and background

### Download Functionality
- Converts canvas to PNG data URL
- Creates temporary download link
- Filename uses timestamp for uniqueness
- Validates that QR code value is not empty

### Form Validation
- Client-side validation in `downloadQRCode()` method
- Alert if user tries to download empty QR code
- Real-time preview updates as user modifies settings

### PWA Features
- Service worker for offline capability
- Auto-updates in background
- Installable on home screen
- Works offline with previously cached data

---

## Code Style & Best Practices

### Naming Conventions

**Components:**
- PascalCase with 'E' prefix (e.g., `EButton`, `EText`, `ECheckbox`)
- Represents "Easy Kit" brand
- Consistent naming across library
- Export names match component names

**Files:**
- Component files: PascalCase (e.g., `EButton.vue`, `EText.vue`)
- Test files: Component name + `.test.ts` (e.g., `EButton.test.ts`)
- Composable files: lowercase with `.ts` extension
- Utility files: lowercase descriptive names

**TypeScript Interfaces:**
- PascalCase for interfaces
- Component prop interface: `ComponentNameProps`
- Descriptive property names in camelCase
- Optional properties marked with `?`

**Variables & Functions:**
- camelCase for local variables and functions
- `const props = defineProps<InterfaceName>()`
- `const emit = defineEmits()`

### TypeScript Usage

**Type Safety:**
- All props defined with TypeScript interfaces
- Strict mode enabled in `tsconfig.json`
- Type inference for event handlers
- Full typing of composable functions

**Interface Examples:**
```typescript
// Props interface
interface Text {
  placeHolder?: string;
  maxLength?: number | null;
  minLength?: number | null;
  readOnly?: boolean;
  disabled?: boolean;
}

// Type definitions
type ButtonType = "button" | "submit" | "reset";
type LengthType = number | null;
```

### Component Structure

**Standard Component Layout:**
1. **Script Setup Block:**
   - Import statements
   - Type and interface definitions
   - Props definition with `defineProps<Interface>()`
   - Emit definition with `defineEmits()`
   - Component logic and event handlers

2. **Template Block:**
   - Semantic HTML elements
   - Proper ARIA attributes for accessibility
   - Conditional rendering with `v-if`, `v-show`
   - Event binding with proper handlers
   - Slot definitions

3. **Script Block:**
   - Component name export for debugging

### Import/Export Patterns

**Main Library Export:**
```typescript
// src/index.ts - All components exported from main entry
export { EButton, ECheckbox, EColorPicker, ... };
```

**Component Imports in Applications:**
```typescript
// Single component
import { EButton } from 'easy-kit-component';

// Tree-shakeable - only imported components are bundled
```

---

## Build & Distribution

### Build Outputs

**Generated Files:**
- `dist/index.es.js` - ES Module (modern, tree-shakeable)
- `dist/index.umd.js` - UMD Module (CommonJS compatible)
- `dist/index.d.ts` - TypeScript declarations

**Distribution Configuration:**
- Vue is marked as external dependency
- Tree-shakeable due to ES module format
- Type definitions included with package
- Both CommonJS and ES Module support

### Package Distribution

**npm Registry:**
- Published as `easy-kit-component`
- Semantic versioning (currently 0.2.0)
- MIT License for open source usage
- Includes source maps for debugging

**Installation:**
```bash
npm install easy-kit-component
# or
pnpm add easy-kit-component
# or
yarn add easy-kit-component
```

### Browser Support & Compatibility

**Target Browsers**
- Modern browsers with ES2015+ support
- Vue 3 supported browsers
- No IE11 support required
- Progressive enhancement friendly

**Compatibility Notes**
- Native HTML5 features (color picker, date picker)
- Modern CSS support assumed
- ES Module syntax required
- TypeScript optional (but recommended)

### Performance Considerations

**Bundle Size**
- Lightweight components (minimal overhead)
- Tree-shakeable modules (only used components included)
- No unnecessary dependencies
- Vue 3 as peer dependency (not bundled)

**Runtime Performance**
- Reactive component updates via Vue 3 reactivity
- Efficient event handling
- Minimal re-renders through composition API
- Happy-dom for testing (not production)

**Build Optimization**
- Vite's fast compilation and bundling
- TypeScript compilation step
- Declaration files for better IDE support
- UMD and ESM outputs for different use cases

---

## Component Development Guidelines

### Adding New Components

**Step 1: Create Component Directory**
```
src/components/category/ComponentName/
├── EComponentName.vue
├── EComponentName.test.ts
```

**Step 2: Implement Component**
- Follow Composition API pattern with `<script setup>`
- Define props with TypeScript interface
- Implement event handlers and emit updates
- Use semantic HTML elements
- Add accessibility attributes (ARIA)

**Step 3: Create Unit Tests**
- Test component mounting
- Test props and their effects
- Test event emissions
- Test slot content rendering
- Test edge cases and error states

**Step 4: Add to Main Export**
```typescript
// src/index.ts
import EComponentName from "./components/category/EComponentName.vue";
export { EComponentName, ... };
```

**Step 5: Create Documentation**
- Create markdown file in `docs/guide/components/`
- Include component description
- Show prop interface
- Provide usage examples
- Document emitted events

### Modifying Existing Components

**Safe Modifications:**
- Add new optional props (don't change prop names)
- Add new emit events (don't remove existing ones)
- Enhance component functionality (backwards compatible)
- Improve documentation

**Breaking Changes to Avoid:**
- Renaming component props
- Changing prop types
- Removing emit events
- Altering component behavior

### Event Handling Pattern

**Standard Event Emission:**
```typescript
// Component emits
const emit = defineEmits<{
  "update:modelValue": [value: any]
}>();

// Event handler
function handleInput(event: Event) {
  const value = (event.target as HTMLInputElement).value;
  emit("update:modelValue", value);
}
```

**Using Composables for Common Patterns:**
```typescript
// In component
@input="useUpdateModelText($event, emit)"
```

### Testing Standards

**Test Framework: Vitest**

**Test File Structure:**
```typescript
import { describe, it, expect, beforeEach } from "vitest";
import { mount } from "@vue/test-utils";
import EButton from "./EButton.vue";

describe("EButton", () => {
  it("should render", () => {
    const wrapper = mount(EButton);
    expect(wrapper.exists()).toBe(true);
  });

  it("should emit events", () => {
    const wrapper = mount(EButton);
    wrapper.find("button").trigger("click");
    expect(wrapper.emitted()).toBeDefined();
  });
});
```

**Testing Best Practices:**
- Test component rendering
- Test prop validation and effects
- Test event emissions with proper payloads
- Test slot content projection
- Test disabled and readonly states
- Test accessibility attributes
- Test form integration (for input components)
- Test edge cases (null values, empty strings, etc.)

---

## Dependency Management

### Direct Dependencies
- `vue` (^3.4.31) - Core UI framework
- `@orama/orama` - Search functionality
- `@orama/plugin-vitepress` - Documentation search
- `happy-dom` - Testing DOM environment
- `vite-plugin-dts` - TypeScript declarations generation

### Development Dependencies
- `@vitejs/plugin-vue` - Vue 3 support in Vite
- `@vue/test-utils` - Vue component testing
- `typescript` - TypeScript compiler
- `vite` - Build tool
- `vitepress` - Documentation generator
- `vitest` - Unit testing framework
- `vue-tsc` - Vue TypeScript compiler

### Peer Dependency
- `vue` (^3.0.0) - Required in consuming applications

## Additional Notes

### Design Philosophy
- **Simplicity First:** Minimal, focused components with no bloat
- **Type Safety:** Full TypeScript support throughout
- **Composability:** Flexible through slots and props
- **Performance:** Lightweight with tree-shaking support
- **Developer Experience:** Clear APIs, good documentation
- **Standards Compliance:** Follow Vue 3 best practices

### Future Considerations
- Theming system for component customization
- Additional form components (range slider, file input, etc.)
- Accessibility enhancements (ARIA attributes)
- Animation support for interactive components
- Integration with form validation libraries

### Project Maintenance
- Regular dependency updates
- Security patches when needed
- Community feedback incorporation
- Backwards compatibility maintenance
- Documentation updates with new features

---

## Quick Reference: Component List

| Component | Location | Purpose |
|-----------|----------|---------|
| **EButton** | `components/button/` | Button element with type support |
| **EText** | `components/input/text/` | Text input field |
| **ETextArea** | `components/input/textarea/` | Multi-line text input |
| **ECheckbox** | `components/input/checkbox/` | Checkbox input with v-model |
| **ERadio** | `components/radio/` | Radio button input |
| **ESelect** | `components/select/` | Dropdown select element |
| **EColorPicker** | `components/input/colorpicker/` | HTML5 color picker |
| **EDatePicker** | `components/input/datepicker/` | HTML5 date picker |

---

## Resources & Links

- **Repository:** https://github.com/DomeT99/easy-kit
- **Author:** Domenico Tenace (@domenicotenace)
- **Vue 3 Documentation:** https://vuejs.org
- **TypeScript Documentation:** https://www.typescriptlang.org
- **Vite Documentation:** https://vitejs.dev
- **VitePress Documentation:** https://vitepress.dev