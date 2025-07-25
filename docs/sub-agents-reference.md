# Complete Sub-Agents Reference Guide

## Understanding the Foundation: What Are Sub-Agents and Why Do They Matter?

Imagine you're working on a complex software project and you need different types of expertise throughout your development process. Sometimes you need a meticulous code reviewer who catches security vulnerabilities, other times you need a debugging specialist who can trace through complex error conditions, and occasionally you need a data analyst who can write sophisticated SQL queries. In a traditional development environment, you might switch between different tools, consult different team members, or context-switch between different mental models for approaching these varied tasks.

Sub-agents in Claude Code solve this challenge by creating specialized AI personalities that you can delegate specific types of work to. Think of sub-agents as having a team of focused experts available on demand, each with their own expertise area, working style, and set of tools they're proficient with. When you encounter a task that falls within a sub-agent's domain of expertise, Claude Code can either automatically delegate that work to the appropriate specialist or you can explicitly request that a particular sub-agent handle the task.

The power of this approach lies in specialization and context management. Just as human experts develop deep knowledge in specific domains, sub-agents can be configured with detailed knowledge about particular types of problems, specific approaches to solving them, and even constraints about which tools they should use. This specialization leads to more accurate, focused, and helpful responses because the sub-agent can apply domain-specific knowledge without the distraction of trying to be a generalist.

## The Architecture: How Sub-Agents Create Specialized Contexts

Understanding how sub-agents work requires grasping the concept of context isolation, which represents one of the most sophisticated aspects of the Claude Code system. In a typical conversation with Claude, everything you discuss becomes part of a single, shared context that influences all subsequent responses. While this shared context can be valuable for maintaining continuity, it can also become a limitation when you need to work on diverse, unrelated tasks within the same development session.

Sub-agents solve this problem by operating in completely separate context windows. When Claude Code delegates a task to a sub-agent, that sub-agent starts with a clean slate, focusing exclusively on the specific task at hand without being influenced by unrelated discussions that might have happened earlier in your main conversation. This context isolation serves multiple important purposes that become clearer when you consider the alternative.

In a shared context system, if you spent the first part of your session discussing frontend component architecture and then needed to debug a backend database performance issue, the AI might inappropriately try to connect these unrelated topics or apply frontend-oriented thinking to a backend problem. With sub-agents, your database debugging specialist operates in isolation, applying only relevant database and performance knowledge to the problem without any interference from the earlier frontend discussion.

This architectural approach also enables much longer, more productive development sessions. In traditional AI interactions, context windows eventually become full, forcing you to either lose important information or start fresh conversations. Sub-agents help preserve your main context for high-level coordination and decision-making while offloading specific technical tasks to specialists who don't consume space in your primary conversation thread.

The context isolation also creates opportunities for more sophisticated workflows. You might have your main conversation focused on project planning and coordination while simultaneously having sub-agents working on code review, testing, and documentation tasks. Each specialist maintains its own understanding of its specific domain without cluttering your primary strategic conversation.

## The Two-Tier Storage System: Project versus Personal Sub-Agents

Sub-agents follow the same thoughtful organizational approach as other Claude Code customizations, using a two-tier system that balances personal preferences with team collaboration needs. Understanding this system helps you make strategic decisions about where to create different types of sub-agents and how to organize them for maximum effectiveness.

**Project sub-agents** live within your repository at `.claude/agents/` and represent shared team knowledge and workflows. When you create a project sub-agent, you're essentially encoding your team's collective expertise about how to handle specific types of tasks within that particular project. These sub-agents become part of your project's development infrastructure, evolving alongside your codebase and ensuring consistent approaches across all team members.

Consider a project sub-agent designed for your team's specific code review process. This sub-agent might know about your particular architectural patterns, understand your security requirements, be familiar with your performance benchmarks, and apply your team's specific coding standards. When any team member uses this sub-agent, they get consistent, project-appropriate guidance that reflects your collective knowledge and decisions.

Project sub-agents also serve as institutional memory, capturing knowledge that might otherwise be lost when team members change roles or leave the organization. The debugging approaches that work best for your specific technology stack, the testing strategies that have proven most effective for your application architecture, or the deployment verification steps that prevent issues in your particular environment can all be encoded into project sub-agents that preserve this knowledge for current and future team members.

**User sub-agents** reside in your home directory at `~/.claude/agents/` and represent your personal development expertise and preferences that apply across all projects you work on. These sub-agents reflect your individual approach to software development, your personal debugging techniques, your preferred analysis methods, or your specialized knowledge areas that you bring to different projects.

