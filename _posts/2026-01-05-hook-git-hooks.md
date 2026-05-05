---
title: "Introducing hook - Git Hooks Made Easy"
date: 2026-01-05
categories:
  - developer-tools
  - cli
  - productivity
tags:
  - git-hooks
  - security
  - developer-productivity
excerpt: "Block secrets, enforce conventions, and automate checks with simple git hooks. No more secrets leaked to GitHub."
---

# Introducing hook - Git Hooks Made Easy

Every developer has horror stories about accidentally committing secrets to GitHub. One `.env` file, one API key, and suddenly your credentials are public.

We've built **hook** to solve this problem.

## Why Git Hooks Matter

Git hooks run before every commit. They're your last line of defense against:
- API keys and tokens being committed
- `.env` files getting pushed
- Bad commit messages
- Wrong branch pushes

## Installation

```bash
npm install -g @fullsparklabs/hook
```

## Usage

### Block Secrets

```bash
hook install no-api-keys pre-commit
```

Blocks common API keys, tokens, and secrets from being committed.

### Block .env Files

```bash
hook install no-env pre-commit
```

Prevents any `.env` file from being committed.

### Require JIRA Tickets

```bash
hook install check-jira commit-msg
```

Enforces JIRA ticket format in commit messages (e.g., `PROJ-123: Fix bug`).

### List Available Hooks

```bash
hook list
```

Shows all available hook templates.

## Templates Included

- `no-api-keys` - Block API keys, tokens, AWS keys
- `no-env` - Block .env files
- `check-jira` - Require JIRA ticket format
- `check-branch` - Enforce branch naming

## Get Started

```bash
npm install -g @fullsparklabs/hook
hook install no-api-keys pre-commit
```

**[View on GitHub →](https://github.com/Fullspark-Labs/hook)**

*Built with ❤️ by Fullspark Labs*