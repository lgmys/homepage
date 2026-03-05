# Astro Blog - Agent Guidelines

## Project Overview
This is an Astro 5.x blog site using content collections, MDX support, and Astro features.

## Commands
- `npm install` - Install dependencies
- `npm run dev` - Start local dev server at `localhost:4321`
- `npm run build` - Build production site to `./dist/`
- `npm run preview` - Preview production build locally
- `npm run astro` - Run Astro CLI commands
- `npm run astro -- check` - Type-check Astro project

## Testing
This is a static site with no automated tests. Use `npm run build` to verify the build works.

## Code Style Guidelines

### Imports and Modules
- Use ESM imports (`import ... from ...`)
- Import Astro components relative to `src/`, not project root
- Group imports: Astro imports first, then components, then utilities, then consts
- Use named exports for shared data in `consts.ts`

### File Structure
- Pages: `src/pages/*.astro` - URL mapped by filename
- Components: `src/components/*.astro` - Reusable components
- Layouts: `src/layouts/*.astro` - Page templates
- Content: `src/content/blog/*.md[mdx]` - Blog posts with content collections
- Globals: `src/consts.ts` - Site metadata

### Astro Templates
- Use `<html>`, `<head>`, `<body>` structure in pages and layouts
- Put imports in YAML frontmatter (3 dashes)
- Destructure `Astro.props` to get component props
- Spread props with `{...props}` syntax
- Use `{expression}` for inline content

### TypeScript
- Use strict typing with `strict: true` and `strictNullChecks: true`
- Use `type Props` alias for component prop types
- Type collection entries: `CollectionEntry<'blog'>` for blog posts
- Use TypeScript for `.astro` files with import types from `astro:content`

### Naming Conventions
- Components: `PascalCase.astro` (Header.astro, BlogPost.astro)
- Pages: kebab-case or dynamic params in brackets `[slug].astro`
- Variables: `camelCase`, consts: `UPPER_SNAKE_CASE`
- Props: Destructure with clear names in frontmatter

### Styling
- Use inline `<style>` blocks in components
- Use CSS custom properties: `rgb(var(--gray))`, `var(--box-shadow)`
- Scoped styles via CSS modules preferred for complex components
- Responsive: Use `@media (max-width: 720px)` breakpoints
- Flexbox for layout, avoid utility classes

### Content Collections
- Define schema in `src/content.config.ts` with zod validators
- Use `astro:content` exports for getCollection, render, type exports
- Frontmatter: `title`, `description`, `pubDate` (required), optional fields
- Image frontmatter auto-validated via `image()` helper

### Best Practices
- Always include `lang="en"` on `<html>` tags
- Add `astro:island` or `astro:component` for interactive elements if needed
- Use semantic HTML: `<header>`, `<nav>`, `<main>`, `<article>`, `<footer>`
- Include alt text for images, mark decorative images as empty alt
- Use `target="_blank"` for external links
- Mark SEO attributes with `rel="canonical"` and OpenGraph data
