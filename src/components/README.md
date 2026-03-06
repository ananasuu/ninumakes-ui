# Component Structure

Components are organized into three logical categories to improve maintainability and understandability.

## 📁 Directory Structure

```
src/components/
├── layout/           # Layout containers (global structure)
│   ├── Header.astro        # Global navigation
│   ├── Section.astro       # General section container
│   └── Spotlight.astro     # Hero/Spotlight section container
....
```

## 🎯 Component Categories

### `layout/` - Layout Containers
Components that define the **global structure**.

- **Header.astro**: Global navigation with language switch
- **Section.astro**: Container for content sections (with ID, Title, Description slot)
- **Spotlight.astro**: Hero section with profile image and card slots

**Usage**: In pages as a wrapper around content.

### `features/` - Reusable UI Components
Small, **self-contained** UI components that can be used independently.

- **LinkCard.astro**: Card for externally linked resources

**Usage**: Imported by other components (e.g., Ressources.astro).

### `sections/` - Data-Rendering Components
Large components that **work with JSON data** and render complete lists.

- **CosCard.astro**: Renders all cosplay entries from JSON
- **Certificates.astro**: Renders certificates from JSON
- **ListCard.astro**: Generic list component (Skills, Interests)
- **Projects.astro**: Renders projects from JSON
- **Resume.astro**: Renders resume entries from JSON
- **Ressources.astro**: Renders resources by categories from JSON

**Features**:
- Load JSON data via `import()`
- Use i18n for localization
- Render complete lists/pages

**Usage**: In pages as a single component.

## 🔄 Import Conventions

```astro
// ✅ Pages import components with full path
import Header from "@/components/layout/Header.astro";
import CosCard from "@/components/sections/CosCard.astro";
import Section from "@/components/layout/Section.astro";

// ✅ Components use @ alias for data
import data from "@/data/work/projects.json";

// ✅ Relative imports within a directory
import LinkCard from "../features/LinkCard.astro";
```

## 📝 Best Practices

1. **Categorize new components**: If data-based → `sections/`, if reusable UI → `features/`, if structural → `layout/`
2. **Keep imports consistent**: Use `@/` alias for data imports
3. **Localization**: All components should use `getLocaleFromUrl()` and `getLocalizedContent()`
4. **Props types**: Define props types in `src/types/index.ts`

## 🎨 Component Props Template

```astro
---
import type { SectionProps } from "@/types";

interface Props {
  id: string;
  title: string;
  class?: string;
}

const { id, title, class: className } = Astro.props as Props;
---
```

