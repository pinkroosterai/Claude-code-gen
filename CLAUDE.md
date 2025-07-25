# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Repository Purpose

This is a template and documentation repository for Claude Code customization. It provides structured templates, reference documentation, and examples for creating:
- CLAUDE.md memory files
- Custom slash commands 
- Sub-agents for specialized tasks
- Project-specific Claude Code configurations

## Architecture and Structure

### Directory Organization
- `docs/` - Comprehensive reference documentation for Claude Code features
- `templates/` - Template files for various Claude Code customizations
- `commands/` - Organized slash command categories for different workflows
- `agents/` - (Not present but supported) Sub-agent configurations

### Template System
The repository uses a template-driven approach where:
- `templates/claude-template.md` - Personal development preferences template
- `templates/claude-project-template.md` - Project-specific guidance template  
- `templates/command-template.md` - Slash command creation template
- `templates/agent-template.md` - Sub-agent configuration template

### Command Categories
Commands are organized by workflow type:
- `commands/claudegen/` - Commands for generating Claude configurations
- `commands/code/` - Code-related workflow commands
- `commands/design/` - Design and architecture commands
- `commands/plan/` - Planning and project management commands
- `commands/research/` - Research and analysis commands
- `commands/workflow/` - General workflow automation commands

## Key Concepts

### Memory System
This repository documents Claude Code's three-tier memory system:
1. **User Memory** (`~/.claude/CLAUDE.md`) - Personal preferences across all projects
2. **Project Memory** (`./CLAUDE.md`) - Team conventions for specific projects  
3. **Local Project Memory** (`./CLAUDE.local.md`) - Personal project-specific context

### Slash Commands
Custom automation framework using Markdown files with YAML frontmatter:
- Support bash command execution with `!` prefix
- File references with `@` prefix
- Argument substitution with `$ARGUMENTS`
- Tool access control via `allowed-tools` configuration

### Sub-Agents
Specialized AI assistants with focused expertise:
- Context isolation for specialized tasks
- Configurable tool access and permissions
- Automatic delegation based on task analysis
- Support for complex multi-agent workflows

## Development Workflow

### Creating New Templates
1. Use existing templates as starting points
2. Customize for specific use cases or technologies
3. Include clear guidance and examples
4. Follow established YAML frontmatter patterns

### Command Development  
1. Start with `templates/command-template.md`
2. Define clear objectives and constraints
3. Specify appropriate tool permissions
4. Test with actual use cases before sharing

### Documentation Updates
The `docs/` directory contains comprehensive reference material. When updating:
- Maintain consistency with established patterns
- Include practical examples
- Consider impact on existing templates
- Update related template files if needed

## Common Development Commands

### Template Generation
- Generate new templates: `/project:claudegen:create-command <command-name> [category] [description]`

### File Structure Analysis
- View template structure: `ls templates/` 
- Check command categories: `ls commands/`
- Validate Markdown formatting: Use standard Markdown linting tools

### Documentation Management
- Reference documentation is in `docs/` directory
- Templates are in `templates/` directory  
- Commands are organized by category in `commands/`

## Best Practices

### Template Design
- Provide clear placeholders with descriptive examples
- Include rationale for recommended patterns
- Balance specificity with flexibility
- Consider both individual and team usage

### Command Organization
- Group related commands by functional area
- Use descriptive filenames that match command purpose
- Include comprehensive documentation in command files
- Test commands in realistic development scenarios

### Documentation Maintenance
- Keep reference docs synchronized with current Claude Code features
- Update examples to reflect current best practices
- Maintain consistency across all documentation files
- Regular review and refinement based on usage patterns