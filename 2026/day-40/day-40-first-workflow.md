# Day 40 – Your First GitHub Actions Workflow

## What I Learned

After completing this task, I learned the following important concepts about GitHub Actions:

* How CI/CD pipelines can run automatically in the cloud.
* How a workflow is triggered when code is pushed to a GitHub repository.
* How GitHub Actions uses **workflow files written in YAML** to define automation.
* The purpose of **jobs, steps, runners, and actions**.
* How to view workflow runs inside the **GitHub Actions tab**.
* How to intentionally break a pipeline and debug errors.
* How to read logs of each step to understand what happened during execution.

This task helped me understand the **basic structure of a CI/CD pipeline using GitHub Actions**.

---

# Workflow Keywords Explanation

## on:

The `on:` keyword defines **which event triggers the workflow**.

Example:

```yaml
on: push
```

This means the workflow will start running whenever code is pushed to the repository.

Other possible triggers include:

* `pull_request`
* `workflow_dispatch` (manual trigger)
* `schedule` (cron jobs)

---

## jobs:

The `jobs:` section defines **the set of jobs that will run in the workflow**.

Each job represents a group of tasks executed on a runner.

Example:

```yaml
jobs:
  greet:
```

A workflow can contain **multiple jobs**, and they can run either **sequentially or in parallel**.

---

## runs-on:

The `runs-on:` keyword defines **which machine will run the job**.

Example:

```yaml
runs-on: ubuntu-latest
```

This tells GitHub to create a temporary Ubuntu virtual machine and execute the job there.

Common runner options include:

* ubuntu-latest
* windows-latest
* macos-latest

These machines are called **GitHub-hosted runners**.

---

## steps:

The `steps:` section defines **individual tasks executed inside a job**.

Each step performs a specific action such as running a command or using a predefined GitHub action.

Example:

```yaml
steps:
  - run: echo "Hello"
```

Steps run **in sequence** from top to bottom.

---

## uses:

The `uses:` keyword is used to **call a reusable GitHub Action** created by GitHub or the community.

Example:

```yaml
uses: actions/checkout@v4
```

This action downloads the repository code onto the runner machine so that it can be used by later steps.

---

## run:

The `run:` keyword is used to **execute shell commands on the runner machine**.

Example:

```yaml
run: echo "Hello from GitHub Actions"
```

You can run multiple commands such as:

* installing dependencies
* running scripts
* building applications
* running tests

---

## name:

The `name:` keyword is used to **provide a human-readable label for workflows, jobs, or steps**.

Example:

```yaml
- name: Print Greeting
```

This name appears in the GitHub Actions logs and helps make pipelines easier to understand.

---

# Workflow File Used in This Task

Location of workflow file:

```
.github/workflows/hello.yml
```

Workflow code:

```yaml
name: Hello Workflow

on: push

jobs:

  greet:

    runs-on: ubuntu-latest

    steps:

      - name: Checkout Repository
        uses: actions/checkout@v4

      - name: Print Greeting
        run: echo "Hello from GitHub Actions!"

      - name: Print Date
        run: date

      - name: Print Branch Name
        run: echo "Branch name is ${{ github.ref_name }}"

      - name: List Repository Files
        run: ls -la

      - name: Print Runner OS
        run: echo "Runner OS is $RUNNER_OS"
```

---

# Screenshot of Successful Workflow Run

(Add your screenshot here)

Example:

```
Actions → Hello Workflow → greet → Success (Green ✔)
```

Insert screenshot below:

![Workflow Success](workflow-success.png)

---

# Understanding the Workflow Execution

When code is pushed to the repository, the following process occurs:

1. GitHub detects the **push event**.
2. The workflow defined in `.github/workflows/hello.yml` is triggered.
3. GitHub creates a **runner machine (Ubuntu VM)**.
4. The job `greet` starts executing.
5. Each step runs one by one:

   * Checkout repository
   * Print greeting
   * Print date
   * Show branch name
   * List repository files
   * Display runner OS
6. If all steps succeed, the pipeline turns **green**.

---

# Breaking the Pipeline (Experiment)

To understand failure behavior, I added a step that intentionally fails.

Example:

```yaml
- name: Break the Pipeline
  run: exit 1
```

After pushing this change, the pipeline failed and GitHub marked the workflow with a **red status**.

From this experiment I learned:

* Pipelines stop execution when a step fails.
* Logs show the exact command that caused the failure.
* Fixing the error and pushing again triggers a new pipeline run.

---

# Repository Structure

```
github-actions-practice
│
├── .github
│   └── workflows
│       └── hello.yml
│
└── 2026
    └── day-40
        ├── day-40-first-workflow.md
        └── workflow-success.png
```

---

# Key GitHub Actions Concepts (Summary)

| Concept  | Description                         |
| -------- | ----------------------------------- |
| Workflow | Automation pipeline defined in YAML |
| Event    | Trigger that starts the workflow    |
| Job      | Group of steps executed on a runner |
| Step     | Individual command or action        |
| Runner   | Machine where the workflow runs     |
| Action   | Reusable automation component       |

---

# Final Summary

GitHub Actions allows developers to automate CI/CD pipelines directly inside GitHub repositories.

By creating my first workflow, I learned how to:

* trigger pipelines automatically,
* execute commands on cloud runners,
* understand workflow structure,
* and debug pipeline failures.

This task demonstrated how **CI/CD pipelines operate in real-world DevOps workflows**.
