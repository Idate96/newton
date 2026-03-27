# Robot Examples Guide

This folder covers articulated robots, imported assets, controllers, and policy playback.

## Common Patterns

- Imported assets and policies often come from `newton-assets` or other external sources. Follow the existing asset-download patterns instead of embedding large assets here.
- These examples often combine importers, articulations, world replication, viewers, and solver behavior in one place.

## Expectations

- Keep robot examples on public APIs and public asset workflows.
- If you change robot import or policy-loading behavior, update the corresponding example and the README entry together.
- Be careful with optional dependencies such as policy inference extras.

## Validation

- Run the example regression that covers the changed example, plus any import tests touched by the change.
