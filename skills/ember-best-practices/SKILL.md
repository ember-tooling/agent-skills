---
name: ember-best-practices
description: Ember.js performance optimization and accessibility guidelines. This skill should be used when writing, reviewing, or refactoring Ember.js code to ensure optimal performance patterns and accessibility. Triggers on tasks involving Ember components, routes, data fetching, bundle optimization, or accessibility improvements.
license: MIT
metadata:
  author: Ember.js Community
  version: '1.0.0'
---

# Ember.js Best Practices

Comprehensive performance optimization and accessibility guide for Ember.js applications. Its rules span 10 categories, prioritized by impact to guide automated refactoring and code generation.

## When to Apply

Reference these guidelines when:

- Writing new Ember components or routes
- Implementing data fetching with WarpDrive
- Reviewing code for performance issues
- Refactoring existing Ember.js code
- Optimizing bundle size or load times
- Implementing accessibility features

## Rule Categories by Priority

| Priority | Category                        | Impact      | Prefix                   |
| -------- | ------------------------------- | ----------- | ------------------------ |
| 1        | Route Loading and Data Fetching | CRITICAL    | `route-`                 |
| 2        | Build and Bundle Optimization   | CRITICAL    | `bundle-`                |
| 3        | Component and Reactivity        | HIGH        | `component-`, `exports-` |
| 4        | Accessibility Best Practices    | HIGH        | `a11y-`                  |
| 5        | Service and State Management    | MEDIUM-HIGH | `service-`               |
| 6        | Template Optimization           | MEDIUM      | `template-`, `helper-`   |
| 7        | Performance Optimization        | MEDIUM      | `performance-`           |
| 8        | Testing Best Practices          | MEDIUM      | `testing-`               |
| 9        | Tooling and Configuration       | MEDIUM      | `vscode-`                |
| 10       | Advanced Patterns               | MEDIUM-HIGH | `advanced-`              |

## Quick Reference

### 1. Route Loading and Data Fetching (CRITICAL)

- [route-parallel-model](references/route-parallel-model.md) - Use RSVP.hash() for parallel data loading
- [route-loading-substates](references/route-loading-substates.md) - Implement loading substates for better UX
- [route-lazy-routes](references/route-lazy-routes.md) - Use route-based code splitting with Embroider
- [route-templates](references/route-templates.md) - Use route templates with co-located syntax
- [route-model-caching](references/route-model-caching.md) - Implement smart route model caching

### 2. Build and Bundle Optimization (CRITICAL)

- [bundle-direct-imports](references/bundle-direct-imports.md) - Import directly, avoid entire namespaces
- [bundle-embroider-static](references/bundle-embroider-static.md) - Enable Embroider static mode for tree-shaking
- [bundle-lazy-dependencies](references/bundle-lazy-dependencies.md) - Lazy load heavy dependencies

### 3. Component and Reactivity Optimization (HIGH)

- [component-use-glimmer](references/component-use-glimmer.md) - Use Glimmer components over classic components
- [component-cached-getters](references/component-cached-getters.md) - Use @cached for expensive computations
- [component-minimal-tracking](references/component-minimal-tracking.md) - Only track properties that affect rendering
- [component-no-tracked-writes-in-render](references/component-no-tracked-writes-in-render.md) - Don't update tracked state while rendering
- [component-tracked-toolbox](references/component-tracked-toolbox.md) - Use tracked collections for complex state
- [component-composition-patterns](references/component-composition-patterns.md) - Use yield blocks and contextual components
- [component-reactive-chains](references/component-reactive-chains.md) - Build reactive chains with dependent getters
- [component-class-fields](references/component-class-fields.md) - Use class fields for component composition
- [component-standalone-tracked](references/component-standalone-tracked.md) - Keep app state on classes, not in standalone tracked() values
- [component-controlled-forms](references/component-controlled-forms.md) - Implement controlled form patterns
- [component-on-modifier](references/component-on-modifier.md) - Use {{on}} modifier for event handling
- [component-args-validation](references/component-args-validation.md) - Validate component arguments
- [component-signatures](references/component-signatures.md) - Write precise signatures for components, helpers and modifiers
- [component-splattributes](references/component-splattributes.md) - Spread ...attributes on the right element, in the right position
- [component-memory-leaks](references/component-memory-leaks.md) - Prevent memory leaks in components
- [component-strict-mode](references/component-strict-mode.md) - Use strict mode and template-only components
- [component-avoid-classes-in-examples](references/component-avoid-classes-in-examples.md) - Avoid unnecessary classes in component examples
- [component-avoid-constructors](references/component-avoid-constructors.md) - Avoid constructors in Glimmer components
- [component-avoid-lifecycle-hooks](references/component-avoid-lifecycle-hooks.md) - Avoid legacy lifecycle hooks
- [component-file-conventions](references/component-file-conventions.md) - Follow proper file naming conventions
- [exports-named-with-default-fallback](references/exports-named-with-default-fallback.md) - Prefer named exports, with a default export for template lookup

