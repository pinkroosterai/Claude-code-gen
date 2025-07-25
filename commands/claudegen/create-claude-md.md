---
description: Generate a new CLAUDE.md memory file to customize Claude Code's behavior and knowledge for your project
allowed-tools: Bash(pwd:*), Bash(ls:*), Bash(find:*), Bash(git:*), Bash(head:*), Bash(test:*), Bash(dirname:*), Bash(basename:*)
argument-hint: [type] [description]
---

# Claude Code Memory File Generator (CLAUDE.md)

## Dynamic Path Resolution
!`SCRIPT_DIR=$(cd "$(dirname "${BASH_SOURCE[0]}")" && pwd)`
!`PROJECT_ROOT=$(pwd)`
!`echo "Generator root: $PROJECT_ROOT"`

## Current Environment Analysis
!`echo "Current directory: $(pwd)"`
!`GIT_ROOT=$(git rev-parse --show-toplevel 2>/dev/null) && echo "Git repository root: $GIT_ROOT" || echo "Not in a git repository"`

## Existing Memory Files
!`echo "=== Searching for existing memory files ==="`
!`find . -maxdepth 3 -name "CLAUDE.md" -o -name "CLAUDE.local.md" 2>/dev/null | head -10 || echo "No memory files found in current directory"`
!`if [ -f "$HOME/.claude/CLAUDE.md" ]; then echo "User memory file found: ~/.claude/CLAUDE.md"; else echo "No user memory file found at ~/.claude/CLAUDE.md"; fi`

## Project Context Discovery
!`echo "=== Project structure ==="`
!`ls -la | head -20`
!`echo "\n=== Detecting project type ==="`
!`find . -maxdepth 3 \( -name "package.json" -o -name "requirements.txt" -o -name "Cargo.toml" -o -name "go.mod" -o -name "*.csproj" -o -name "pom.xml" -o -name "Gemfile" -o -name "composer.json" \) 2>/dev/null | head -10 || echo "No standard project files detected"`

## Template References
!`TEMPLATE_USER="$PROJECT_ROOT/templates/claude-template.md"`
!`TEMPLATE_PROJECT="$PROJECT_ROOT/templates/claude-project-template.md"`
!`if [ -f "$TEMPLATE_USER" ]; then echo "User template found"; else echo "WARNING: User template not found at $TEMPLATE_USER"; fi`
!`if [ -f "$TEMPLATE_PROJECT" ]; then echo "Project template found"; else echo "WARNING: Project template not found at $TEMPLATE_PROJECT"; fi`
@templates/claude-template.md
@templates/claude-project-template.md

## Memory File Generation Request

Create a CLAUDE.md memory file with the following specifications:

**Request:** $ARGUMENTS
**Parsed Arguments:**
!`if [ -n "$ARGUMENTS" ]; then echo "$ARGUMENTS" | awk '{print "Type: " $1; if(NF>1) {$1=""; print "Description:" $0}}'; else echo "No specific type requested - will determine based on context"; fi`
**Analysis Required:**

### Memory Type Determination
1. **User Memory** (`~/.claude/CLAUDE.md`)
   - Personal development preferences across all projects
   - General coding philosophy and approaches
   - Preferred tools and workflows
   - Learning and communication style

2. **Project Memory** (`./CLAUDE.md`)
   - Team conventions and standards
   - Architecture decisions and patterns
   - Technology stack specifics
   - Testing and deployment procedures

3. **Local Project Memory** (`./CLAUDE.local.md`)
   - Personal project-specific preferences
   - Local development environment settings
   - Individual workflow optimizations
   - Private debugging approaches

### Content Generation Guidelines

#### For User Memory Files
Focus on cross-project preferences:
- **Code Style Philosophy** - General approach to clean code
- **Debugging Methodology** - Systematic problem-solving approach
- **Testing Philosophy** - Beliefs about test design and coverage
- **Documentation Standards** - How to write effective docs
- **Communication Preferences** - How technical concepts should be explained
- **Learning Style** - Preferred ways to understand new concepts
- **Common Patterns** - Frequently used design patterns
- **Tool Preferences** - Editor, version control, and development tools

#### For Project Memory Files
Capture project-specific knowledge:
- **Project Overview** - Purpose, audience, and key requirements
- **Architecture Decisions** - High-level design and technology choices
- **Coding Standards** - Language-specific conventions and patterns
- **Testing Strategy** - Framework choices and coverage requirements
- **Error Handling** - Exception strategies and validation approaches
- **API Design** - Interface conventions and versioning
- **Security Requirements** - Authentication and authorization patterns
- **Performance Considerations** - Targets and optimization strategies
- **Deployment Process** - CI/CD pipeline and environments
- **Common Gotchas** - Project-specific issues to watch for

#### For Local Project Memory Files
Include personal project context:
- **Local Environment** - Development server URLs and configurations
- **Personal Shortcuts** - Custom commands and aliases
- **Test Data** - Preferred test scenarios and datasets
- **Debugging Setup** - Personal debugging tools and approaches
- **Work-in-Progress** - Current focus areas and experiments
- **Personal Notes** - Reminders and observations

### Project Analysis Steps

1. **Technology Detection**
   - Identify programming languages from file extensions
   - Detect frameworks from configuration files
   - Determine build tools and package managers
   - Recognize testing frameworks

2. **Convention Discovery**
   - Analyze existing code structure
   - Identify naming patterns
   - Detect architectural patterns
   - Review existing documentation

3. **Context Integration**
   - Consider user's stated preferences
   - Adapt templates to project specifics
   - Include relevant best practices
   - Ensure actionable guidance

### Output Requirements

1. **Header Section**
   - Start with `# CLAUDE.md` or appropriate title
   - Add explanatory comment about file purpose
   - Include generation timestamp if helpful

2. **Content Organization**
   - Use clear, hierarchical Markdown structure
   - Group related concepts under descriptive headings
   - Provide specific, actionable guidance
   - Include examples where helpful

3. **Style Guidelines**
   - Write in clear, concise language
   - Avoid generic or obvious statements
   - Focus on project-specific insights
   - Balance comprehensiveness with readability

4. **Integration Advice**
   - Suggest appropriate file location
   - Explain version control considerations
   - Recommend complementary memory files
   - Provide usage tips

## Delivery Process

1. **Analyze the request** to determine memory type and focus areas
2. **Examine project context** to understand technology stack and conventions
3. **Generate appropriate content** using templates as foundation
4. **Create the memory file** with proper structure and formatting
5. **Provide integration guidance** for effective usage

Focus on creating memory content that provides genuine value by capturing specific, actionable knowledge that improves development efficiency and consistency.