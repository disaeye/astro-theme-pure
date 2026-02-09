# AGENTS.md - Coding Guidelines for Astro Theme Pure

## Build Commands

```bash
# Development
bun dev              # Start dev server
bun dev:check        # Dev with type checking

# Build & Deploy
bun build            # Production build (runs astro-pure check, astro check, astro build)
bun preview          # Preview production build

# Code Quality
bun lint             # ESLint with auto-fix
bun format           # Prettier format all files
bun check            # Astro type check
bun sync             # Astro sync
bun yijiansilian     # Run lint + sync + check + format together

# Utilities
bun clean            # Clean .astro, .vercel, dist
bun cache:avatars    # Cache avatar images
```

## Testing

Currently, this project does not have a test framework configured. The packages/pure/package.json has a placeholder test script that exits with error.

To add tests in the future, consider:
- **Unit tests**: Vitest for TypeScript utilities
- **E2E tests**: Playwright for page navigation and interactions
- **Component tests**: Use Astro's built-in testing patterns

## Code Style

### Formatting (Prettier)
- **No semicolons** - `semi: false`
- **Single quotes** - `singleQuote: true`, `jsxSingleQuote: true`
- **2 spaces** indentation - `tabWidth: 2`, `useTabs: false`
- **No trailing commas** - `trailingComma: 'none'`
- **Print width**: 100 characters
- **Arrow parens**: always
- **End of line**: LF

### Import Order
1. Astro modules (`astro:*`)
2. @astrojs packages
3. Third-party modules
4. astro-pure imports
5. Project aliases (`@/types`, `@/layouts`, `@/pages`, `@/components`, `@/utils`, `@/plugins`, `@/assets`, `@/site-config`)
6. Relative imports (`./`, `../`)

### TypeScript
- Use `type` imports: `import type { Foo } from '...'`
- Path aliases: `@/components/*`, `@/utils`, `@/layouts/*`, `@/types`, `@/site-config`
- Strict null checks enabled
- Astro strict tsconfig base
- Use `interface` for object shapes, `type` for unions/complex types

### Naming Conventions
- **Components**: PascalCase (e.g., `BaseLayout.astro`, `ProjectCard.astro`)
- **Files**: camelCase for TS, PascalCase for Astro components
- **Variables**: camelCase
- **Constants**: UPPER_SNAKE_CASE for true constants
- **Types/Interfaces**: PascalCase with `type` keyword
- **Functions**: camelCase, use verb prefixes (e.g., `getData`, `handleClick`)

### Astro Components
- Use frontmatter for imports and logic
- Props interface: `type Props = { ... }`
- Access props via `Astro.props`
- Use `const` for destructured props
- Slots use `slot` attribute: `<slot name="icon" />`
- Keep frontmatter logic minimal; extract to utilities when complex
- Use `Astro.params` and `Astro.props` for data flow

### Error Handling
- Use early returns for guard clauses
- Throw descriptive errors for missing data
- Use optional chaining (`?.`) and nullish coalescing (`??`)
- Handle async errors with try/catch blocks
- Validate environment variables at startup

### Styling
- Use UnoCSS/Tailwind classes
- Custom CSS in `@/assets/styles/`
- Theme colors via CSS variables (`--primary`, `--background`, etc.)
- Prose classes for typography
- Prefer utility classes over custom CSS
- Use CSS variables for theming

### Comments
- Use `{/* */}` for JSX comments in Astro
- Minimize unnecessary comments
- Self-documenting code preferred
- Document complex business logic with JSDoc
- Use TODO/FIXME comments sparingly and include issue references

## Project Structure

```
src/
  components/     # Reusable Astro components
    home/         # Homepage specific components
    projects/     # Project page components
    links/        # Links page components
    waline/       # Comment system components
  layouts/        # Page layouts
    BaseLayout.astro      # Root layout with HTML structure
    ContentLayout.astro   # Content-focused layout
    BlogPost.astro        # Blog post layout
  pages/          # Astro pages (file-based routing)
    blog/         # Blog listing and posts
    docs/         # Documentation pages
    about/        # About page
    projects/     # Projects showcase
    links/        # Friends/links page
  assets/         # Images, fonts, styles
    styles/       # Global CSS files
  utils/          # Utility functions
  types/          # TypeScript types
  plugins/        # Custom plugins (rehype, shiki)
  site.config.ts  # Site configuration
packages/pure/    # astro-pure integration (submodule)
  components/     # Pure theme components
  utils/          # Server utilities
```

## Content Collections

Blog posts are stored in `src/content/posts/` with frontmatter:
- `title`: Post title
- `description`: Post description
- `publishDate`: Publication date
- `tags`: Array of tags
- `draft`: Boolean for draft status

## Key Technologies

- **Framework**: Astro 5.x
- **Language**: TypeScript (ES modules)
- **Styling**: UnoCSS (Tailwind-compatible)
- **Content**: MDX support with custom remark/rehype plugins
- **Search**: Pagefind integration
- **Comments**: Waline
- **Math**: KaTeX for rendering
- **Code Highlighting**: Shiki with custom transformers
- **Linting**: ESLint with astro plugin
- **Formatting**: Prettier with astro and import sorting
- **Package Manager**: Bun

## Development Workflow

1. Run `bun yijiansilian` before committing to ensure code quality
2. Use `bun check` to verify TypeScript types
3. Test production build with `bun build && bun preview`
4. Follow conventional commit messages when possible
5. Keep components small and focused on single responsibility
