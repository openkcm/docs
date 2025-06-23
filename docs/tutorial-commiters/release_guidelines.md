# 📦 Release Workflow Guidelines

## 🌟 Objective

Automate project releases through Pull Requests (PRs) using specific labels and enforce [Conventional Commits](https://www.conventionalcommits.org/) to standardize changelog generation and semantic versioning.

---

## 🧪 Overview

This release system is:

- Triggered on **PR merge**
- Controlled using **PR labels**
- Based on **Semantic Versioning**
- Powered by **Conventional Commits** for changelog generation and version bump logic

---

## 🏷️️ Label-Driven Release Rules

### ✅ Required Label

To trigger a release, add the following label to your Pull Request:

- `release`

Without this label, the PR **will not** generate a version bump or release tag.

### 🔹 Optional Version Bump Labels

| Label    | Action                        | Example (`v1.2.3` → …) |
| -------- | ----------------------------- | ---------------------- |
| `major`  | Increments **major** version  | `v2.0.0`               |
| `minor`  | Increments **minor** version  | `v1.3.0`               |
| *(none)* | Defaults to **patch** version | `v1.2.4`               |

If no `major` or `minor` label is present, a **patch bump** is assumed by default.

---

## 🧶 Version Calculation

- Determines the current version from the **latest Git tag** (e.g., `v1.4.2`)
- Applies label-driven version bump
- Creates and pushes a new Git tag (e.g., `v1.5.0`)
- Optionally updates changelog and GitHub release

---

## 📜 Conventional Commits (Required)

To support automatic changelog generation and semantic versioning, all commits and PR titles must follow the [Conventional Commits](https://www.conventionalcommits.org/) specification.

### ✅ Format

```
<type>[optional scope]: <short description>
```

### 💡 Examples

```
feat: add login functionality
fix(auth): handle expired token
chore(deps): update eslint to v8
refactor(ui): simplify button component
```

### 💥 Breaking Changes

Use `!` in the type or a `BREAKING CHANGE:` footer:

```
feat!: remove deprecated auth flow

BREAKING CHANGE: auth headers must now include `x-access-token`
```

---

## ✅ PR Workflow Summary

1. **Create a PR** with a Conventional Commit-style **title**
2. **Add labels**:
   - `release` ✅
   - `major` or `minor` (optional)
3. **Merge the PR** into the main branch
4. 🎉 Automation will:
   - Determine version from the latest tag
   - Bump version based on labels
   - Create a Git tag (`vX.Y.Z`)
   - Generate release notes or changelog (optional)

---

## ✅ Best Practices

### 🪄 1. Keep Commits Clean and Purposeful

- Use one commit per logical change
- Avoid noisy commits like `fix typo` or `update stuff`
- Squash commits when appropriate

### ✍️ 2. Use Descriptive PR Titles

- PR titles must follow Conventional Commit format
- Titles are used in changelogs — make them clear and meaningful

**Good:**

```
feat(api): add rate-limiting support
```

**Bad:**

```
Update things
```

### 📌 3. Label Carefully

- Always include `release` if the PR affects production code
- Use `major` only for **breaking changes**
- Use `minor` for **new features**
- Leave both off for patch-level fixes

### 🧪 4. Test Before Merging

- Run CI and tests before merging
- Tags and releases should only be created from a clean, passing main branch

### 📚 5. Maintain a Clean Tag History

- Tags must follow `vX.Y.Z` format
- Avoid creating tags manually — let automation handle this

### 📖 6. Write Good Commit Bodies

- Explain the **why**, not just the what
- Use footers for issues and breaking changes

Example:

```
fix(config): handle null env values

Fixes #123
```

### 🔒 7. Review Labels in Code Reviews

- Double-check PR has the correct labels:
  - `release` is present
  - Only one of `major` or `minor` is used, if applicable

---

## 🧪 Optional Enhancements

- Add PR templates to guide contributors on format
- Use `commitlint` with `husky` to validate commits locally
- Use tools like `release-drafter` to preview changelogs

---

## 🛑 Summary Table

### 🚀 Release Labels

| Label     | Required? | Description            |
| --------- | --------- | ---------------------- |
| `release` | ✅         | Triggers a release     |
| `major`   | ❌         | Major version bump     |
| `minor`   | ❌         | Minor version bump     |
| *(none)*  | ❌         | Defaults to patch bump |

### 🗘️ Commit & PR Formatting

| Rule                            | Required?         | Purpose                         |
| ------------------------------- | ----------------- | ------------------------------- |
| Conventional Commit format      | ✅                 | Required for changelogs         |
| PR title as Conventional Commit | ✅                 | Affects changelog/release notes |
| `BREAKING CHANGE:` footer       | ✅ (if applicable) | Signals major version bump      |

---

