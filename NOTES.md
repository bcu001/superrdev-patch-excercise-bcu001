# Patch Notes

## Summary of changes

Fixed two issues in the task filtering flow.

1. Fixed the SQL status-filtering bug in `TaskRepository.java`. The original query did not group the title and description search conditions, so SQL operator precedence caused the status filter to be applied incorrectly in some search cases.

2. Fixed the frontend pagination state when the status filter changes. The page is now reset to page 1 when the status changes, preventing an invalid/empty page from being requested after filtering.

## What I chose not to change

I did not modify the Oracle PL/SQL reference artifact because it is explicitly described as a non-running reference implementation for this exercise.

I also did not add search debouncing or change invalid-status handling. These are potential improvements, but they were not necessary to fix the demonstrated behavior and I wanted to keep the patch focused within the timebox.

## Biggest remaining risk

`TaskController.java` at line 30, I noticed that TaskStatus.valueOf() can throw an exception for an invalid status supplied directly to the API. I chose not to change it because the current frontend only sends valid enum values, and I prioritized the demonstrated SQL correctness issue and pagination behavior within the timebox

## Tools / AI used

I used ChatGPT to review the frontend, backend, and SQL, trace the status-filter request flow, identify the SQL operator-precedence issue, and reason about the pagination behavior. I verified the suggestions against the existing code and applied only the changes relevant to the exercise.