---
name: project-select
description: Project selector for workspace navigation. Use when user wants to navigate between projects in the workspace (/Users/mengxianhua/workspace_imp). First cd to workspace directory, then list all projects sorted alphabetically, and finally cd to the user-specified project directory.
---

# Project-select

## Overview

Navigate to projects in the workspace directory `/Users/mengxianhua/workspace_imp` by name.

## Workflow

When user provides a project name:

1. **Navigate to workspace directory**:
   ```bash
   cd /Users/mengxianhua/workspace_imp && pwd
   ```

2. **List all projects sorted alphabetically**:
   ```bash
   ls -1 | sort
   ```

3. **Navigate to the user-specified project**:
   ```bash
   cd <project-name>
   ```

## Usage

User input: Select a project directory to work in.

Example:
```
User: kxpay
Action: cd /Users/mengxianhua/workspace_imp/kxpay
```

## Notes

- The workspace contains approximately 70-80 sub-projects
- Always verify the project exists before attempting to cd into it
- If project name is ambiguous or not found, list available projects for the user to select from