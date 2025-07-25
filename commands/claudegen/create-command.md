---
description: Generate a new Claude Code slash command to automate workflows and extend Claude's capabilities
allowed-tools: Bash(ls:*), Bash(mkdir:*), Bash(find:*), Bash(test:*), Bash(dirname:*), Bash(basename:*)
argument-hint: <command-name> [--scope=project|user] [--category=category] [--description="description"]
---

# Claude Code Slash Command Generator

## Argument Validation
!`if [ -z "$ARGUMENTS" ]; then echo "ERROR: Command name is required. Usage: /project:claudegen:create-command <command-name> [--scope=project|user] [--category=category] [--description=\"description\"]"; exit 1; fi`

## Dynamic Path Resolution
!`SCRIPT_DIR=$(cd "$(dirname "${BASH_SOURCE[0]}")" && pwd)`
!`PROJECT_ROOT=$(pwd)`
!`echo "Project root: $PROJECT_ROOT"`

## Current Command Structure
!`echo "=== Existing commands in this project ==="`
!`find "$PROJECT_ROOT/commands" -name "*.md" -type f 2>/dev/null | sort | head -20 || echo "No commands found"`
!`echo "\n=== User commands ==="`
!`find "$HOME/.claude/commands" -name "*.md" -type f 2>/dev/null | sort | head -10 || echo "No user commands found"`

## Existing Categories
!`echo "=== Project command categories ==="`
!`ls -1 "$PROJECT_ROOT/commands/" 2>/dev/null || echo "No project command categories found"`
!`echo "=== User command categories ==="`
!`ls -1 "$HOME/.claude/commands/" 2>/dev/null || echo "No user command categories found"`

## Template Reference
!`TEMPLATE_PATH="$PROJECT_ROOT/templates/command-template.md"`
!`if [ -f "$TEMPLATE_PATH" ]; then echo "Template found at: $TEMPLATE_PATH"; else echo "WARNING: Template not found at $TEMPLATE_PATH"; fi`
@templates/command-template.md

## Command Generation Request

Create a new slash command with the following specifications:

**Arguments:** $ARGUMENTS
**Parsed Arguments:**
!`echo "$ARGUMENTS" | sed 's/--scope=/\nScope: /g; s/--category=/\nCategory: /g; s/--description=/\nDescription: /g' | sed 's/"//g' | head -10`
!`COMMAND_NAME=$(echo "$ARGUMENTS" | awk '{print $1}')`
!`SCOPE=$(echo "$ARGUMENTS" | grep -o 'scope=[^[:space:]]*' | cut -d= -f2 | tr -d '"')`
!`CATEGORY=$(echo "$ARGUMENTS" | grep -o 'category=[^[:space:]]*' | cut -d= -f2 | tr -d '"')`
!`if echo "$COMMAND_NAME" | grep -q '[^a-zA-Z0-9_-]'; then echo "WARNING: Command name contains special characters. Consider using only alphanumeric characters, hyphens, and underscores."; fi`
## Command Storage Location Analysis
!`echo "=== Scope Detection ==="`
!`if [ "$SCOPE" = "project" ]; then echo "Explicitly requested: PROJECT scope"; TARGET_DIR="$PROJECT_ROOT/commands"; elif [ "$SCOPE" = "user" ]; then echo "Explicitly requested: USER scope"; TARGET_DIR="$HOME/.claude/commands"; else echo "Auto-detecting based on context..."; if [ -d "$PROJECT_ROOT/commands" ]; then echo "Found project commands directory - using PROJECT scope"; TARGET_DIR="$PROJECT_ROOT/commands"; else echo "No project commands directory - using USER scope"; TARGET_DIR="$HOME/.claude/commands"; fi; fi`
!`echo "Target directory: $TARGET_DIR"`

**Available Scopes:**
- **project** - Create in `./commands/` (project-specific command)
- **user** - Create in `~/.claude/commands/` (user-wide command)
- Auto-detect if not specified based on current context
**Requirements Analysis:** Analyze the command description to determine:

### Essential Components
1. **Primary Function** - What is the main task this command performs?
2. **Context Requirements** - What information does it need to gather?
3. **Tool Dependencies** - Which tools should it have access to?
4. **Expected Arguments** - What parameters should it accept?
5. **Output Format** - How should results be structured?

### Technical Specifications
- **Bash Commands** - What system information needs to be gathered?
- **File References** - Which files should be included as context?
- **Security Constraints** - What tool permissions are appropriate?
- **Error Handling** - How should edge cases be managed?

### Implementation Guidelines
1. Use the command template structure as the foundation
2. Include comprehensive context gathering in the bash execution section
3. Provide clear objectives and constraints
4. Specify expected output format
5. Add appropriate tool restrictions for security

### Category Placement
Determine the most appropriate category directory:
- `claudegen/` - Commands for generating Claude configurations
- `code/` - Code analysis, review, and manipulation commands  
- `design/` - Architecture and design decision commands
- `plan/` - Planning and project management commands
- `research/` - Analysis and investigation commands
- `workflow/` - General automation and process commands

### Command File Structure
Generate the complete command file following these patterns:
- YAML frontmatter with proper metadata
- Context gathering bash commands with appropriate permissions
- File references for relevant documentation or code
- Clear instruction sections with objectives and constraints
- Professional formatting and comprehensive documentation

## Delivery Requirements

1. **Analyze the request** and determine command scope (project vs user), category, and requirements
2. **Generate the complete command file** with proper YAML frontmatter
3. **Create the file** in the appropriate directory:
   - Project commands: `./commands/[category]/[command-name].md`
   - User commands: `~/.claude/commands/[category]/[command-name].md`
4. **Provide usage instructions** showing how to invoke the new command
5. **Suggest related commands** that might work well with this new command

Focus on creating a command that follows established patterns while being genuinely useful for the specified purpose. Ensure proper security constraints and clear documentation.