A user sub-agent might embody your personal approach to performance optimization, incorporating techniques you've learned across multiple projects and technologies. This sub-agent travels with you from project to project, providing consistent access to your accumulated expertise regardless of which specific codebase you're working on.

The precedence system works intuitively: when sub-agent names conflict between project and user levels, project-specific sub-agents take priority. This allows teams to override personal preferences with project-specific requirements while still allowing individual developers to maintain their personal toolkit of specialists for areas not covered by project sub-agents.

## Creating Effective Sub-Agents: The Art of Specialization

The process of creating sub-agents involves more than just writing system prompts; it requires thinking carefully about specialization, scope, and the specific value each sub-agent provides. The most effective sub-agents emerge from a deep understanding of specific problem domains and clear thinking about when specialized expertise adds value over general-purpose assistance.

### Starting with Claude-Generated Foundations

The recommended approach for creating sub-agents begins with leveraging Claude's own understanding of different expert domains. When you use the `/agents` command to create a new sub-agent, Claude can generate an initial foundation that captures the essential knowledge and approaches for specific types of expertise. This Claude-generated foundation provides several advantages that become apparent when you compare it to starting from scratch.

Claude's initial sub-agent generation draws on its broad training to identify the key responsibilities, methodologies, and best practices associated with different expert roles. For a code reviewer sub-agent, Claude understands the importance of security considerations, performance implications, maintainability concerns, and team consistency. For a debugging specialist, Claude knows about systematic approaches to problem isolation, evidence gathering, hypothesis testing, and solution verification.

However, the real value comes from using this generated foundation as a starting point for customization rather than an endpoint. Claude's initial generation provides professional-grade expertise, but your specific development environment, team conventions, project requirements, and personal preferences require additional refinement to make the sub-agent truly effective in your particular context.

This customization process involves several important considerations. You need to adapt the sub-agent's approach to match your team's specific workflows, incorporate knowledge about your particular technology stack, adjust the communication style to match your preferences, and ensure the sub-agent understands any constraints or requirements specific to your development environment.

### Designing Focused Responsibilities

The most successful sub-agents follow the principle of focused responsibility, handling specific types of tasks extremely well rather than trying to be general-purpose assistants. This focus creates several important advantages that compound over time as you use the sub-agents in real development scenarios.

Focused sub-agents develop deeper expertise in their specific domains because their system prompts can include detailed guidance about particular types of problems, specific methodologies that work best for certain situations, and accumulated knowledge about edge cases and subtle considerations that matter in specialized contexts. A debugging sub-agent can include sophisticated approaches to different types of bugs, systematic methodologies for isolating problems, and specific techniques for different programming languages or runtime environments.

The focus also makes sub-agents more predictable and reliable. When you invoke a code review sub-agent, you know exactly what type of analysis you'll receive and what aspects of your code will be examined. This predictability helps you develop efficient workflows where you know which sub-agent to use for which types of tasks, creating a more streamlined development experience.

Focused responsibility also enables better tool selection and security posture. A sub-agent that only needs to read and analyze code doesn't need write permissions or bash execution capabilities, while a sub-agent responsible for automated testing might need broader tool access. This granular approach to permissions follows security best practices while ensuring each sub-agent has exactly the capabilities it needs to be effective.

### Crafting Detailed System Prompts

The system prompt represents the heart of a sub-agent's expertise, encoding not just what the sub-agent should do but how it should approach problems, what methodologies it should apply, and what constraints should guide its behavior. Writing effective system prompts requires balancing several important considerations that influence how well the sub-agent performs in real development scenarios.

Effective system prompts begin with clear role definition that establishes the sub-agent's identity and primary responsibilities. Rather than vague descriptions like "helps with code," effective prompts establish specific expertise areas like "senior security-focused code reviewer specializing in web application vulnerabilities" or "database performance optimization specialist with expertise in PostgreSQL and query analysis."

The prompt should include specific methodologies that guide how the sub-agent approaches problems within its domain. A debugging sub-agent might follow a systematic approach that starts with error message analysis, moves through reproduction steps, includes hypothesis formation and testing, and concludes with solution verification. Including these methodologies in the system prompt ensures consistent, professional approaches to problem-solving.

Consider including specific examples or patterns within the system prompt that illustrate the sub-agent's approach to common scenarios. These examples serve as templates that help the sub-agent understand not just what to do but how to communicate its findings effectively. A code reviewer might include examples of how to structure feedback with severity levels, specific recommendations, and code examples that demonstrate improvements.

