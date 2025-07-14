# Git Commit Instructions

- Commit messages should follow the format `"<prefix>: <Capital description>"` in present tense, where:
  - The prefix follows the pattern `{directory}/{optional_subdirectory}` describing the part of the code you are changing
  - Examples: `"users: Add validation for email format"`, `"payments/processor: Fix transaction timeout"`, `"wallet/crypto: Implement new signature verification"`
  - The description starts with a capital letter and uses present tense
  - When including the directory name, the `.` at the start should be omitted (if present)
- The commit message should not be longer than 80 characters
