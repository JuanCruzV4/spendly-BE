# Copilot Instructions for spendly-BE

- Stack: NestJS 11 + TypeScript; entry bootstrap in [src/main.ts](src/main.ts) creates the app and listens on `PORT` env (defaults 3000).
- Composition: `AppModule` in [src/app.module.ts](src/app.module.ts) is empty; new features should be added via Nest modules/services/controllers instead of piling into `main.ts`.
- Build output: TypeScript compiles to `dist` with ES2023 target, decorators, and metadata enabled ([tsconfig.json](tsconfig.json)).
- Scripts (npm): `start` (Nest), `start:dev` (watch), `start:debug`, `start:prod` (runs `dist/main`), `build` (Nest compiler), `lint` (eslint with `--fix`), `format` (Prettier on src/test), `test` (Jest unit), `test:watch`, `test:cov`, `test:debug`, `test:e2e` (separate config at [test/jest-e2e.json](test/jest-e2e.json)).
- Testing defaults: unit tests live under `src` matching `*.spec.ts`; e2e specs match `.e2e-spec.ts` under `test` rootDir.
- Linting: eslint covers `{src,apps,libs,test}/**/*.ts`; prefer autofix via `npm run lint` before commits.
- Formatting: `npm run format` applies Prettier; keep codebase aligned with this instead of ad-hoc formatting.
- Dependency baseline: only Nest core packages plus RxJS and reflect-metadata are present—introduce new libs sparingly and justify in PR notes.
- Error handling/logging: rely on Nest defaults (exceptions filters/loggers); introduce cross-cutting concerns via Nest providers rather than ad-hoc console usage.
- Configuration: prefer environment variables surfaced in `main.ts` (e.g., `PORT`); wire additional config through Nest ConfigModule when expanding.
- Module pattern: add new modules and controllers under `src/<feature>` and import them in `AppModule`; keep providers injectable and lean.
- DX tips: use `start:dev` for watch; for debugging use `start:debug` or `test:debug` with Node inspector.
- Output artifacts: `dist/` is generated—avoid checking it in.
- When adding tests: align Jest paths with rootDir (`src` for unit, `test` for e2e); keep coverage via `test:cov` to validate additions.
- Keep README in sync if commands or entrypoints change; it currently mirrors the Nest starter.
- If you add request handlers, validate inputs at controller level; follow Nest's DTO/pipe conventions even though none exist yet.
