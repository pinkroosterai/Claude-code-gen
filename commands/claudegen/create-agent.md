---
description: Generate a new Claude Code sub-agent configuration to extend Claude's capabilities with specialized expertise
allowed-tools: Bash(ls:*), Bash(mkdir:*), Bash(find:*), Bash(test:*), Bash(dirname:*), Bash(basename:*)
argument-hint: <agent-name> [type] [description]
---

# Claude Code Sub-Agent Generator

## Argument Validation
!`if [ -z "$ARGUMENTS" ]; then echo "ERROR: Agent name is required. Usage: /project:claudegen:create-agent <agent-name> [type] [description]"; exit 1; fi`

## Dynamic Path Resolution
!`SCRIPT_DIR=$(cd "$(dirname "${BASH_SOURCE[0]}")" && pwd)`
!`PROJECT_ROOT=$(pwd)`
!`echo "Project root: $PROJECT_ROOT"`

## Current Agent Structure
!`find "$PROJECT_ROOT/agents" -name "*.md" 2>/dev/null | head -10 || echo "No existing agents found"`
!`find ".claude/agents" -name "*.md" 2>/dev/null | head -10 || echo "No project agents found"`
!`find "$HOME/.claude/agents" -name "*.md" 2>/dev/null | head -10 || echo "No user agents found"`

## Agent Storage Locations
!`echo "Project agents: .claude/agents/"`
!`echo "User agents: ~/.claude/agents/"`

## Template Reference
!`TEMPLATE_PATH="$PROJECT_ROOT/templates/agent-template.md"`
!`if [ -f "$TEMPLATE_PATH" ]; then echo "Template found at: $TEMPLATE_PATH"; else echo "WARNING: Template not found at $TEMPLATE_PATH"; fi`
@templates/agent-template.md

## Claude Code Sub-Agent Generation Request

Generate a new Claude Code sub-agent to extend Claude's capabilities with specialized expertise:

**Agent Name:** $ARGUMENTS
**Parsed Arguments:**
!`echo "$ARGUMENTS" | awk '{print "Name: " $1; if(NF>1) print "Type: " $2; if(NF>2) {$1=$2=""; print "Description:" $0}}'`
**Target Location:** Determine if this should be a project or user agent
**Requirements Analysis:** Analyze the agent description to determine:

### Core Expertise Definition
1. **Primary Domain** - What specific area does this agent specialize in?
2. **Key Responsibilities** - What are the 3-5 main tasks it handles?
3. **Expertise Level** - What depth of knowledge should it demonstrate?
4. **Unique Value** - What makes this agent more effective than general assistance?

### Methodology Specification
- **Analysis Approach** - How should the agent systematically approach problems?
- **Decision Framework** - What criteria guide the agent's recommendations?
- **Communication Style** - How should findings be structured and presented?
- **Quality Standards** - What output standards should be maintained?

### Technical Configuration
1. **Tool Requirements** - Which tools are essential for this agent's role?
   - Read-only tools for analysis agents
   - Execution tools for automation agents
   - Write tools for generation agents
2. **Security Constraints** - What permissions align with principle of least privilege?
3. **Delegation Trigger** - One-line description for automatic task routing
4. **Context Boundaries** - What should the agent explicitly avoid?

### Knowledge Components
- **Domain Principles** - Fundamental concepts the agent must understand
- **Best Practices** - Proven approaches for common scenarios
- **Common Patterns** - Typical situations and optimal responses
- **Anti-patterns** - What to watch for and actively avoid

### Implementation Structure
Generate the complete agent file following these patterns:
1. **YAML Frontmatter** with system prompt, description, and tools
2. **Role Definition** establishing clear identity and expertise
3. **Methodology Section** detailing systematic approaches
4. **Domain Knowledge** encoding specific expertise
5. **Constraints and Boundaries** preventing scope creep
6. **Output Standards** ensuring consistent, professional results

### Agent Type Patterns

#### Code Review Specialist
- Focus: Security, performance, maintainability, consistency
- Tools: Read-only file access, search capabilities
- Approach: Systematic review with severity levels

#### Debugging Expert
- Focus: Problem isolation, root cause analysis, solution verification
- Tools: Read access, bash execution for diagnostics
- Approach: Hypothesis-driven investigation

#### Testing Automation
- Focus: Test creation, execution, coverage analysis
- Tools: File manipulation, test runners, coverage tools
- Approach: Comprehensive test strategy implementation

#### Documentation Specialist
- Focus: Clarity, completeness, maintainability
- Tools: Read and write access for documentation files
- Approach: User-centric documentation creation

#### Performance Analyst
- Focus: Bottleneck identification, optimization strategies
- Tools: Profiling tools, diagnostic commands
- Approach: Data-driven performance improvement

#### Architecture Consultant
- Focus: Design patterns, scalability, maintainability
- Tools: Diagram generation, code analysis
- Approach: Strategic technical decision making

## Delivery Requirements

1. **Analyze the request** to determine agent type and specialization
2. **Generate the complete agent file** with comprehensive system prompt
3. **Determine appropriate location** (project vs user agent)
4. **Create the file** with proper YAML structure
5. **Provide activation instructions** showing how to use the new agent
6. **Suggest complementary agents** that might work well together

Focus on creating an agent that provides genuine expertise in its domain while maintaining appropriate boundaries and security constraints. Ensure the agent's personality and approach align with professional development practices.