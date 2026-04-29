# Contributing From a Fork

This guide explains the recommended workflow for contributing from your fork and passing local hooks.

## Why commits can fail

This repository uses Lefthook with:

- `pre-commit`: runs ESLint and TypeScript checks.
- `commit-msg`: runs commitlint (Conventional Commits format).

If your message is like `added minor changes`, commitlint rejects it.

## 1) Configure remotes once

Use your fork as `origin` and the source repository as `upstream`.

```sh
git remote -v
```

Expected:

- `origin` -> your fork URL
- `upstream` -> original source URL

If needed:

```sh
git remote rename origin old-origin
git remote add origin https://github.com/<your-user>/react-native-ui-datepicker.git
git remote add upstream https://github.com/farhoudshapouran/react-native-ui-datepicker.git
```

## 2) Keep your fork branch up to date

```sh
git fetch upstream
git checkout main
git merge upstream/main
git push origin main
```

## 3) Create a feature branch

```sh
git checkout -b feat/minor-pack-update
```

## 4) Run checks before commit

```sh
yarn lint
yarn typecheck
yarn test
```

## 5) Commit with Conventional Commits

Valid examples:

- `feat: add range calendar footer props`
- `fix: prevent month jump on timezone switch`
- `docs: update publishing notes`
- `chore: align scoped publishConfig`

Commit command:

```sh
git add .
git commit -m "chore: align scoped publishConfig"
```

## 6) Push to your fork

First push from a new branch:

```sh
git push -u origin feat/minor-pack-update
```

Then open a PR from your fork branch into upstream `main`.

## Hook troubleshooting

Run hooks manually:

```sh
npx lefthook run pre-commit
printf "chore: test commit\n" | npx commitlint
```

If commitlint fails with `type-empty` or `subject-empty`, your commit message format is invalid.

## Common pitfalls

- Committing on `main` instead of a feature branch.
- `origin` points to a shared org repo instead of your personal fork.
- Non-conventional commit messages.
- Trying to push before making a successful commit.
