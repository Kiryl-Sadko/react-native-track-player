# Repository Guidelines

## Project Structure & Module Organization
Library sources live in `src/`, with platform bridges under `src/android` and `src/ios` and shared utilities in `src/common`. Build outputs land in `lib/`; regenerate them rather than editing by hand. Native modules sit in `android/` and `ios/`, the HTML5 implementation lives in `web/`, the showcase app is in the `example/` workspace, and reference material is stored under `docs/`.

## Build, Test, and Development Commands
Install dependencies with `yarn install`. Run `yarn build` (alias `yarn prepare`) to compile and emit artifacts into `lib/`. `yarn lint`, `yarn format`, and `yarn typecheck` keep style and types in check, while `yarn test` runs the Jest suite. Use `yarn example ios` or `yarn example android` to launch the workspace app for manual verification. Run `yarn clean` before release builds to purge stale outputs.

## Coding Style & Naming Conventions
TypeScript spans the repo; prefer explicit exports from barrel files. Follow ESLint + Prettier defaults (2-space indent, single quotes, trailing commas). Components use PascalCase, hooks and functions use camelCase, and constants are SCREAMING_SNAKE_CASE. Group platform-specific code by directory rather than suffix when possible.

## Testing Guidelines
Jest drives unit tests; place specs under `src/__tests__` using the `*.test.tsx` pattern. Keep tests deterministic—mock timers and native bridges via Jest mocks when needed. Ensure `yarn test` and `yarn typecheck` pass before opening a PR, and expand coverage when touching playback state, queue handling, or native bridge boundaries.

## Commit & Pull Request Guidelines
Commits follow Conventional Commits (e.g., `feat: add queue prioritisation`, `fix: restore progress events`), enforced by Commitlint and surfaced in the changelog. Squash trivial fixups locally; version bumps are handled via `release-it`. Each PR should describe behaviour changes, link issues where relevant, and include example app screenshots for UI-affecting updates. Confirm `yarn lint`, `yarn test`, and `yarn typecheck` before requesting review, and tag maintainers if native code paths were touched.

## Native & Configuration Notes
Regenerate codegen artifacts after editing the TurboModule spec by running `yarn build` and rebuilding the example app. Keep secrets out of the repo; store Android keystores and iOS provisioning profiles locally. For native validation, run `./example/android/gradlew lintDebug` and `cd example/ios && pod install` after relevant changes.
