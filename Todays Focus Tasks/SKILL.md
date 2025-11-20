---
name: todays-focus-tasks
description: This skill transfers focus tasks from the daily "@Today" note in Notion to Todoist. It should be used when the user wants to sync their daily focus tasks, import today's tasks from Notion, or create Todoist tasks from their daily planning note. Trigger phrases include "sync my focus tasks", "import today's tasks", "create tasks from my daily note", or "todays focus tasks".
---

# Today's Focus Tasks

This skill automates the transfer of focus tasks from the user's daily "@Today" note in Notion to Todoist.

## When to Use

Use this skill when the user wants to:
- Sync their daily focus tasks from Notion to Todoist
- Import today's tasks from their daily planning note
- Create Todoist tasks from their "@Today" note

## Workflow

### Step 1: Find the @Today Note in Notion

Search for today's note using the Notion search tool:

```
Notion:notion-search
- query: "@Today" or the current date
- query_type: internal
```

Look for a page with the title "@Today" or containing today's date. The note is typically in the Notes database with a "Daily" category.

### Step 2: Fetch the Note Contents

Once the page is identified, fetch its full contents:

```
Notion:notion-fetch
- id: [page URL or ID from search results]
```

### Step 3: Extract Focus Tasks

Parse the page content to identify the focus tasks. The tasks are formatted as a bullet point list under a "Focus" heading:

```
Focus
- Task 1
- Task 2
- Task 3
```

Extract each bullet point as a separate task. If a task contains a URL (e.g., a Confluence link), preserve it in the task description.

### Step 4: Find the Mapp Project in Todoist

Search for the Mapp project:

```
todoist:find-projects
- search: Mapp
```

Note the project ID for use in task creation.

### Step 5: Create Tasks in Todoist

Create all extracted tasks in Todoist with the following parameters:

```
todoist:add-tasks
- tasks: [array of task objects]
  - content: [task text]
  - projectId: [Mapp project ID]
  - dueString: "today"
  - labels: ["Focus"]
  - description: [any URLs or additional context from the task]
```

## Configuration

- **Notion Note Title**: @Today (in the Notes database)
- **Todoist Project**: Mapp
- **Due Date**: today
- **Label**: Focus

## Example Output

After successful execution, confirm the tasks created:

"Created X focus tasks in your Mapp project with today's due date and the Focus label:
1. [Task 1]
2. [Task 2]
..."
