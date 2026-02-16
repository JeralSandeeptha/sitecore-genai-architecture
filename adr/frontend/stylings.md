# ADR: Use Tailwind CSS for Styling

## Status
Accepted

## Context
Our frontend applications require a consistent, maintainable, and efficient approach to styling. Key considerations for the styling solution include:

- `Developer Productivity`: Frontend developers should be able to rapidly create and iterate on UI components without writing repetitive CSS.
- `Consistency`: The design system should be consistent across components and pages, reducing visual inconsistencies.
- `Performance`: The CSS solution must minimize unused styles in production to reduce bundle size and improve page load times.
- `Flexibility`: Styling should be adaptable for custom themes, responsive design, and component-specific overrides.
- `Integration`: The solution should integrate seamlessly with our React/Next.js stack and existing build tooling.

Several styling approaches were evaluated, including traditional CSS, CSS Modules, Sass/SCSS, Styled Components, and Tailwind CSS.

## Decision
We decided to adopt Tailwind CSS as the primary styling framework for our frontend applications. Bydefault V0 supports tailwind also. Then we don't need to deal with stylings as well.

Implementation approach:

- Use Tailwind CSS utility classes directly in JSX for fast, composable UI styling.
- Configure a central Tailwind configuration file (tailwind.config.js) to define color palettes, spacing, typography, breakpoints, and custom utilities.
- Leverage purge/content paths in production builds to remove unused CSS, minimizing bundle size.
- Integrate with PostCSS and the existing build pipeline for React applications.
- Use Tailwind’s responsive, state, and variant utilities to handle hover, focus, dark mode, and responsive layouts without writing custom CSS.

Optionally extend Tailwind with plugins for form styles, typography, and animations where needed.

## Consequences

Positive:
- Rapid development: Developers can style components quickly without writing repetitive CSS.
- Consistent design system: Shared utility classes ensure visual consistency across the application.
- Small CSS footprint: Purge mechanism reduces production CSS size, improving performance.
- Highly responsive and customizable: Tailwind utilities make it easy to implement responsive layouts and custom themes.
- Seamless React integration: No additional runtime overhead or dependency bloat compared to CSS-in-JS solutions.

Negative:
- Steeper learning curve: Developers must become familiar with Tailwind utility classes.
- Verbose JSX: Class names can become long and hard to read for complex components.
- Migration cost: Existing CSS/SCSS styles may need to be refactored to Tailwind over time.
- Limited dynamic theming: Some runtime dynamic styling scenarios require additional configuration or workarounds.

## Date
2026-01-25

## Authors / Reviewers
Frontend Team Lead
UI/UX Designer
Software Architect