# Git and CircleCI beginner demo

This repository contains a tiny Python program and a CircleCI pipeline. The
pipeline runs a check on every push to GitHub. It verifies that `hello.py`
prints the expected greeting.

## What CI/CD means

- **Continuous Integration (CI):** automatically check code changes (for
  example, run tests) when you push them.
- **Continuous Delivery/Deployment (CD):** prepare or automatically publish an
  application to a server or hosting service.

This demo sets up **CI only**. It has no deployable web app or hosting target,
so it does not deploy anything.

## What you need

- A GitHub account and a repository that you can push to.
- A CircleCI account. The CircleCI service used below is CircleCI Cloud.
- Git installed on your computer.

The GitHub repository must contain this project, including
`.circleci/config.yml`. Check the repository URL before pushing:

```powershell
git remote -v
```

If `origin` is not the GitHub repository you own or can write to, change it:

```powershell
git remote set-url origin https://github.com/<YOUR-USERNAME>/<YOUR-REPOSITORY>.git
```

Replace both placeholders with the actual GitHub username and repository name.
Then push the project:

```powershell
git status
git add README.md .circleci/config.yml
git commit -m "Add CircleCI CI pipeline"
git push -u origin main
```

If Git says there is nothing to commit, continue to the push. If the push gets
a `403`, the GitHub account Git is signing in as needs write access to that
repository. CircleCI cannot fix GitHub push permissions.

## Step 1: Connect GitHub to CircleCI

1. Sign in or create an account at [CircleCI](https://circleci.com/).
2. Connect CircleCI to GitHub when prompted. Approve access for the GitHub
   account that contains your repository.
3. If asked which repositories CircleCI can access, allow access to this
   repository. You can usually choose selected repositories instead of granting
   access to all repositories.

CircleCI needs permission to read the repository and receive push events. This
is separate from the Git credentials used by `git push` on your computer.

## Step 2: Add this project in CircleCI

1. In CircleCI, open **Projects** (or the page for setting up a project).
2. Find the GitHub repository and select **Set Up Project**.
3. If CircleCI asks which configuration to use, choose the existing CircleCI
   config in the repository. It is at `.circleci/config.yml`. Do not replace it
   with a generated sample.
4. Choose the `main` branch if CircleCI asks for a branch, then start the
   pipeline.

If the repository is not listed, confirm that you connected the correct GitHub
account and that CircleCI was granted access to this repository. CircleCI's
screens may vary slightly depending on your GitHub integration.

## Step 3: Understand the configuration

Open `.circleci/config.yml`. It tells CircleCI what to run:

- `version: 2.1` selects CircleCI's configuration format.
- `jobs.test` defines a job named `test`.
- `cimg/python:3.12` gives the job a Linux container with Python 3.12.
- `checkout` downloads your repository into that container.
- The `run` step sends `CircleCI` to the program and checks that its output
  matches the expected greeting. A mismatch makes the job fail.
- `workflows.test-on-push` tells CircleCI to run the `test` job as part of a
  workflow.

CircleCI runs these commands on its own machine. You do not need to install
Python on your computer to run this CircleCI job.

## Step 4: Make a change and see CI run

1. Edit `hello.py` and save it.
2. In PowerShell, from the project folder, run:

   ```powershell
   git status
   git diff
   git add hello.py
   git commit -m "Change greeting"
   git push
   ```

3. Open the project in CircleCI and select **Pipelines**. A new pipeline should
   appear for your push.
4. Open the pipeline, then open the `test` job to see each step and its output.
   A green success means the check passed. A red failure means a step failed;
   open it to read the error.

If you change the expected greeting in `hello.py`, the check will fail until
you update the expected text in `.circleci/config.yml` too. This is a simple
way to see that CI catches an unexpected result.

## Troubleshooting

- **No pipeline appears:** make sure the commit was pushed to the connected
  repository and branch, and that CircleCI can access that repository.
- **The job cannot find `hello.py`:** confirm `.circleci/config.yml` is in the
  project root's `.circleci` folder and that `checkout` is present.
- **The greeting test fails:** compare the program's output with the expected
  string in the config. Spelling, punctuation, and spaces must match.
- **`git push` returns 403:** authenticate with a GitHub account that has
  write access, or ask the repository owner to grant that access.

## Keep learning

- [CircleCI: Create a project](https://docs.circleci.com/guides/getting-started/create-project/)
- [CircleCI: Hello world configuration](https://docs.circleci.com/guides/getting-started/hello-world)
- [CircleCI: Configuration reference](https://docs.circleci.com/reference/configuration-reference)
