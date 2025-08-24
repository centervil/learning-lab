# AGENTS.md - Project Guidelines

## Quick Reference
- [1. Project Overview](#1-project-overview)
- [2. Workflow](#2-workflow)
  - [2.1. Branch Creation per Issue](#21-branch-creation-per-issue)
  - [2.2. Development Logs](#22-development-logs)
- [3. Commit Guidelines](#3-commit-guidelines)
  - [3.1. Commit Message Format](#31-commit-message-format)
  - [3.2. Commit Frequency (Atomic Commits)](#32-commit-frequency-atomic-commits)
- [4. Project Structure](#4-project-structure)
- [5. Operational Guidelines](#5-operational-guidelines)
  - [5.1. Git Management and `.gitignore`](#51-git-management-and-gitignore)
  - [5.2. Tooling and Version Management](#52-tooling-and-version-management)
  - [5.3. Quick Reference Maintenance](#53-quick-reference-maintenance)
- [6. Using Gemini CLI](#6-using-gemini-cli)

## 1. Project Overview

This repository is for conducting various technical verifications.

## 2. Workflow

### 2.1. Branch Creation per Issue

When starting work on each task (Issue), always create a new branch. It is recommended to name branches in a way that clearly indicates the Issue number and content (e.g., `issue-2-repo-setup`). Upon completion of the work, a Pull Request (PR) should be issued for review and merging into the main branch.

### 2.2. Development Logs

All work records will be saved as Markdown files within the `development_logs/` directory, following the guidelines below. This makes it easier to track work content and decisions later.

- **Location**: `development_logs/`
- **File Naming**: `YYYY-MM-DD-issue-[issue-number]-session-[session-number].md`
- **Content**: The log will contain a summary of actions taken, decisions made, and any issues encountered during the session. Crucially, it should explain *why* certain actions were taken, provide context for technical decisions, and briefly explain any specialized tools, libraries, or technical terms used, ensuring clarity for future reference and understanding.

## 3. Commit Guidelines

### 3.1. Commit Message Format

Commit messages should follow the structure below:

- **`<type>`**: `feat` (new feature), `fix` (bug fix), `chore` (miscellaneous), `docs` (documentation), `style` (code style), `refactor` (refactoring), `test` (testing), `ci` (CI related).
- **`<scope>` (optional)**: The part of the codebase affected (e.g., `dotfiles`, `install-script`).
- **`<description>`**: A concise, imperative-mood description of the change.
- **`<body>` (optional)**: The motivation and context for the change.
- **`<footer>` (optional)**: References to GitHub Issues (e.g., `Closes #123`) and breaking change notifications.

**Example:**
```
feat(dotfiles): add zsh configuration

Initial setup for zsh, including oh-my-zsh installation and basic plugin configuration.
Closes #5
```

### 3.2. Commit Frequency (Atomic Commits)

Each commit should be an "atomic" unit of work, representing a single, complete logical change.

- **One Change per Commit**: Avoid bundling unrelated changes (e.g., a feature and a typo fix) into one commit.
- **Commit Early, Commit Often**: Commit frequently at logical points in your development process.
- **Good Times to Commit**:
    1. After passing a new test (the "Green" in Red-Green-Refactor).
    2. After completing a refactoring of existing code.
    3. After a small, self-contained bug fix.
- **Keep Commits Clean**: Ensure that every commit leaves the project in a working state. Do not commit broken or work-in-progress code to a feature branch that will be merged.

## 4. Project Structure

This project follows a structured approach where each issue has its own dedicated directory for all related work. This ensures that all artifacts for a specific task are neatly organized.

- **Issue-Specific Directories**: For each new issue, a directory named `issue-<issue-number>` is created at the root of the repository. This directory will house all the files, code, and other materials related to that specific issue.

**Example Directory Structure:**
```
./
├── .github/
├── development_logs/   # Contains logs of development sessions
├── issue-16/           # Dedicated directory for work related to Issue #16
├── scripts/            # General-purpose scripts
└── AGENTS.md           # This file, containing guidelines
```

## 5. Operational Guidelines

### 5.1. Git Management and `.gitignore`

- **Strict Git Management**: Always be mindful of what is being added to Git. Only commit files that are essential for the project and should be version-controlled.
- **Proactive `.gitignore` Usage**: Immediately add entries to `.gitignore` for any new files or directories that are generated during development (e.g., build artifacts, temporary files, IDE-specific configurations, personal logs) and should not be tracked by Git.
- **Precise Staging**: Avoid using `git add .` indiscriminately. Prefer `git add <file>` or `git add -u` to stage only the intended changes, reducing the risk of accidentally committing unwanted files.

### 5.2. Tooling and Version Management

- **Version Dependency Awareness**: Be aware that tools and libraries can have breaking changes in major version updates. Always consult official documentation, migration guides, and changelogs before performing major version upgrades.
- **Official Documentation First**: When encountering issues or seeking to understand tool behavior, prioritize consulting the official documentation. This is the most reliable source of information for correct usage and best practices.

### 5.3. Quick Reference Maintenance

- **Update on Change**: The "Quick Reference" section at the top of this `AGENTS.md` document must be updated whenever new top-level sections or significant subsections are added, removed, or renamed. This ensures the quick reference remains accurate and useful for navigation.
- **Maintain Link Integrity**: Ensure that all links within the quick reference accurately point to the correct sections using Markdown anchor links (e.g., `[Section Name](#section-name)`).

## 6. Using Gemini CLI

In this project, `gemini-cli` is used to support task management and execution.

- **Checking Issues**: You can check the current list of tasks with `gh issue list`.
- **Issue Details**: You can view the details of a specific Issue with `gh issue view <issue-number>`.
- **Recording Work**: When recording work in `development_logs/` in Markdown format, you can refer to your interactions with `gemini-cli`.
- **Always Respond in Japanese**: When using `gemini-cli`, always respond in Japanese to maintain consistency with the project's language requirements.
