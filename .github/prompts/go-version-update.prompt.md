---
mode: 'agent'
tools: ['search_repositories', 'get_pull_request', 'create_pull_request', 'update_pull_request', 'create_or_update_file', 'Codebase']
description: 'Bulk update Go version across all repositories in a GitHub organisation'
---

# Bulk Go Version Update Task

## Go Version Management Instructions

### Go Version Updates

- Always update to the latest patch version within a major.minor release.
- Preserve exact formatting and spacing in go.mod files.
- Ensure go.mod files end with a newline character.
- Only modify the `go` directive line, leave all other content unchanged.
- Often there are unit tests in .github/workflows, these will need to be updated to use the new Go version as well. By specifying `1` we are targeting the latest version, which should be the version we are setting to. We should add the latest minor version before that too. e.g. if we are updating to `1.24.3`, we should set the workflow to use `'1.23, '1'` in the version matrix.

### Commit Messages

- Use the format: `gomod: Update Go version to X.Y.Z` (e.g., `gomod: Update Go version to 1.24.3`)
- Keep commit messages concise and descriptive

### PR Guidelines

- Use descriptive titles that indicate the version change
- Include the rationale for the update in PR descriptions
- Add label `AI::Created` for automated PRs
- Reference the specific Go version being updated to and from

## Task Description

I need to update the Go version to `${input:majorMinorVersion}.${input:patchVersion}` across all repositories in the GitHub organisation `${input:organisation}`. Please help me create pull requests for all repositories that need updating.

## Requirements

- Target Organisation: `${input:organisation}`
- Target Go Version: `${input:majorMinorVersion}.${input:patchVersion}`
- Update Condition: Only update repositories where the current Go version doesn't already start with `${input:majorMinorVersion}`
- Branch Author: `${input:branchAuthor}`

## Task Steps

### 1. Discovery Phase

- Find all repositories in the `${input:organisation}` organisation that have `go.mod` files
- Check the current Go version in each `go.mod` file
- Skip archived repositories
- Identify which repositories need updating vs which are already on Go `${input:majorMinorVersion}`.x

### 2. PR Creation Phase

For each repository that needs updating, create a pull request with these specifications:

**Branch naming:** `${input:branchAuthor}-go-version-update`
**Commit message:** `gomod: Update Go version to ${input:majorMinorVersion}.${input:patchVersion}`
**PR Title:** `gomod: Update Go version to ${input:majorMinorVersion}.${input:patchVersion}`

**PR Description:**

```markdown
## Changed

- Updated `go` directive in `go.mod` from `go <current_version>` to `go ${input:majorMinorVersion}.${input:patchVersion}`

## Rationale

- Go ${input:majorMinorVersion}.${input:patchVersion} is the latest patch release of Go ${input:majorMinorVersion}
- This ensures the project can update to other libraries that declare _their_ minimum version as ${input:majorMinorVersion}
- Aligns with other ${input:organisation} repositories that are already using Go ${input:majorMinorVersion}.x
```

**Labels:** Add `AI::Created` label to each PR

**File modifications:**

- Only change the `go` directive line in `go.mod`
- Preserve all other content exactly as-is
- Ensure there's a newline at the end of the `go.mod` file

## Expected Output

Please provide:

1. **Discovery Summary:** List of all repositories found and their current Go versions
2. **Update Plan:** Which repositories need updating vs which are already compliant
3. **Execution:** Create PRs systematically, starting with the first repository as an example
4. **Final Report:** Summary of all PRs created with links and any failures

## Context Requirements

Use the #search_repositories tool to access the target organisation repositories. When processing each repository:

1. Check if the repository is archived (skip if archived)
2. Look for `go.mod` in the root directory
3. Parse the current Go version from the `go` directive
4. Compare against the target version pattern

## Error Handling

- If a repository doesn't have a `go.mod` file, log and skip
- If API rate limits are hit, implement appropriate backoff
- If a PR creation fails, log the error but continue with other repositories
- Provide a summary of any repositories that couldn't be processed

## Variables Available

- `${workspaceFolder}` - Current workspace root
- `${input:organisation}` - GitHub organisation name
- `${input:majorMinorVersion}` - Major.minor version (e.g., 1.24)
- `${input:patchVersion}` - Patch version (e.g., 3)
- `${input:branchAuthor}` - Git username for branch naming

Run this prompt in CoPilot with:

```shell
/go-version-update organisation=luno majorMinorVersion=1.24 patchVersion=3 branchAuthor=<yourName>
```
