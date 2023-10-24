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
- Feature: Merge to `release/1.3`. Make sure to resolve conflicts correctly since several releases have gone by
- Fix: If it was an fix for `release/1.0` that wasn't fixed yet 

