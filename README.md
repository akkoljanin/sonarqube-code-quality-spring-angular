# SonarQube Code Quality Analysis: Spring Boot & Angular

Static code analysis of a full-stack application (Spring Boot backend + Angular frontend) with **SonarQube** and **SonarScanner**. All detected issues were reviewed and fixed until the final analysis reported **0 issues in security, reliability and maintainability** for both projects.

Done as a project for the *Information Systems Reengineering* course at the Faculty of Technical Sciences (FTN), University of Novi Sad.

---

## Scope

| Project | Stack | Analysed with |
|---|---|---|
| **RVA Backend** | Java, Spring Boot, Maven (REST controllers, service layer, domain model, integration tests) | SonarQube + Maven |
| **Frontend** | Angular, TypeScript, HTML/CSS, Angular Material | SonarQube + SonarScanner, SonarLint in the IDE |

The application is a banking information system (entities such as bank, branch, service, service user) built in the *Multi-tier Application Development* course.

## Results

| Project | Security | Reliability | Maintainability |
|---|---|---|---|
| Backend, before | 0 | 11 | 51 |
| Backend, after | 0 | 0 | 0 |
| Frontend, before | 0 | 17 | 35 |
| Frontend, after | 0 | 0 | 0 |

Final Quality Gate status: **Passed** for both projects.

## Issues found and how they were fixed

### Backend (Spring Boot / Java)

| Issue | Rule | Fix |
|---|---|---|
| Unused imports | `java:S1128` | Removed in controllers, services, models and tests |
| Wildcard generic return type `ResponseEntity<?>` | `java:S1452` | Replaced with concrete types (`Banka`, `Filijala`, ...) |
| Field injection with `@Autowired` | `java:S6813` | Switched to constructor injection with `final` fields |
| Duplicated string literals | Sonar code smell | Extracted into constants |
| Commented-out code in integration tests | Sonar code smell | Removed |
| `Math.random()` as insecure PRNG | Security hotspot | Replaced with `SecureRandom` |

### Frontend (Angular / TypeScript)

| Issue | Rule | Fix |
|---|---|---|
| Insufficient text/background contrast (WCAG) | `css:S7924` | Adjusted colours in CSS/HTML |
| Comma operator inside `subscribe` | `typescript:S878` | Restructured into proper `next` / `error` callbacks |
| Expression with no effect (misplaced error callback) | `typescript:S905` | Moved the callback into the `subscribe` call |
| Unused imports and commented-out code | Sonar code smells | Removed |
| Table rows not keyboard-accessible | Accessibility | Added `tabindex` and a `keydown` handler |
| Class members never reassigned | Maintainability | Marked as `readonly` |
| Promise-chain bootstrap | Modernisation | Replaced `.catch()` with top-level `await` |

## What the report also covers

- SonarQube architecture (server, Compute Engine, Elasticsearch, database, plugins) and the role of SonarScanner.
- Issue types (bugs, vulnerabilities, code smells, security hotspots) and severity levels.
- Dashboard, metrics, Quality Gates and Quality Profiles.
- CI/CD integration and the benefits of static analysis in industrial projects.

## Limitations

- Test coverage is **0 %** in both projects: the analysis focused on fixing detected issues, not on writing unit tests.
- Only the Spring and Angular projects are analysed in the report's results.

## Repository contents

```
├── README.md
└── SonarQube_Static_Analysis_Report.pdf    # Full report (Serbian) with screenshots, before/after code and rationale
```

The source code of the analysed applications is not included here. The report contains the original and corrected code for every issue type.

## Tools

SonarQube Community, SonarScanner, SonarLint (VS Code), Maven, Spring Boot, Angular, TypeScript.

