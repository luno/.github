---
applyTo: "**/go.mod"
---

# Go Version Management Instructions

## Go Version Updates
- Always update to the latest patch version within a major.minor release
- Preserve exact formatting and spacing in go.mod files
- Ensure go.mod files end with a newline character
- Only modify the `go` directive line, leave all other content unchanged

## Commit Messages
- Use the format: `gomod: Update Go version to X.Y.Z`
- Keep commit messages concise and descriptive

## PR Guidelines
- Use descriptive titles that indicate the version change
- Include rationale for the update in PR descriptions
- Add label `AI::Created` for automated PRs
- Reference the specific Go version being updated to and from