### 4. Accessibility Best Practices (HIGH)

- [a11y-automated-testing](references/a11y-automated-testing.md) - Use ember-a11y-testing for automated checks
- [a11y-semantic-html](references/a11y-semantic-html.md) - Use semantic HTML and proper ARIA attributes
- [a11y-keyboard-navigation](references/a11y-keyboard-navigation.md) - Ensure full keyboard navigation support
- [a11y-form-labels](references/a11y-form-labels.md) - Associate labels with inputs, announce errors
- [a11y-route-announcements](references/a11y-route-announcements.md) - Announce route transitions to screen readers

### 5. Service and State Management (MEDIUM-HIGH)

- [service-cache-responses](references/service-cache-responses.md) - Cache API responses in services
- [service-shared-state](references/service-shared-state.md) - Use services for shared state
- [service-ember-data-optimization](references/service-ember-data-optimization.md) - Optimize WarpDrive queries
- [service-owner-linkage](references/service-owner-linkage.md) - Manage service owner and linkage patterns
- [service-data-requesting](references/service-data-requesting.md) - Implement robust data requesting patterns

### 6. Template Optimization (MEDIUM)

- [template-let-helper](references/template-let-helper.md) - Use {{#let}} to avoid recomputation
- [template-each-key](references/template-each-key.md) - Use {{#each}} with @key for efficient list updates
- [template-avoid-computation](references/template-avoid-computation.md) - Move expensive work to cached getters
- [template-helper-imports](references/template-helper-imports.md) - Import helpers directly in templates
- [template-conditional-rendering](references/template-conditional-rendering.md) - Optimize conditional rendering
- [template-fn-helper](references/template-fn-helper.md) - Use {{fn}} helper for partial application
- [template-only-component-functions](references/template-only-component-functions.md) - Use template-only components
- [helper-composition](references/helper-composition.md) - Compose helpers for reusable logic
- [helper-builtin-functions](references/helper-builtin-functions.md) - Use built-in helpers effectively
- [helper-plain-functions](references/helper-plain-functions.md) - Write helpers as plain functions

### 7. Performance Optimization (MEDIUM)

- [performance-on-modifier-vs-handlers](references/performance-on-modifier-vs-handlers.md) - Use {{on}} modifier instead of event handler properties

### 8. Testing Best Practices (MEDIUM)

- [testing-modern-patterns](references/testing-modern-patterns.md) - Use modern testing patterns
- [testing-qunit-dom-assertions](references/testing-qunit-dom-assertions.md) - Use qunit-dom for better test assertions
- [testing-test-waiters](references/testing-test-waiters.md) - Use @ember/test-waiters for async testing
- [testing-render-patterns](references/testing-render-patterns.md) - Use correct render patterns for components
- [testing-msw-setup](references/testing-msw-setup.md) - Mock API requests with MSW
- [testing-library-dom-abstraction](references/testing-library-dom-abstraction.md) - Use Testing Library patterns

### 9. Tooling and Configuration (MEDIUM)

- [vscode-setup-recommended](references/vscode-setup-recommended.md) - VS Code extensions and MCP server setup

### 10. Advanced Patterns (MEDIUM-HIGH)

- [advanced-modifiers](references/advanced-modifiers.md) - Use modifiers for DOM side effects
- [advanced-modifier-reruns](references/advanced-modifier-reruns.md) - Keep expensive modifier setup separate from updates
- [advanced-helpers](references/advanced-helpers.md) - Extract reusable logic into helpers
- [advanced-tracked-built-ins](references/advanced-tracked-built-ins.md) - Use reactive collections from @ember/reactive/collections
- [advanced-concurrency](references/advanced-concurrency.md) - Use ember-concurrency for task management
- [advanced-data-loading-with-ember-concurrency](references/advanced-data-loading-with-ember-concurrency.md) - Data loading patterns with ember-concurrency

## How to Use

Each entry in the Quick Reference links to its rule in `references/`. Read the rules that apply to the task before writing or reviewing code, rather than loading them all.

Each rule file contains:

- Brief explanation of why it matters
- Incorrect code example with explanation
- Correct code example with explanation
- Links to the official documentation it is based on

## Accessibility with OSS Tools

Ember has excellent accessibility support through community addons:

- **ember-a11y-testing** - Automated accessibility testing in your test suite
- **ember-a11y-refocus** - Route announcements and focus management
- **ember-focus-trap** - Focus trapping for modals and dialogs
- **ember-page-title** - Accessible page title management
- **Platform-native validation** - Use browser's Constraint Validation API for accessible form validation

These tools, combined with native web platform features, provide comprehensive a11y support with minimal configuration.

## Full Compiled Document

For the complete guide with all rules expanded: `AGENTS.md`
