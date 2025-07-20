# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Overview

This is a Scala Steward configuration repository that manages automated dependency updates for multiple Scala projects. Scala Steward is a bot that creates pull requests to update library dependencies in Scala projects.

## Repository Structure

- `repos.md` - List of repositories to be monitored and updated by Scala Steward
- `.github/workflows/scala-steward.yml` - GitHub Actions workflow that runs Scala Steward every 4 hours
- `.github/dependabot.yml` - Configuration for Dependabot to keep GitHub Actions up to date

## Key Commands

### Adding a New Repository

1. Edit `repos.md` and add the repository in the format: `- owner/repo-name`
2. Ensure @xerial-bot user is invited as a collaborator to the target repository
3. Commit and push the changes - Scala Steward will automatically pick up the new repository on the next run

### Manually Triggering Scala Steward

The workflow can be manually triggered through GitHub Actions:
- Go to Actions tab → Scala Steward workflow → Run workflow

## Architecture

The system works as follows:

1. **GitHub Actions Workflow** (`.github/workflows/scala-steward.yml`):
   - Runs on a schedule (every 4 hours) or can be manually triggered
   - Uses the official Scala Steward GitHub Action
   - Reads repository list from `repos.md`
   - Uses a GitHub token with appropriate permissions to create PRs

2. **Repository List** (`repos.md`):
   - Simple markdown file listing all repositories to monitor
   - Each repository must have @xerial-bot as a collaborator

3. **Scala Steward Configuration**:
   - Author email: leo+bot@xerial.org
   - Automatically adds labels to created PRs
   - Uses Java 21 (Zulu distribution) and Node.js 18