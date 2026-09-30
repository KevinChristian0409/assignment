# Solution

## Task A — Root cause analysis

### Failing test 1: `search filters the task list by title` (`./tests/e2e/search.spec.ts`)

- **Root cause: The Page Object Model (POM)'s `search` method was using the incorrect `data-testid`, `task-search-input` while the search input in the application uses `search-input`. As a result, Playwright could not locate the search field and the test timed out.**

![Playwright test failure](docs/screenshots/task-a-search-failure.png)

- **Fix applied: Updated the `search` method in `TaskManagerPage.ts` to use the correct existing `search-input` locator**

![Application search input and correct data-testid](docs/screenshots/task-a-search-locator.png)

### Failing test 2: `marking a task as Done updates its status badge` (`./tests/e2e/task-status.spec.ts`)

- **Root cause: The test expects the task status badge to have text `Completed`, but the application uses `Done` as the status value**

![Test failure showing expected Completed and received Done](docs/screenshots/task-a-status-failure.png)

- **Fix applied: Updated the expect statement for task status badge to `Done`**

![Application showing the task status as Done](docs/screenshots/task-a-status-done.png)

## Task B — New test

- **Scenario covered: Cancelling an edit does not update the task**
- **Why this scenario matters / why it was missing: The existing tests check that an edit can be saved, but they don't check what happens when the user cancels the edit. I added this test to make sure any changes are discarded and the task stays the same.**

## Task C — API validation

- **What the new API test verifies: The test verifies that a new task can be created using the `POST /tasks` endpoint. It checks that the response returns status code `201`, contains the expected task fields, and that the title, description, and status match the values sent in the request.**

## Task D — Bug / usability / improvement report

- **What I observed: Clicking the Delete button removes the task immediately without asking the user to confirm the action.**
- **Steps to reproduce (if applicable): 1.Open the Task Manager 2. Find any task in the task list 3.Click the Delete button 4.The task is removed immediately**
- **Why it matters: A user could accidentally delete a task by clicking the Delete button by mistake.**
- **Suggested fix or improvement: Add a confirmation message before deleting a task, such as asking the user if they are sure they want to delete it. This would give the user a chance to cancel the action.**

## Anything else you'd like us to know

- - Coincidentally, I recently worked on a mini Jira-style project, so I found this assessment quite familiar and enjoyable to work through.

- One small note: I have VS Code configured to run Prettier automatically when I save files, so some files may show formatting changes in the commits in addition to the changes related to the assessment.
