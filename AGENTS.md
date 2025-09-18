# Repository Guidelines

## Project Structure & Module Organization
- Root `pom.xml` aggregates the Java modules; main service lives in `stockinfo-analysis`.
- Service code sits in `stockinfo-analysis/src/main/java/com/jerrystarter/analysis`, with configuration under `src/main/resources`.
- Database migrations use Liquibase changelog files in `src/main/resources/db/changelog`.
- `akshare_data` stores cached AKShare artifacts and is mounted into containers; keep large datasets out of Git.

## Build, Test, and Development Commands
- `mvn clean install` from the root builds all modules and produces the runnable JAR in `stockinfo-analysis/target`.
- `mvn -pl stockinfo-analysis spring-boot:run` starts the API locally on port 18080 using the default profile.
- `docker build -t aktools:latest -f Dockerfile.aktools .` refreshes the local AKTools image used by Compose.
- `docker-compose up --build` launches the full stack (service, PostgreSQL, RocketMQ, AKTools) for integration testing.

## Coding Style & Naming Conventions
- Use Java 17, 4-space indentation, and standard Spring annotations; follow `PascalCase` for classes, `camelCase` for methods/fields.
- Place new configs in `application.yml` or profile-specific files; keep secrets out of source.
- Mapper XML files belong under `src/main/resources/mapper`, mirroring package structure.

## Testing Guidelines
- Add unit tests under `src/test/java`, matching package names; name classes `*Tests`.
- Prefer JUnit 5; if adding integration tests, annotate with `@SpringBootTest` and isolate external dependencies.
- Run `mvn test -pl stockinfo-analysis` before pushing; document any skipped suites in the PR.

## Commit & Pull Request Guidelines
- Follow the existing short-prefix format: `MOD: ...`, `FIX: ...`, `ADD: ...`; describe the observable change in sentence case.
- Keep commits focused and rebased; avoid committing generated files in `target/` or datasets.
- PRs should include a concise summary, deployment or migration notes, linked issues, and screenshots or curl examples when APIs change.

## Environment & Deployment Notes
- Update Liquibase changelogs incrementally; never edit past change sets.
- When running via Compose, align service env vars with `SPRING_PROFILES_ACTIVE=prod`; override in `.env` for local tweaks.
- Expose new topics or queues through RocketMQ configuration and document them alongside the code change.
