---
title: "hook - Git Hooks Without the Headache"
date: 2026-01-05
image: https://avatars.githubusercontent.com/u/281868970?v=4
categories:
  - developer-tools
  - cli
tags:
  - git-hooks
  - security
  - developer-productivity
excerpt: "Block secrets before they hit GitHub. Enforce conventions. Run checks. All with one command."
---

Git hooks are powerful but underused. Most developers don't bother because writing and managing them is a pain.

**hook** makes it easy.

## Installation

```bash
npm install -g @fullsparklabs/hook
```

## One Command to Start

```bash
hook install no-api-keys
```

That's it. Now commits containing API keys, tokens, or secrets will be blocked.

## Built-in Templates

### Security

```bash
# Block API keys, tokens, secrets
hook install no-api-keys

# Block .env files
hook install no-env

# Block .pem, .key files
hook install no-secrets

# Block node_modules
hook install no-node-modules

# Block files >100KB
hook install no-large-files
```

### Code Quality

```bash
# Block debugger statements
hook install no-debugger

# Prefer pnpm/yarn over npm
hook install no-package-lock
```

### Conventions

```bash
# Require JIRA tickets: PROJ-123
hook install check-jira commit-msg

# Enforce branch naming: feat/, fix/, chore/
hook install check-branch

# Require emoji in commits
hook install require-emoji

# Block merge commits
hook install check-merge-commit
```

## Usage

### List Templates

```bash
hook list
```

### Install to Specific Hook

```bash
# Install to commit-msg hook
hook install check-jira commit-msg

# Install to pre-push hook
hook install check-jira pre-push
```

### Create Custom Template

```bash
hook create mycheck '#!/bin/bash
if [ -f "BREAKING.txt" ]; then
  echo "❌ Cannot commit BREAKING.txt"
  exit 1
fi
exit 0'
```

### Remove Hook

```bash
hook remove pre-commit
```

## How It Works

```
.git/hooks/
├── pre-commit     ← hook install no-api-keys
├── commit-msg    ← hook install check-jira
└── pre-push
```

Each hook runs automatically on the corresponding git action.

## Real Example

```bash
$ hook install no-api-keys
✅ Installed: no-api-keys → .git/hooks/pre-commit

$ git add src/config.js
$ git commit -m "add config"
🔍 Checking for secrets...
❌ Blocked: src/config.js contains potential secret (API key, token, etc.)

💡 To allow this file, move secrets to environment variables
```

## Sharing with Team

Since hooks go in `.git/hooks/` (not git-tracked), you have options:

**Option 1**: Use [lefthook](https://github.com/arkark/lefthook) - Git-aware hooks

**Option 2**: Commit hooks directory

```bash
mkdir -p .githooks
cp .git/hooks/* .githooks/
git add .githooks
git commit -m "add hooks"
```

**Option 3**: Use Husky

```bash
npx husky add .husky/pre-commit "hook run no-api-keys"
```

## Why hook?

- **Zero config** - Works out of the box
- **Safe defaults** - Blocks secrets, not code
- **Cross-platform** - Works on macOS, Linux, Windows
- **Customizable** - Create your own templates

## Get Started

```bash
npm install -g @fullsparklabs/hook
hook install no-api-keys
hook install no-env
```

**[Full Documentation →](https://github.com/Fullspark-Labs/hook)**

*Built with ❤️ by Fullspark Labs*