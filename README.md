[![support version](https://img.shields.io/badge/kotlin-1.9.22%2B-blueviolet.svg?style=flat&logo=kotlin&label=kotlin&labelColor=%23000&color=%23a97bff)](https://github.com/JetBrains/kotlin/releases/tag/v1.9.22) [![support version](https://img.shields.io/badge/Compose-1.5.10%2B-blueviolet.svg?style=flat&logo=jetpackcompose&label=JCompose&labelColor=%23000&color=%234285F4)](https://github.com/JetBrains/compose-multiplatform/releases?q=1.5.10) [![support version](https://img.shields.io/badge/kotlin-2.51.0%2B-blueviolet.svg?style=flat&logo=android&label=Hilt&labelColor=%23000&color=%234cc71e
)](https://github.com/google/dagger/releases/tag/dagger-2.51) [![support version](https://img.shields.io/badge/Room-2.6.1-blueviolet.svg?style=flat&logo=sqlite&logoColor=%23d085a0&label=Room&labelColor=%23000&color=%23d085a0
)](https://developer.android.com/jetpack/androidx/releases/room) [![support version](https://img.shields.io/badge/Retrofit-2.10.0-blueviolet.svg?style=flat&logo=postman&label=Retrofit&labelColor=%23000&color=%23FF6C37
)](https://github.com/square/retrofit/releases/tag/2.10.0) [![support version](https://img.shields.io/badge/Apollo-3.8.3%2B-blueviolet.svg?style=flat&logo=apollographql&label=Apollo&labelColor=%23000&logoColor=%23E10098&color=%23E10098
)](https://github.com/apollographql/apollo-kotlin/releases/tag/v3.8.3)

# PowerPlay Android App: Getting started on this repository

## Kotlin code style:
Kotlin code should follow common [convention](https://kotlinlang.org/docs/coding-conventions.html).

## App:
- Kotlin `1.9.22` or [higher](https://kotlinlang.org/docs/releases.html).
- Architecture: `MVVM`
- Navigation: Android Jetpack's Navigation
- UI: Jetpack Compose with Compiler `1.5.10`. See Compiler-Kotlin compatibility [here](https://developer.android.com/jetpack/androidx/releases/compose-kotlin#pre-release_kotlin_compatibility).
- DI: Hilt `2.51.0` or [higher](https://mvnrepository.com/artifact/com.google.dagger/hilt-android). Following official [guide](https://developer.android.com/training/dependency-injection/hilt-android) to use best practices
- DB: Database used is Room `2.6.1` or [higher](https://developer.android.com/jetpack/androidx/releases/room)
- Networking:
  - [REST client] Retrofit `2.10.0`
  - [GraphQL client] Apollo `3.8.3`
- Versioning: We use [semantic versioning](https://www.semver.org)

## CI/CD:
### Test
Using a `test` branch, you can provide builds to testers.  
After completing the tasks you should merge the code from the `develop` branch to the `test` branch, then **Github Actions** will launch a workflow to create a new build. Once the build is built *(you can see it [here](https://github.com/Team-PowerPlay/ontario-android/actions))*, it will be submitted to the distribution service. The project uses **Firebase App Distribution** as a service for distributing. You can see more details about this service [here](https://firebase.google.com/docs/app-distribution).

> [!NOTE]
> Since workflow is not capable of raising versions of test builds - you need to manually describe the build changes *(steps 3-5 below)* to the tester so that he understands which tasks he should pay attention to. In the future, we will try to simplify this flow.

Follow the instructions to submit a build for testing:
1. Having done some task you merge it into the `develop` branch.
2. To provide a build with this task, you merge the current `develop` branch code into the `test` branch.
  - Once the code has been pushed in the `test` branch - **Github Actions** immediately starts building the build for testing.
  - When the build is created, workflow will automatically provide the build to the **Firebase App Distribution** service.
  - After that, when the build is uploaded, the workflow will be successfully completed.
3. Navigate to the **Firebase App Distribution** console.
4. Find the most recently uploaded build and open its details.
5. Go to the **Release notes** tab and describe the tasks that were completed as part of this testing.

### Release
NOT IMPLEMENTED YET.

## Repository Workflow:

> [!CAUTION]
> **Before you start working with Git, ensure you set up SSH or GPG commit signing. Follow the [provided instructions](https://docs.github.com/en/authentication/managing-commit-signature-verification/about-commit-signature-verification#ssh-commit-signature-verification).**
### Branching Strategy
- **`develop` Branch**: Use this branch as the main development branch. From here, create:
  - `feature` branches for implementing new features (e.g., `feature/MAD-0/registration-flow`).
  - `bugfix` branches for fixing bugs (e.g., `bugfix/MAD-0/registration-flow`).
- **Merge to `test`**: After a certain number of tasks are completed, merge the code from the `develop` branch to the `test` branch. This will automatically start the workflow and create a build for testers to test the completed tasks *(more details in [**CI/CD** section](https://github.com/Team-PowerPlay/ontario-android/edit/develop/README.md#test))*.
- **Release Branches**: Create `release/x.x.x` branches for version releases. Until a release is made, all changes should be on `develop`.
- **Merge to `main`**: After a release, merge code from `release/x.x.x` branches into `main`.

### Committing Guidelines
- **Commit Format**: Follow the format `MAD-0: Commit message`, where `MAD-0` is the Jira task identifier and `Commit message` describes the change.
- **Single Commit**: It's recommended to make one commit per feature or fix.

### Merge Rules
- **Force Push**: Prohibited on all branches except `feature` and `bugfix`.
- **Code Review**: Require at least one approval during code review.
- **Cleanup After PR**: Delete feature or fix branches after merging to avoid clutter.
- **Squash Commits**: Perform squash commits during merge.
- **Rebase Over Merge**: While it's recommended to use rebase over merge for a cleaner history tree, the choice is ultimately yours.
- **CI Integration**: Ensure tests pass and approval is given before merging. 