The system prompt should also establish constraints and boundaries that prevent the sub-agent from overstepping its intended role. A testing sub-agent might be instructed to focus on test implementation and execution rather than broader architectural concerns, while a documentation sub-agent might be constrained to focus on clarity and completeness rather than implementation details.

## Managing Tool Access: Security and Capability Considerations

Tool access management represents one of the most important aspects of sub-agent configuration, balancing capability needs with security considerations. Understanding how to configure tool access effectively requires thinking about both what each sub-agent needs to accomplish its tasks and what potential risks different tool combinations might create.

### Understanding Tool Inheritance

The default behavior for sub-agent tool access involves inheriting all tools available to the main Claude Code session, including any connected MCP (Model Context Protocol) tools. This inheritance model provides immediate capability while allowing you to restrict access when security or focus considerations make limitations appropriate.

Tool inheritance works well for sub-agents that need broad access to your development environment, such as a general-purpose debugging specialist that might need to read files, execute commands, search through codebases, and interact with various development tools. However, inheritance might be too permissive for specialized sub-agents that have more focused responsibilities.

The inheritance model also means that sub-agents automatically gain access to new tools as you connect additional MCP servers or enable new Claude Code capabilities. This automatic capability expansion can be beneficial for sub-agents that should have access to your full development toolkit, but it requires consideration of whether new tools align with each sub-agent's intended role and security posture.

### Implementing Granular Tool Control

When sub-agent responsibilities are more focused, implementing granular tool control provides better security and helps the sub-agent maintain focus on its intended tasks. The `tools` configuration field in sub-agent definitions allows you to specify exactly which tools each sub-agent can access, creating a more controlled and predictable environment.

Granular tool control works particularly well for sub-agents that have specific, well-defined responsibilities. A code analysis sub-agent might only need file reading capabilities and text search tools, while a deployment verification sub-agent might need bash execution for running specific commands but shouldn't have write access to source files.

The tool selection process benefits from thinking about the minimum set of capabilities each sub-agent needs to be effective. This principle of least privilege reduces security risks while also helping the sub-agent focus on its core responsibilities without being distracted by irrelevant capabilities.

Consider the workflow implications of tool restrictions when designing sub-agent tool access. A sub-agent that can identify problems but cannot implement fixes might be appropriate for review and analysis tasks, while a sub-agent responsible for automated problem resolution might need broader tool access to implement solutions.

### Using the Interactive Tool Management Interface

The `/agents` command provides an interactive interface for managing tool access that makes it easier to understand available tools and configure appropriate permissions for each sub-agent. This interface becomes particularly valuable when working with complex development environments that include multiple MCP servers and diverse tool ecosystems.

The interactive interface lists all available tools, including both Claude Code's built-in capabilities and any tools provided by connected MCP servers. This comprehensive view helps you understand what capabilities are available and make informed decisions about which tools each sub-agent should have access to.

The interface also provides descriptions and context for different tools, helping you understand what each tool does and whether it's appropriate for particular sub-agent roles. This contextual information becomes especially valuable when working with MCP tools that might have capabilities you're not immediately familiar with.

When modifying existing sub-agents, the interactive interface shows current tool configurations and makes it easy to add or remove specific tools based on evolving requirements or changing security considerations.

## Effective Sub-Agent Usage Patterns

Understanding how to use sub-agents effectively involves developing intuition about when delegation adds value, how to structure requests for optimal results, and how to combine sub-agent capabilities with your broader development workflow.

### Automatic Delegation: Teaching Claude When to Use Sub-Agents

Claude Code's automatic delegation system represents one of the most sophisticated aspects of the sub-agent framework, using contextual clues to determine when specific sub-agents would be most appropriate for particular tasks. Understanding how this system works helps you configure sub-agents and structure requests to maximize the benefits of automatic delegation.

The automatic delegation system analyzes several factors when determining whether to invoke a sub-agent. The task description in your request provides primary signals about what type of expertise might be needed, while the `description` fields in your sub-agent configurations establish the domains where each specialist should be considered. The current context and available tools also influence delegation decisions, ensuring that sub-agents are only invoked when they can actually contribute to solving the problem at hand.

To maximize automatic delegation, the `description` field in your sub-agent configurations should be specific and action-oriented, clearly establishing when the sub-agent should be invoked. Rather than vague descriptions like "helps with testing," effective descriptions might specify "automatically runs and analyzes test failures, providing specific fixes for common test issues" or "reviews all code changes for security vulnerabilities and performance implications."

