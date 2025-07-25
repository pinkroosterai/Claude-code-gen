---
description: [Brief description of what this command does]
allowed-tools: [Comma-separated list of allowed bash commands with patterns]
argument-hint: [Expected argument format, e.g., <file-path> or <issue-number>]
---

# [Command Title]

## Context Gathering
[Use bash commands to gather current state]

### Current State
!`[bash command to check current state]`

### Relevant History
!`[bash command to get historical context]`

### Configuration
!`[bash command to check configuration]`

## File Context
[Reference relevant files]
@[path/to/relevant/file.ext]
@[path/to/config/file.json]

## Agent Use
[Instructions and guidance on agent use]

## Analysis Request

[Main instruction for Claude, can use $ARGUMENTS placeholder]

### Objectives
1. [First objective]
2. [Second objective]
3. [Third objective]

### Constraints
- [Constraint 1]
- [Constraint 2]
- [Constraint 3]

### Expected Output
[Describe the format and content of expected response]

## Additional Considerations
[Any extra context or requirements]
[References to team standards or documentation]
