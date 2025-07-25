# Complete Slash Commands Reference Guide

## Understanding Slash Commands: The Foundation

Think of slash commands as your personal command palette for Claude Code. Just as modern code editors have command palettes that let you quickly access functionality without navigating through menus, slash commands provide instant access to both built-in Claude Code features and custom workflows you define yourself.

The beauty of slash commands lies in their dual nature. They serve as both immediate shortcuts for common tasks and as a framework for encoding complex, reusable workflows. When you type a slash command, you're essentially telling Claude Code to execute a predefined sequence of actions or apply a specific context to your request.

What makes slash commands particularly powerful is their ability to bridge the gap between simple text-based interactions and complex, multi-step development workflows. They can gather system information, reference multiple files, execute shell commands, and apply specialized prompting all in a single, memorable command.

## The Built-in Command Foundation

Before diving into custom commands, understanding the built-in slash commands helps you grasp the full scope of what's possible. These commands handle essential session management and provide templates for how commands should behave.

### Session Management Commands

The session management commands control the flow and state of your Claude Code interactions. Understanding when and why to use these commands helps you maintain productive development sessions.

The `/clear` command provides a fresh start by removing conversation history while preserving your memory files and configuration. This proves valuable when you've been working on one problem and want to switch contexts without the previous discussion influencing new responses. Think of it as starting a new chapter in your development session while keeping your established preferences and project knowledge intact.

The `/compact` command offers a more nuanced approach to context management. Rather than clearing everything, it compresses your conversation history while preserving essential context. You can even provide focus instructions that guide what aspects of the conversation should be emphasized during compaction. This command becomes particularly valuable during long development sessions where you want to maintain continuity while reducing the cognitive load of extensive conversation history.

### Configuration and Development Commands

The configuration commands provide access to Claude Code's settings and development tools without leaving your development flow. The `/config` command opens your configuration for review and modification, while `/model` allows you to switch between different AI models based on your current needs.

The `/memory` command deserves special attention because it demonstrates how slash commands can provide intuitive access to complex functionality. Rather than manually navigating to memory files and opening them in editors, `/memory` provides an interactive interface for managing your CLAUDE.md files directly within your development session.

### Information and Diagnostic Commands

Commands like `/cost` and `/doctor` provide transparency into Claude Code's operation. The `/cost` command helps you understand token usage patterns, which becomes valuable for managing API costs and understanding which types of interactions are most resource-intensive. The `/doctor` command performs health checks on your Claude Code installation, helping diagnose issues before they impact your workflow.

## Custom Slash Commands: Your Personal Automation Framework

Custom slash commands transform Claude Code from a general-purpose AI assistant into a specialized development partner that understands your specific workflows and conventions. These commands are essentially templated prompts stored as Markdown files that Claude Code can execute on demand.

### Understanding Command Scopes

Custom commands operate within two distinct scopes that reflect different aspects of your development environment. Understanding these scopes helps you organize commands effectively and ensures they're available in the right contexts.

**Project Commands** live within your repository at `.claude/commands/` and represent workflows, conventions, and knowledge that should be shared across your team. These commands become part of your project's development infrastructure, evolving alongside your codebase and ensuring consistent practices across team members.

When you create project commands, you're essentially encoding your team's collective knowledge about how to work effectively within that specific project. A project command might encapsulate your code review checklist, your deployment verification steps, or your debugging approach for a particular service.

**User Commands** reside in your home directory at `~/.claude/commands/` and represent your personal development practices that apply across all projects. These commands reflect your individual workflow preferences, personal debugging techniques, or analysis approaches that you want to use consistently regardless of which project you're working on.

The distinction between project and user commands encourages you to think carefully about whether a particular workflow represents team knowledge that should be shared or personal preferences that should remain individual.

### Command File Structure and Anatomy

Every custom command starts as a Markdown file with a specific structure that Claude Code understands. The filename determines the command name, while the file content defines what Claude should do when the command is executed.