Including trigger phrases like "use PROACTIVELY" or "MUST BE USED" in description fields signals to Claude Code that the sub-agent should be considered automatically when relevant tasks arise. These phrases help overcome any hesitation in the delegation system and ensure that specialized expertise is applied consistently when appropriate.

The automatic delegation system works best when sub-agent descriptions clearly establish boundaries and contexts where each specialist is most valuable. This specificity helps Claude Code make appropriate delegation decisions without confusion about which sub-agent might be best suited for ambiguous or overlapping task types.

### Explicit Invocation: Direct Control Over Sub-Agent Usage

While automatic delegation provides convenience and consistency, explicit invocation gives you direct control over which sub-agents handle specific tasks. This explicit control proves valuable when you want to ensure a particular type of analysis is performed, when you're working on edge cases that might not trigger automatic delegation, or when you want to leverage specific sub-agent expertise for exploratory analysis.

Explicit invocation works through natural language requests that mention the sub-agent by name and clearly specify what you want that specialist to focus on. The request structure can be conversational and context-aware, allowing you to provide specific guidance about what aspects of the problem the sub-agent should prioritize or what constraints should guide its analysis.

Effective explicit invocation often includes context about why you're requesting a particular sub-agent, what specific aspects of their expertise you want to leverage, and what outcomes you're hoping to achieve. This contextual information helps the sub-agent understand not just what to analyze but what type of insights or recommendations would be most valuable for your current situation.

Explicit invocation also enables sub-agent chaining, where you might request that multiple specialists work on different aspects of a complex problem. You could have a security reviewer analyze potential vulnerabilities in a code change, followed by a performance specialist examining the efficiency implications, concluded by a testing expert developing comprehensive test cases for the new functionality.

## Advanced Sub-Agent Patterns and Workflows

As you develop expertise with sub-agents, several advanced patterns emerge that leverage the full potential of specialized AI assistance within complex development workflows.

### Creating Sub-Agent Ecosystems

The most sophisticated sub-agent implementations involve creating ecosystems of specialists that work together to handle complex, multi-faceted development challenges. These ecosystems recognize that real development problems often require multiple types of expertise applied in coordination rather than isolation.

Consider a deployment readiness workflow that involves multiple sub-agents working in sequence. A security reviewer might first analyze the proposed changes for potential vulnerabilities, followed by a performance specialist examining efficiency implications, then a testing expert verifying comprehensive test coverage, and finally a deployment specialist checking configuration requirements and rollback procedures.

Sub-agent ecosystems work best when individual specialists have clear, non-overlapping responsibilities but can build upon each other's work. The security reviewer establishes that the code is safe to deploy, the performance specialist confirms that it won't negatively impact system efficiency, the testing expert verifies that it's thoroughly validated, and the deployment specialist ensures that the rollout process is properly planned.

Creating effective ecosystems requires thinking about information flow between sub-agents and ensuring that each specialist has access to the context and findings from previous analyses. This might involve structuring requests so that later sub-agents can reference the work of earlier specialists, or using explicit chaining where you request that specific sub-agents build upon previous analyses.

### Contextual Sub-Agent Selection

Advanced sub-agent usage involves developing intuition about which specialists are most appropriate for different types of problems and learning to provide contextual cues that guide optimal sub-agent selection. This contextual awareness helps you leverage the right expertise at the right time while avoiding unnecessary overhead from inappropriate specialist involvement.

Different development phases often benefit from different sub-agent involvement patterns. During active development, you might rely heavily on debugging specialists and code reviewers who can provide immediate feedback and problem resolution. During preparation for releases, deployment specialists and comprehensive testing experts become more important. During maintenance phases, performance optimization and security audit specialists might take precedence.

The complexity and scope of problems also influence optimal sub-agent selection. Simple, focused issues might benefit from direct specialist involvement, while complex, multi-faceted problems might require ecosystem approaches with multiple specialists contributing different perspectives and expertise areas.

Understanding your project's specific risk profile and priorities helps guide sub-agent selection decisions. Security-critical applications might benefit from more frequent security reviewer involvement, while performance-sensitive systems might require regular performance specialist analysis. High-reliability systems might emphasize testing and deployment verification specialists.

### Sub-Agent Learning and Evolution

While individual sub-agents don't learn or retain information across invocations, your sub-agent configurations can evolve based on experience and changing project requirements. This evolution process involves regularly reviewing sub-agent effectiveness, updating system prompts based on lessons learned, and refining tool access based on actual usage patterns.

