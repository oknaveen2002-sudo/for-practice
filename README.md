# CI/CD Demo (Java + Maven + GitHub Actions)

A minimal Java project for practicing CI/CD pipelines with GitHub Actions.

## Project structure

```
ci-cd-demo/
├── .github/workflows/ci.yml   # GitHub Actions pipeline (build, test, package, deploy placeholder)
├── pom.xml                    # Maven build file
└── src/
    ├── main/java/com/example/demo/
    │   ├── App.java            # Entry point
    │   └── Calculator.java     # Class under test
    └── test/java/com/example/demo/
        └── CalculatorTest.java # JUnit 5 tests
```

## Run locally

```bash
mvn compile        # build
mvn test           # run unit tests
mvn package         # produce target/ci-cd-demo.jar
java -jar target/ci-cd-demo.jar
```

## How to use this for practice

1. Create a new GitHub repository and push this project to it (or unzip it into an existing repo).
2. Go to the repo's **Actions** tab — GitHub will automatically detect `.github/workflows/ci.yml`.
3. Push a commit or open a pull request against `main` and watch the pipeline:
   - `build-and-test` job compiles the code, runs the JUnit tests, and packages a JAR.
   - `deploy` job only runs on pushes to `main` (and only after tests pass) — it currently just echoes a placeholder message.
4. Try breaking a test (e.g. change an assertion in `CalculatorTest.java`) and push — you'll see the workflow fail.
5. Extend the `deploy` step with something real once you're comfortable: e.g.
   - Build and push a Docker image
   - Deploy to a cloud service (AWS/GCP/Azure/Render/Heroku)
   - Publish the JAR to GitHub Packages or Maven Central

## Ideas to extend your practice

- Add a code coverage tool (JaCoCo) and upload the report as an artifact.
- Add a linting/static-analysis step (Checkstyle, SpotBugs).
- Add a matrix build to test against multiple JDK versions (11, 17, 21).
- Add branch protection rules requiring the workflow to pass before merging.
- Split into separate `ci.yml` (test on every push/PR) and `cd.yml` (deploy on release tag) workflows.