The most basic command consists simply of a Markdown file containing the prompt or instructions you want Claude to execute. For example, a file named `code-review.md` creates a `/project:code-review` command that executes whatever instructions are written in that file.

However, commands become much more powerful when you add YAML frontmatter that provides metadata and configuration options. The frontmatter sits at the top of your Markdown file and controls aspects like tool access, command descriptions, and argument handling.

```markdown
---
description: Perform comprehensive code review focusing on security and performance
allowed-tools: Bash(git log:*), Bash(git diff:*)
argument-hint: [branch-name] | [file-path]
---

# Code Review Protocol

Review the specified code changes with emphasis on:
- Security vulnerabilities and best practices
- Performance implications and optimization opportunities
- Code maintainability and readability
- Adherence to project conventions

## Analysis Steps
1. Examine the change scope and impact
2. Review for security considerations
3. Assess performance implications
4. Check for consistency with project standards
```

This structure separates the command's metadata from its functional content, making commands both machine-readable for Claude Code's execution and human-readable for team members who need to understand or modify the commands.

## Advanced Command Features: Building Intelligent Workflows

The real power of slash commands emerges when you understand their advanced features. These capabilities transform simple text templates into sophisticated workflows that can gather context, execute system commands, and create rich, informed prompts for Claude.

### Namespacing: Organizing Complex Command Libraries

As your command library grows, namespacing becomes essential for maintaining organization and preventing conflicts. Namespacing in slash commands works through directory structure, creating logical groupings that make commands easier to find and use.

When you organize commands in subdirectories, the directory path becomes part of the command name. A file at `.claude/commands/frontend/component.md` creates the command `/project:frontend:component`, while `.claude/commands/backend/api.md` creates `/project:backend:api`. This hierarchical naming system allows you to group related commands while avoiding name conflicts.

Consider how you might organize commands for a full-stack application. Your frontend directory might contain commands for component generation, styling review, and bundle analysis. Your backend directory might include commands for API testing, database migration review, and performance profiling. Each namespace groups related functionality while maintaining clear boundaries between different domains of your application.

The namespacing system also supports conflicts between user and project commands in a sensible way. If you have both a user-level command at `~/.claude/commands/test.md` and a project-level command at `.claude/commands/frontend/test.md`, they coexist as `/user:test` and `/project:frontend:test` respectively. This allows you to maintain personal testing workflows while also supporting project-specific testing commands.

### Arguments: Making Commands Dynamic and Reusable

Arguments transform static command templates into dynamic workflows that can adapt to different contexts and inputs. The `$ARGUMENTS` placeholder within your command files gets replaced with whatever arguments you provide when executing the command.

Understanding how to design effective argument systems requires thinking about the different ways you might want to use a command. A simple example might involve a bug fix command that accepts an issue number:

```markdown
---
description: Fix GitHub issue following our debugging protocol
argument-hint: <issue-number>
---

# Bug Fix Protocol for Issue #$ARGUMENTS

## Investigation Steps
1. Reproduce the issue described in #$ARGUMENTS
2. Identify the root cause using our debugging checklist
3. Develop a minimal fix that addresses the core problem
4. Test the fix against edge cases mentioned in #$ARGUMENTS
5. Update any related documentation or tests

Please start by examining issue #$ARGUMENTS and walking through our standard debugging process.
```

When you execute `/project:fix-issue 123`, Claude receives a prompt that specifically references issue #123 throughout the instructions. This creates consistency in how you approach similar problems while allowing each execution to focus on the specific context you're working with.

More sophisticated argument handling might involve multiple parameters or optional arguments. While slash commands don't support complex argument parsing like traditional command-line tools, you can design commands that expect structured input and provide clear guidance about expected formats.

### Bash Command Execution: Bridging AI and System Context

One of the most powerful features of slash commands is their ability to execute bash commands and include the output as context for Claude's response. This capability transforms slash commands from simple text templates into intelligent workflows that can gather current system state and provide Claude with real-time information about your development environment.