Effective sub-agent evolution involves paying attention to which sub-agents provide the most value in your specific development context, what types of problems they handle most effectively, and where gaps exist in your current specialist coverage. This analysis helps guide decisions about creating new sub-agents, modifying existing ones, or reorganizing responsibilities among your current specialists.

The evolution process also benefits from team feedback when working with project-level sub-agents. Different team members might discover new use cases for existing sub-agents, identify areas where specialist expertise could be more helpful, or suggest modifications that would make sub-agents more effective for team-wide usage.

Consider versioning important sub-agent configurations, especially project-level specialists that multiple team members rely on. This versioning approach allows you to experiment with improvements while maintaining stable fallback configurations if changes don't work as expected.

## Troubleshooting and Optimization

Understanding how to diagnose and resolve common sub-agent issues helps you maintain an effective specialist ecosystem and optimize performance for your specific development workflows.

### Performance Considerations and Context Management

Sub-agent performance involves balancing the benefits of specialized expertise against the overhead of context switching and the latency associated with delegating tasks to separate context windows. Understanding these performance implications helps you make informed decisions about when sub-agent delegation adds value versus when direct interaction might be more efficient.

The context isolation that makes sub-agents powerful also creates performance considerations. Each sub-agent invocation starts with a clean context window, which means the sub-agent might need to gather relevant context about your current problem before providing specialized assistance. This context gathering process can add latency, especially for sub-agents that need to understand significant amounts of background information.

Optimizing sub-agent performance often involves designing system prompts that help specialists quickly understand and focus on the essential aspects of problems without requiring extensive context exploration. Well-designed sub-agents include guidance about what information is most important for their specific expertise areas and how to efficiently gather necessary context.

The main conversation context preservation represents one of the key performance benefits of sub-agents. By offloading specialized tasks to separate context windows, you can maintain longer, more productive main conversations focused on high-level coordination and decision-making. This context preservation becomes particularly valuable during extended development sessions that span multiple different types of tasks.

### Diagnosing Sub-Agent Issues

When sub-agents don't behave as expected, systematic diagnosis helps identify whether issues stem from configuration problems, prompt design challenges, tool access limitations, or context misunderstandings. Understanding common failure modes guides effective troubleshooting approaches.

Configuration issues often manifest as sub-agents not being available when expected or not having access to required tools. Verifying file locations, checking YAML frontmatter syntax, and confirming tool availability help resolve these fundamental configuration problems.

Prompt design issues typically appear as sub-agents that understand their role but apply inappropriate approaches or focus on wrong aspects of problems. These issues often require refining system prompts to provide clearer guidance about methodologies, constraints, and expected outcomes.

Tool access problems usually become apparent when sub-agents attempt to perform actions they don't have permissions for or when they can't access information necessary for their analysis. Reviewing and adjusting tool configurations often resolves these capability mismatches.

Context misunderstandings might occur when sub-agents make incorrect assumptions about the problem they're supposed to solve or when they lack sufficient information to apply their expertise effectively. These issues often benefit from more explicit invocation with clearer problem descriptions and relevant context.

### Optimizing Sub-Agent Effectiveness

Continuous improvement of sub-agent effectiveness involves regular evaluation of how well specialists perform their intended roles and systematic refinement based on actual usage experience. This optimization process helps ensure that your sub-agent ecosystem continues to provide value as your development practices and project requirements evolve.

Effective optimization begins with tracking which sub-agents you use most frequently, what types of problems they handle best, and where their assistance proves most valuable. This usage analysis helps guide decisions about where to invest effort in improving existing sub-agents versus creating new specialists for unaddressed needs.

The optimization process also benefits from experimentation with different prompt approaches, tool configurations, and responsibility boundaries. Small, focused experiments help identify improvements without disrupting established workflows, allowing you to refine sub-agent effectiveness incrementally.

Consider gathering feedback from team members about project-level sub-agents, particularly regarding which specialists they find most helpful, what improvements would increase value, and what additional expertise areas might benefit from specialist coverage. This collaborative approach helps ensure that shared sub-agents serve the entire team effectively.

Regular review and maintenance of sub-agent configurations helps prevent degradation over time as project requirements change and development practices evolve. This maintenance process ensures that specialist expertise remains current and aligned with actual development needs rather than becoming outdated artifacts of previous project phases.

The most effective sub-agent ecosystems evolve organically based on real development needs while maintaining focus on providing genuine value rather than complexity for its own sake. Start with a few well-designed specialists that address clear needs, then expand and refine based on experience and changing requirements. This measured approach helps build a sub-agent system that enhances your development workflow rather than adding unnecessary overhead or complexity.