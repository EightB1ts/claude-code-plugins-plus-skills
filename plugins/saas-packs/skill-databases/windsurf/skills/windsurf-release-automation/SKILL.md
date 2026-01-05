---
name: "windsurf-release-automation"
description: |
  Execute automate release processes with semantic versioning. Activate when users mention
  "release automation", "version bump", "changelog generation", "semantic release",
  or "publish release". Handles release engineering automation. Use when working with windsurf release automation functionality. Trigger with phrases like "windsurf release automation", "windsurf automation", "windsurf".
allowed-tools: "Read,Write,Edit,Bash(cmd:*)"
version: 1.0.0
license: MIT
author: "Jeremy Longshore <jeremy@intentsolutions.io>"
---

# Windsurf Release Automation

Automate release processes with semantic versioning and changelog generation.

## Overview

This skill enables automated release workflows within Windsurf using Cascade AI. It analyzes commits to determine semantic version bumps, generates comprehensive changelogs, manages Git tags, and publishes releases. Cascade understands conventional commits to automatically categorize changes and highlight breaking changes for proper version increments.

## Prerequisites

- Windsurf IDE with Cascade enabled
- Git repository with commit history
- Conventional commits or consistent commit format
- npm/yarn/pnpm for JavaScript projects (or equivalent)
- CI/CD pipeline for automated publishing (optional)

## Directory Structure

```
project-root/
    CHANGELOG.md                     # Release history
        # Version entries
        # Change categories
        # Breaking changes
        # Contributors

    package.json                     # Version source
        # Current version
        # Release scripts
        # Publish configuration

    .releaserc.js                    # Semantic release config
        # Branch configuration
        # Plugin settings
        # Commit analysis rules

    .windsurf/
        release/
            templates/
                changelog-entry.md       # Changelog template
                    # Version header format
                    # Category sections
                    # Link formatting

                release-notes.md         # Release notes template
                    # Summary section
                    # Highlights
                    # Migration guide

            config/
                version-rules.json       # Version bump rules
                    # Commit type to version mapping
                    # Breaking change detection
                    # Pre-release handling

                publish-config.json      # Publishing settings
                    # Registry configuration
                    # Artifact definitions
                    # Distribution channels

            history/
                releases.json            # Release history log
                    # Version and dates
                    # Commit ranges
                    # Artifact links
```

## Release Features

### Version Management
- Semantic version calculation
- Pre-release tagging
- Version consistency checks
- Git tag management

### Changelog Generation
- Commit analysis
- Category grouping
- Breaking change highlighting
- Contributor attribution

## Instructions

1. **Configure Version Strategy**
   - Define commit type to version mapping
   - Set branch policies for releases
   - Configure pre-release handling (alpha, beta, rc)

2. **Set Up Automation**
   - Install semantic-release or equivalent
   - Configure CI/CD integration
   - Set up publishing credentials

3. **Prepare Release**
   - Review commits since last release
   - Cascade analyzes and suggests version bump
   - Generate changelog preview

4. **Execute Release**
   - Trigger release workflow
   - Review generated changelog
   - Verify published artifacts

5. **Post-Release Tasks**
   - Merge release branch if applicable
   - Announce release to stakeholders
   - Monitor for post-release issues

## Output

- Updated version in package.json
- Generated CHANGELOG.md entry
- Git tag for release version
- Published package to registry
- Release notes for distribution

## Error Handling

| Error | Cause | Solution |
|-------|-------|----------|
| Version calculation failed | No conventional commits | Add feat/fix prefixes to commits |
| Changelog generation empty | No changes since last release | Verify commit range, check for tags |
| Publish failed | Auth or permission issue | Check registry credentials |
| Tag already exists | Duplicate version | Delete tag and bump version |
| Breaking change missed | Commit not marked | Add BREAKING CHANGE footer |

## Examples

**Example: Determine Version Bump**
Request: "What version should this release be?"
Result: Cascade analyzes commits, recommends minor bump (1.2.0 -> 1.3.0) based on feat commits

**Example: Generate Changelog**
Request: "Generate changelog for upcoming release"
Result: Formatted changelog with features, fixes, breaking changes, and contributors

**Example: Execute Full Release**
Request: "Release version 2.0.0 with changelog"
Result: Version bumped, changelog generated, tag created, package published

## Resources

- [Windsurf Release Automation](https://docs.windsurf.ai/features/release)
- [Semantic Release Documentation](https://semantic-release.gitbook.io/)
- [Conventional Commits](https://www.conventionalcommits.org/)

## Success Criteria

- Correct semantic version tagging
- Comprehensive changelogs
- 50% reduction in release cycle time