The bash execution feature uses the `!` prefix within your command files to mark shell commands that should be executed before Claude processes the prompt. The output from these commands becomes part of the context that Claude receives, allowing it to make informed decisions based on current system state rather than assumptions or outdated information.

Understanding when and how to use bash execution requires careful consideration of security and performance implications. The `allowed-tools` frontmatter field provides granular control over which bash commands a particular slash command can execute. This security model ensures that commands can only perform the specific system operations they actually need.

Consider a git workflow command that needs to understand the current repository state:

```markdown
---
description: Create intelligent git commit based on current changes
allowed-tools: Bash(git status:*), Bash(git diff:*), Bash(git log:*)
---

# Intelligent Git Commit

## Current Repository State

**Git Status:**
!`git status --porcelain`

**Staged Changes:**
!`git diff --cached`

**Unstaged Changes:**
!`git diff`

**Recent Commit History:**
!`git log --oneline -5`

**Current Branch:**
!`git branch --show-current`

## Your Task

Based on the repository state shown above, create an appropriate git commit. Consider:
- The scope and nature of the changes
- Our commit message conventions
- Whether the changes represent a logical unit of work
- Any potential impact on other team members

If the changes are too broad or unclear, suggest breaking them into multiple commits.
```

When this command executes, Claude receives not just the prompt template but also the actual current state of your git repository. This allows Claude to provide specific, contextual advice about commit strategy rather than generic guidance about git workflows.

The bash execution capability works particularly well for commands that need to understand project structure, current system state, or the results of previous operations. However, it's important to use this feature judiciously, as executing many shell commands can slow down command execution and potentially expose sensitive information if not properly controlled.

### File References: Including Project Context

File references allow slash commands to include the contents of specific files as context for Claude's response. Using the `@` prefix, you can reference individual files or even multiple files to provide Claude with specific code or documentation context.

The file reference system integrates seamlessly with Claude Code's existing file handling capabilities, supporting the same syntax and patterns you use in regular conversations. This consistency means you can reference specific files, directories, or even patterns of files within your slash commands.

File references prove particularly valuable for commands that need to understand existing code structure or compare different implementations. Consider a refactoring command that needs to understand both the current implementation and the target architecture:

```markdown
---
description: Refactor component following our new architecture patterns
argument-hint: <component-path>
---

# Component Refactoring Analysis

## Current Implementation
@$ARGUMENTS

## Target Architecture Pattern
@docs/architecture/component-patterns.md

## Related Components for Reference
@src/components/examples/

## Refactoring Task

Based on the current implementation and our target architecture pattern, provide a step-by-step refactoring plan that:

1. Identifies specific areas that need to change
2. Suggests the order of changes to minimize breakage
3. Highlights any potential compatibility issues
4. Recommends testing strategies for validating the refactoring

Focus on maintaining backward compatibility while moving toward our standardized patterns.
```

This command combines argument handling with file references to create a focused refactoring workflow. When you execute `/project:refactor src/components/UserProfile.js`, Claude receives the current component code, the architecture documentation, and examples of properly structured components, allowing it to provide specific, informed refactoring guidance.

File references also work well for commands that need to understand configuration files, documentation, or test cases. By including relevant files as context, you ensure that Claude's responses are grounded in your actual codebase rather than general assumptions about how code should be structured.

### Thinking Mode: Enabling Deep Analysis

Slash commands can trigger Claude's extended thinking mode by including specific keywords that signal when deeper analysis would be beneficial. Extended thinking mode encourages Claude to work through complex problems step-by-step, showing its reasoning process and considering multiple approaches before providing recommendations.

The thinking mode integration works by including keywords or phrases within your command prompts that indicate when extended analysis would be appropriate. These might include phrases like "think through this carefully," "consider multiple approaches," or "analyze step-by-step."

Consider a architectural decision command that benefits from extended thinking:

```markdown
---
description: Analyze complex architectural decisions with thorough reasoning
argument-hint: <decision-topic>
---

# Architectural Decision Analysis: $ARGUMENTS

## Current Context
@docs/architecture/current-state.md
@docs/requirements/$ARGUMENTS.md

## Analysis Request

Think through this architectural decision carefully, considering multiple approaches and their trade-offs. Please:

1. **Analyze the problem space thoroughly** - What are we really trying to solve?
2. **Consider multiple solution approaches** - What are the different ways we could address this?
3. **Evaluate trade-offs systematically** - What are the pros and cons of each approach?
4. **Consider long-term implications** - How will each choice affect future development?
5. **Make a reasoned recommendation** - Which approach best fits our constraints and goals?

Take your time to work through this systematically, showing your reasoning process throughout.
```

Commands designed for extended thinking work particularly well for complex decisions that benefit from structured analysis. The thinking mode helps ensure that important architectural or design decisions receive appropriate consideration rather than quick, potentially superficial responses.

## MCP Slash Commands: Extending Your Command Arsenal

MCP (Model Context Protocol) slash commands represent a sophisticated extension system that allows external tools and services to expose their functionality as slash commands within Claude Code. These commands bridge Claude Code with external systems, creating seamless workflows that span multiple tools and platforms.

### Understanding MCP Command Structure

MCP commands follow a specific naming pattern that reflects their external origin: `/mcp__<server-name>__<prompt-name>`. This naming convention clearly identifies MCP commands while avoiding conflicts with your custom commands.

The double underscore separators and the `mcp` prefix create a distinct namespace for these dynamically-discovered commands. When an MCP server connects to Claude Code and exposes prompts, those prompts automatically become available as slash commands without requiring any manual configuration.

For example, if you have a GitHub MCP server connected, you might see commands like `/mcp__github__list_prs` for listing pull requests or `/mcp__github__pr_review` for conducting pull request reviews. These commands leverage the MCP server's integration with GitHub's API while presenting a familiar slash command interface.

### MCP Command Discovery and Usage

MCP commands are discovered dynamically when MCP servers connect to Claude Code. This means your available MCP commands can change based on which external services are configured and accessible. The dynamic discovery process happens automatically, so new MCP servers immediately extend your command capabilities without requiring restarts or manual configuration.

MCP commands can accept arguments just like custom commands, but the argument structure depends on what the underlying MCP server expects. Some MCP commands work without arguments, while others require specific parameters to function properly.

The argument handling for MCP commands often reflects the underlying API or service requirements. A JIRA MCP server might expose commands like `/mcp__jira__create_issue` that expect specific arguments for issue title and priority, while a database MCP server might expose query commands that accept SQL as arguments.

Understanding how to effectively use MCP commands requires familiarity with the underlying services they represent. While the slash command interface provides convenience and consistency, you still need to understand what each external service can do and how to provide appropriate arguments for the operations you want to perform.

## Advanced Command Patterns and Best Practices

As you develop expertise with slash commands, certain patterns and practices emerge that make commands more effective, maintainable, and useful for your team.

### Designing Commands for Team Collaboration

When creating project-level commands that your team will use, consider how to make them self-documenting and easy to understand. Include clear descriptions in the frontmatter, provide helpful argument hints, and structure the command content to explain not just what should be done but why.

Effective team commands often include sections that explain the reasoning behind particular approaches or reference relevant documentation. This educational aspect helps team members understand not just the mechanics of using the command but the principles it's designed to enforce.

Consider including examples within your command files that show how the command should be used in different contexts. These examples serve as both documentation and templates that team members can adapt for their specific situations.

### Combining Multiple Advanced Features

The most powerful slash commands often combine multiple advanced features to create sophisticated workflows. A command might use bash execution to gather system state, file references to include relevant code context, arguments to customize behavior, and thinking mode keywords to ensure thorough analysis.

When combining features, consider the order of operations and how different elements interact. Bash commands execute first, then file references are resolved, and finally the complete prompt (including command output and file contents) is presented to Claude with any argument substitutions applied.

This execution order allows you to create commands that gather dynamic context and then use that context to inform more sophisticated analysis. For example, you might have a deployment readiness command that checks current system state, references configuration files, and then analyzes whether the system is ready for deployment based on both current conditions and configuration requirements.

