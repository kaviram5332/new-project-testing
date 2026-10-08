Notes and assumptions for the assessment

- Upgraded/fixed SQL operator precedence in `TaskRepository` to ensure `archived=false` applies to both title and description matches.
- Validated `status` parameter in `TaskController` to return 400 for invalid values instead of throwing an exception.
- Removed artificial Thread.sleep delay used for logging that blocked request threads.
- Added AbortController support in frontend `fetchTasks` and hook to cancel stale requests when user types quickly.
- Reset pagination to page 1 when filters (query/status) change to avoid showing empty pages.
- Guarded rendering of `task.status` in `TaskTable` to avoid runtime errors when status is missing.

Assumptions:
- API proxy is configured in `vite.config.js` to forward `/api` to Spring Boot on port 8080.
- Handwritten notes will be created in `handwritten/` before submission.
- Running `mvnw spring-boot:run` will start backend and `npm run dev` will start frontend.
