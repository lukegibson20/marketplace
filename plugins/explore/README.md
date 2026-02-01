# Explore Plugin

Helps Claude read planning documents and explore related files to get familiar with a codebase topic before writing code.

## Overview

The Explore plugin is part of the **Explore → Plan → Execute** workflow pattern. It guides Claude to thoroughly understand a codebase area before making changes, reducing errors and improving code quality.

## Usage

```bash
/explore:explore [optional: specific area to explore]
```

### What It Does

1. Reads `claude-checklists/DESCRIPTION-OF-THIS-AREA-OF-YOUR-SYSTEM.md`
2. Reads `claude-checklists/CURRENT-PROJECT.md`
3. Explores related code files and tests
4. Prepares Claude to discuss the codebase (without writing code yet)

### Example

```bash
/explore:explore authentication system
```

Claude will read planning documents and explore auth-related files to understand the current implementation before any changes are made.

## Setup

Create the checklist directory and files in your project:

```bash
mkdir -p claude-checklists
```

### DESCRIPTION-OF-THIS-AREA-OF-YOUR-SYSTEM.md

Describes the area of code you're working on:

```markdown
# Authentication System

This area handles user authentication including:
- Login/logout flows
- OAuth providers (Google, Apple, GitHub)
- Session management and token refresh
- Password reset functionality

## Key Files
- `src/auth/auth_service.dart`
- `src/auth/providers/`
- `src/auth/models/`

## Architecture
[Describe how components interact]

## Known Issues
[List any technical debt or quirks]
```

### CURRENT-PROJECT.md

Describes what you're currently working on:

```markdown
# Current Project: Add Biometric Login

## Goal
Add fingerprint/Face ID authentication as a secondary auth option.

## Related Files
- `src/auth/biometric_auth.dart` (to create)
- `src/auth/auth_service.dart` (to modify)
- `src/settings/security_settings.dart` (to modify)

## Acceptance Criteria
- [ ] Users can enable biometric login in settings
- [ ] Biometric prompt appears on app launch when enabled
- [ ] Fallback to password if biometric fails 3 times
- [ ] Works on both iOS (Face ID/Touch ID) and Android

## Design Decisions
[Document key decisions and trade-offs]
```

## Workflow Integration

### Recommended Workflow

1. **Explore** (this plugin) - Familiarize with the codebase
2. **Plan** - Design the implementation approach
3. **Execute** - Write the actual code

### When to Use

- **Starting a new feature**: Understand existing patterns first
- **Fixing a bug**: Explore related code before making changes
- **Onboarding to a codebase**: Get familiar with an area
- **Before major refactoring**: Understand dependencies and impacts

### Pro Tips

- **Be specific**: Add arguments to focus exploration on a specific area
- **Update checklists**: Keep CURRENT-PROJECT.md updated as work progresses
- **Use with Plan**: After exploration, use `/plan` to design your approach
- **Prepare for discussions**: "Prepare to discuss" works better than "prepare to implement"

## Installation

This plugin is included in the [Awesome Claude Code Plugins](https://github.com/ccplugins/marketplace) marketplace.

```bash
/plugins
# Search for "explore"
# Install
```

## Troubleshooting

### Checklist Files Not Found

**Issue**: Claude reports missing checklist files

**Solution**: Create the `claude-checklists/` directory with the required files:
```bash
mkdir -p claude-checklists
touch claude-checklists/DESCRIPTION-OF-THIS-AREA-OF-YOUR-SYSTEM.md
touch claude-checklists/CURRENT-PROJECT.md
```

### Not Enough Context

**Issue**: Exploration feels shallow

**Solution**: Add more detail to your checklist files, especially the "Key Files" section in DESCRIPTION-OF-THIS-AREA-OF-YOUR-SYSTEM.md

## Contributing

Found issues or have suggestions? Open an issue at:
https://github.com/ccplugins/marketplace/issues

## License

Apache 2.0 (inherited from marketplace root)

## Author

Galen Ward

---

**Quick Start**: Create `claude-checklists/` directory, add your planning docs, then run `/explore:explore`!
