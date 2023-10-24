## 1. Starting a repo

- At the start of the project, just create a `main` branch and start pushing code. In this phase it's not very recommended o create feature branches, since the code will be changing constantly, so communication is critical if more than one person is working on the project
- When developers agree that the project has reached a more stable status, it's time to adopt git ship. It will be done in the following way:
	1. Create a branch named `release/1.0`
	2. Make sure the latest changes of `main` are in this newly created branch
	3. Now start using Git Ship. To keep working just branch out from `release/1.0`

---
## 2. Lingering features

Lets suppose that we created a feature branch from `release/1.0`, but before merging it back, it's decided to get postponed or developing this feature turns out to take a long time.

When this happens, it's possible that the release branches continued going forward. In this example, when the feature is complete, `release/1.3` was already created. When this happens, the merging process will vary between the nature of the feature branch:
- Feature: Merge to `release/1.3`. Make sure to resolve conflicts correctly since several releases have gone by. Don't merge with previous releases, because they will not be receiving new features (just bug fixes)
- Fix: If it was an fix for `release/1.0` that hasn't been resolved, merge this feature branch with `release/1.0`, `release/1.1`, `release/1.2` and `release/1.3`

---
## 3. Hotfixes

If you're about to do an important fix, it's an option to bypass the usual Git Ship flow (create branch, change, merge back) and commit directly to the release branch, subsequently merging it with `main` and generating a new patch version

---


## 1. Initializing a Repository

- At the start of a project, establish a `main` branch and begin pushing code to it. During this phase, it's advisable to avoid creating feature branches as the code will be in a constant state of change. If multiple individuals are collaborating on the project, effective communication is crucial.
- Once a consensus is reached among the developers regarding the stability of the project, it's time to implement the Git Ship workflow. Follow these steps:
    1. Establish a branch named `release/1.0`.
    2. Ensure the latest updates from the `main` branch are merged into `release/1.0`.
    3. Initiate the use of Git Ship. Henceforth, branch off from `release/1.0` for ongoing development work.

---
## 2. Managing Ongoing Features

Suppose a feature branch is branched off from `release/1.0`, but its merging gets postponed, or its development extends over a prolonged period.

Meanwhile, release branches might have progressed; for instance, `release/1.3` might be established by the time the feature is completed. The merging approach will be contingent on the nature of the feature branch:

- **Feature:** Merge the feature branch into `release/1.3`. Given the passage of several releases, ensure conflict resolutions are handled accurately. Avoid merging with earlier releases as they are only earmarked for bug resolutions, not new features.
- **Fix:** If it pertains to a fix for `release/1.0` that remains unaddressed, merge the feature branch with `release/1.0`, `release/1.1`, `release/1.2`, and `release/1.3` sequentially.

---
## 3. Hotfix Procedures

For crucial fixes, there's an option to deviate from the standard Git Ship workflow (create branch, make changes, merge back) and commit directly to the relevant release branch. Following this, merge the fix with the `main` branch and roll out a new patch version.

---