### Performance and Security Considerations

As commands become more sophisticated, consider their performance implications. Commands that execute many bash operations or reference large files can take longer to execute and consume more resources. Design commands to gather only the information actually needed for the task at hand.

Security considerations become particularly important with bash execution capabilities. Always use the most restrictive `allowed-tools` configuration that still enables your command to function properly. Avoid granting broad bash access when specific, limited commands would suffice.

Consider the information exposure implications of your commands, especially those that might be shared with team members. Commands that gather system information or include file contents can potentially expose sensitive data, so design them with appropriate boundaries and considerations for what information should be included in command output.

## Troubleshooting Common Command Issues

Understanding how to diagnose and resolve common command problems helps you maintain an effective command library and debug issues when they arise.

### Command Discovery Problems

When commands don't appear or aren't recognized, start by verifying the file structure and naming conventions. Commands must be in the correct directories (`.claude/commands/` for project commands, `~/.claude/commands/` for user commands) and must have `.md` extensions.

Check that your YAML frontmatter is properly formatted if you're using it. Malformed YAML can prevent commands from loading correctly. Test your frontmatter syntax using a YAML validator if you're unsure about formatting.

Verify that Claude Code is starting from the directory you expect. Project commands are only available when Claude Code can find the `.claude/commands/` directory, which requires starting Claude Code from within the project or a subdirectory.

### Argument and Substitution Issues

When argument substitution isn't working as expected, verify that you're using the correct `$ARGUMENTS` placeholder syntax and that you're providing arguments in the expected format when executing the command.

Remember that the entire argument string gets substituted as a single unit. If you need more sophisticated argument parsing, consider designing your commands to accept structured input or using bash execution to parse and validate arguments before proceeding with the main command logic.

### Bash Execution and Permission Problems

Bash execution issues often relate to the `allowed-tools` configuration in your command frontmatter. Verify that you've granted the specific bash commands your command needs to execute. The `allowed-tools` field requires explicit permission for each command pattern you want to use.

Check that the bash commands you're trying to execute actually work in your environment. Test them manually before including them in slash commands to ensure they produce the expected output and don't require interactive input.

### File Reference Resolution Issues

File reference problems typically stem from incorrect paths or files that don't exist when the command executes. Remember that file paths in commands are resolved relative to Claude Code's current working directory, which may not always be what you expect.

Test file references with simple, known files before using them in complex commands. This helps you verify that the path resolution is working correctly and that Claude Code can access the files you're trying to reference.

## Building Your Command Library Strategy

Developing an effective slash command library requires thinking strategically about which workflows to automate and how to organize commands for maximum utility and maintainability.

### Starting Simple and Growing Complexity

Begin with simple commands that automate frequently-used prompts or encode basic team conventions. As you gain experience with the command system, gradually add more sophisticated features like bash execution and file references.

Focus initially on commands that provide immediate value by reducing repetitive typing or ensuring consistent approaches to common tasks. These early wins help establish the value of the command system and provide foundation patterns you can extend.

### Identifying Command Opportunities

Look for patterns in your development workflow where you find yourself providing similar context or asking similar questions repeatedly. These repetitive patterns often represent good opportunities for command automation.

Pay attention to workflows that require gathering multiple pieces of context before providing instructions to Claude. These complex setup processes often benefit significantly from command automation that can gather all necessary context automatically.

### Evolving Commands Over Time

Treat your command library as living infrastructure that evolves alongside your project and development practices. Regular review and refinement help ensure commands remain useful and accurate as your codebase and workflows change.

Consider establishing team processes for command maintenance, including reviews of command effectiveness and updates when project conventions change. This collaborative approach helps ensure that your command library continues to provide value and remains aligned with current practices.

The most effective command libraries balance comprehensive coverage of important workflows with maintainability and ease of use. Focus on creating commands that genuinely improve your development experience rather than automating every possible task, and you'll build a command system that becomes an integral part of your productive development workflow.