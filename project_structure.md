# Project Structure

## Root Layout
```
stock_info/
├── akshare_data/                 # Local cache mounted into the AKTools container
├── Dockerfile.aktools            # Builds the AKShare/AKTools helper image
├── docker-compose.yml            # Orchestrates AKTools, analysis service, Postgres, RocketMQ
├── pom.xml                       # Maven parent POM aggregating modules
├── stockinfo-analysis/           # Spring Boot analysis service module
├── LICENSE
└── AGENTS.md                     # Contributor guidelines
```
Supplementary IDE/config directories (`.codebuddy/`, `.idea/`, `.vscode/`) and Git metadata live alongside these files.

## Module: stockinfo-analysis
```
stockinfo-analysis/
├── pom.xml                       # Module-specific dependencies and plugins
├── Dockerfile                    # Runtime image for the analysis service
├── src/
│   ├── main/
│   │   ├── java/com/jerrystarter/analysis/
│   │   │   └── StockinfoAnalysisApplication.java  # Spring Boot entry point
│   │   └── resources/
│   │       ├── application.yml                   # Service configuration
│   │       └── db/changelog/db.changelog-master.xml  # Liquibase migrations
│   └── test/java/                               # Placeholder for unit tests
└── target/                                     # Maven build output (generated)
    ├── classes/
    ├── test-classes/
    └── ...
```
`src/main/java` currently contains the core application bootstrap; additional packages should mirror the `com.jerrystarter.analysis` namespace. Resource files (YAML configs, Liquibase changelogs, mapper XML) belong under `src/main/resources`.

## Supporting Infrastructure
- `docker-compose.yml` wires the analysis service with Postgres and RocketMQ; service exposes port 18080.
- `Dockerfile.aktools` and `akshare_data/` support a local AKTools container that fronts AKShare APIs.
- Build artifacts reside in `stockinfo-analysis/target/` and should be cleaned via `mvn clean` or excluded from commits.
