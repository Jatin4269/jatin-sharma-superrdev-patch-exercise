# Patch Notes

## Summary

I reviewed the task tracker across the React frontend, Spring Boot backend, and Oracle reference SQL. I focused on correctness issues affecting search/filter behavior, pagination state, and unnecessary request latency.

### Fixed

1. **Status filter precedence**

  * Fixed the SQL condition in `TaskRepository.java` by grouping the title/description `OR` condition before applying the status filter.

2. **Unnecessary backend delay**

  * Removed the artificial `Thread.sleep()` from `TaskController.java`, which added avoidable latency to API requests.

3. **Search/filter pagination state**

  * Updated `frontend/src/App.jsx` so changing the search query or status filter resets pagination to page 1.

4. **Oracle reference query precedence**

  * Applied the same SQL grouping fix to both the count query and paginated result query in `db/oracle/task_search_package.sql`.

## Not Changed

I did not add CRUD functionality because the provided smoke-test scope covers viewing, searching, filtering, and pagination. Adding task creation/edit/delete would introduce new functionality rather than fixing an existing required behavior.

I also did not change task IDs or pagination implementation because their observed behavior was consistent with the existing data/order and did not represent a demonstrated defect.

## Biggest Remaining Risk

The backend currently retrieves all matching tasks and performs pagination in Java. This may become inefficient as the dataset grows. A future improvement would be database-level pagination using Spring Data pagination/query limits.

## Tools / AI Used

Used PowerShell, Maven, npm/Vite, Git, browser-based manual testing, and AI assistance for code review, debugging, and reasoning about the patch. All changes were reviewed manually and verified with the available build/smoke checks.
