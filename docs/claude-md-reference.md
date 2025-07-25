# Complete CLAUDE.md Reference Guide

## Understanding the Foundation: What Are CLAUDE.md Files?

Think of CLAUDE.md files as Claude Code's memory system. Just as you might keep notes about a project's conventions or your personal preferences in a notebook, CLAUDE.md files serve as persistent memory that Claude Code can reference across different sessions. These files bridge the gap between the ephemeral nature of individual conversations and the need for consistent, contextual assistance over time.

The beauty of this system lies in its simplicity and flexibility. Rather than requiring complex configuration files or database setups, Claude Code uses plain Markdown files that you can read, edit, and version control just like any other project documentation. This approach makes the memory system transparent, portable, and easy to understand.

## The Three-Tier Memory Architecture

Claude Code organizes memory into three distinct tiers, each serving a specific purpose in your development workflow. Understanding this hierarchy is crucial because it determines how Claude prioritizes and applies different pieces of information.

### User Memory: Your Global Preferences

At the foundation of the memory system sits your user memory, stored in `~/.claude/CLAUDE.md` within your home directory. This file represents your personal preferences and conventions that should apply across every project you work on. Think of this as your development personality encoded in text.

Your user memory might include preferences like your coding style, preferred libraries, common debugging approaches, or general development philosophies. For example, you might specify that you always prefer TypeScript interfaces over type aliases, or that you follow a particular error handling pattern. These preferences become part of Claude's understanding of how you like to work, regardless of which project you're currently focused on.

The user memory file serves as your baseline. When you start a new project or work in an environment without project-specific memory files, Claude will still understand your fundamental preferences and can provide assistance aligned with your personal development style.

### Project Memory: Team Conventions and Shared Knowledge

The next layer consists of project memory, stored in `./CLAUDE.md` files within your project directories. These files capture the shared knowledge, conventions, and decisions that apply to a specific project and should be consistent across all team members working on that project.

Project memory typically includes architectural decisions, coding standards, deployment procedures, testing strategies, and any project-specific context that new team members need to understand. For instance, you might document that the project uses a particular state management pattern, follows specific naming conventions for database tables, or has certain performance requirements that influence design decisions.

When you commit project memory files to version control, they become living documentation that evolves with your project. This creates a feedback loop where the memory files help maintain consistency while also serving as onboarding documentation for new team members.

### Local Project Memory: Personal Project Context

The most specific layer consists of local project memory, stored in `./CLAUDE.local.md` files. These files contain personal preferences and context that apply to a specific project but shouldn't be shared with other team members. By convention, these files are typically added to `.gitignore` to keep them local to your development environment.

Local project memory might include your personal development server URLs, preferred test data sets, individual debugging preferences, or shortcuts specific to your local setup. This allows you to maintain personal productivity enhancements without imposing them on your team or cluttering the shared project memory.

## How Claude Code Discovers and Loads Memory

Understanding how Claude Code finds and loads memory files helps you organize your projects more effectively and troubleshoot when memory isn't working as expected.

### The Recursive Discovery Process

When you launch Claude Code, it begins a recursive search process starting from your current working directory. This search moves upward through the directory tree, collecting every `CLAUDE.md` and `CLAUDE.local.md` file it encounters until it reaches the filesystem root.

This recursive approach creates powerful possibilities for organizing large projects. Imagine you're working on a monorepo with multiple services. You might have memory files organized like this: a root-level `CLAUDE.md` containing overall project conventions, service-specific memory files in each service directory, and even more granular memory files in subdirectories for complex services.

When you run Claude Code from deep within this structure, it automatically builds a complete picture by loading all relevant memory files. The most specific files take precedence, allowing you to override general conventions with more specific guidance when needed.

### Memory Loading Order and Precedence

Claude Code loads memory files in a specific order that creates a logical precedence system. User memory loads first, establishing your baseline preferences. Then project-specific memory files load from the filesystem root down to your current directory, with each more specific file taking precedence over more general ones.

This layered approach means you can establish broad conventions at the project root and then provide more specific guidance in subdirectories. For example, your root project memory might establish general coding standards, while a frontend-specific memory file might add additional guidelines about component structure and styling approaches.

## Memory File Structure and Best Practices

### Writing Effective Memory Content

The most effective memory files balance specificity with readability. Rather than writing vague instructions like "write good code," effective memory files provide specific, actionable guidance like "use dependency injection for service classes and include comprehensive JSDoc comments for all public methods."

Consider organizing your memory files using clear Markdown headings that group related concepts together. This structure makes the files easier to scan and helps Claude understand the relationships between different pieces of information. For instance, you might have sections for coding standards, testing approaches, deployment procedures, and architectural decisions.

When writing memory content, think about the context a new team member would need to be productive. Include not just what to do, but why certain decisions were made. This background helps Claude provide more nuanced assistance that aligns with your project's philosophy rather than just following mechanical rules.

### Structuring Memory for Maximum Effectiveness

Effective memory files follow a hierarchical structure that moves from general principles to specific implementation details. Start with high-level project goals and architectural decisions, then move into specific coding standards, testing requirements, and operational procedures.

Use descriptive headings that clearly indicate the scope and purpose of each section. For example, rather than a generic "Database" heading, use "Database Schema Conventions" or "Database Query Optimization Guidelines." This specificity helps Claude understand exactly when and how to apply different pieces of guidance.

Consider including examples within your memory files, especially for complex or nuanced guidelines. When you specify a particular pattern or approach, show a brief example of what that looks like in practice. This helps Claude provide more accurate and helpful suggestions that match your intended implementation style.

### Managing Memory File Growth

As projects evolve, memory files can grow quite large. Rather than allowing them to become unwieldy, consider strategies for keeping them organized and maintainable. One effective approach involves breaking complex topics into focused sections with clear boundaries.

When memory files become too large to scan easily, consider whether some content might be better suited for separate documentation files that your memory file references. The memory file should contain the essential context Claude needs to provide immediate assistance, while detailed implementation guides might live in separate documentation that team members can reference when needed.

Regularly review and update your memory files as your project evolves. Outdated guidance can lead to inconsistent suggestions or recommendations that no longer align with current project practices. Treat memory files as living documentation that requires periodic maintenance.

## Practical Memory Management Techniques

### Adding Memory During Development Sessions

Claude Code provides several convenient ways to add memory content during active development sessions. The quickest method involves starting any input with the `#` character, which signals Claude Code to treat your input as memory content rather than a regular request.

When you use this shortcut, Claude Code presents an interactive prompt asking which memory file should store the new information. This decision point encourages you to think about the appropriate scope for each piece of knowledge. Personal preferences belong in user memory, team conventions belong in project memory, and personal project-specific context belongs in local project memory.

This workflow integration means you can capture insights and decisions immediately when they occur, rather than trying to remember them later. When you discover a useful pattern or make an important architectural decision, you can immediately encode that knowledge into the appropriate memory file.

### Editing Memory Files Directly

For more extensive additions or reorganization, Claude Code's `/memory` command opens any memory file in your configured system editor. This approach works well when you need to restructure existing content, add substantial new sections, or perform detailed editing that would be cumbersome through the chat interface.

The direct editing approach also allows you to leverage your editor's features for working with Markdown content, such as spell checking, formatting assistance, and plugin support. This can be particularly valuable when creating comprehensive memory files for large projects.

When editing memory files directly, consider the impact on any ongoing Claude Code sessions. Memory files are loaded when Claude Code starts, so changes made during a session won't take effect until you restart Claude Code or explicitly reload the memory.

### Memory File Synchronization and Sharing

Project memory files should be committed to version control alongside your code, allowing team members to benefit from shared knowledge and ensuring that memory files evolve alongside the project. This creates a collaborative knowledge base that improves over time as team members contribute their insights and discoveries.

When working in teams, establish conventions for how memory files should be updated. Consider implementing review processes for significant changes to project memory files, just as you would for code changes. This helps maintain quality and ensures that memory files accurately reflect team consensus rather than individual preferences.

Local memory files should remain local to each developer's environment. Use `.gitignore` entries to prevent accidentally committing these personal files to shared repositories. This separation allows each team member to maintain personal productivity enhancements without affecting others' workflows.

## Advanced Memory Strategies

### Creating Hierarchical Memory Systems

In large, complex projects, consider creating hierarchical memory systems that reflect your project's structure. This might involve root-level memory files for overall project conventions, service-specific memory files for microservices architectures, or feature-specific memory files for large monoliths.

This hierarchical approach allows you to provide increasingly specific guidance as Claude Code works in different parts of your codebase. General coding standards apply everywhere, while specific implementation patterns might only apply to particular services or features.

When designing hierarchical memory systems, ensure that more specific memory files build upon rather than contradict more general ones. The goal is progressive refinement of guidance, not conflicting instructions that might confuse Claude's assistance.

### Memory Files for Different Development Phases

Consider how your memory files might need to adapt for different phases of development. Early-stage projects might focus on architectural decisions and broad conventions, while mature projects might emphasize maintenance procedures and optimization guidelines.

You might maintain separate memory files or sections for different types of work. Development-focused memory might emphasize coding standards and testing approaches, while operations-focused memory might emphasize deployment procedures and monitoring requirements.

This phase-aware approach helps ensure that Claude's assistance remains relevant and valuable as your project evolves from initial development through long-term maintenance.

### Memory Files as Documentation Strategy

Well-crafted memory files serve dual purposes as both Claude Code configuration and project documentation. This dual role can streamline your documentation efforts while ensuring that guidance remains current and actionable.

When memory files serve as documentation, they naturally stay updated because outdated information directly impacts development productivity. This creates a positive feedback loop where maintaining accurate memory files provides immediate benefits to daily development work.

Consider how memory files might complement or replace other forms of project documentation. While detailed API documentation or architectural diagrams might live elsewhere, the essential context for day-to-day development decisions can live effectively within memory files.

## Troubleshooting Common Memory Issues

### When Memory Doesn't Seem to Load

If Claude Code doesn't seem to be using your memory files, start by verifying the file locations and names. Memory files must be named exactly `CLAUDE.md` or `CLAUDE.local.md` and must be located in the expected directories. Case sensitivity matters on many filesystems, so ensure the filename casing matches exactly.

Check that your memory files contain valid Markdown content. While Claude Code is generally tolerant of formatting variations, severely malformed Markdown might prevent proper loading. Test your memory files by viewing them in a Markdown preview tool to ensure they render correctly.

Verify that Claude Code is starting from the directory you expect. The recursive search begins from your current working directory, so if you're running Claude Code from an unexpected location, it might not find your project memory files.

### Resolving Conflicting Memory Guidance

When memory files contain conflicting guidance, Claude Code follows the precedence hierarchy with more specific files overriding more general ones. However, conflicting guidance within the same memory file or across files at the same level can create confusion.

Review your memory files for internal consistency, ensuring that different sections don't provide contradictory guidance. When you discover conflicts, resolve them by clarifying the specific contexts where different approaches should be used.

Consider using explicit conditional language in memory files when different approaches apply to different situations. Rather than providing absolute rules, specify when and where particular guidelines apply. This helps Claude understand the nuanced decision-making that experienced developers naturally apply.

### Managing Memory File Performance

Very large memory files can impact Claude Code's performance and effectiveness. If your memory files become unwieldy, consider strategies for keeping them focused and manageable.

Focus memory files on the information Claude needs for immediate decision-making rather than comprehensive documentation that might be better suited for separate files. Link to detailed documentation when appropriate, but keep the memory files focused on actionable guidance.

Regularly review memory files to remove outdated information and consolidate redundant guidance. This maintenance keeps memory files effective while preventing them from becoming overwhelming or difficult to navigate.

## Memory Files in Different Development Contexts

### Memory Files for Solo Projects

When working alone, memory files serve primarily as consistency tools that help maintain coherent approaches across development sessions. Solo project memory files might focus on personal coding standards, preferred libraries, and decision rationales that help maintain consistency over time.

Solo developers can use memory files to capture learning and insights that might otherwise be forgotten. When you discover useful patterns or solve complex problems, encoding that knowledge in memory files makes it available for future reference and similar situations.

Consider using memory files to maintain personal development standards that you want to apply consistently across projects. This helps develop and maintain good practices even when working without team oversight or code review processes.

### Memory Files for Team Projects

Team memory files require more careful consideration of shared conventions and collaborative workflows. Focus on decisions and standards that affect team productivity and code consistency rather than individual preferences.

Establish team processes for updating and maintaining memory files. Consider assigning ownership of different sections to appropriate team members and implementing review processes for significant changes.

Use team memory files to capture institutional knowledge that might otherwise be lost when team members leave or transition to different roles. This includes not just technical decisions but also the reasoning behind those decisions and the contexts that influenced them.

### Memory Files for Open Source Projects

Open source projects can use memory files to help contributors understand project conventions and philosophy. These files serve as living style guides that help maintain consistency across diverse contributor communities.

Consider how memory files might help new contributors get started more quickly by providing clear guidance about code organization, testing requirements, and contribution standards. This can reduce the overhead of code review and help maintain project quality.

Balance the specificity of memory files with the diverse backgrounds and preferences of open source contributors. Focus on essential conventions that maintain project coherence while allowing flexibility for different approaches within those constraints.

## The Future of Your Memory System

As you develop experience with CLAUDE.md files, you'll discover patterns and approaches that work particularly well for your projects and development style. The memory system is designed to evolve with your needs, supporting both simple single-file approaches and sophisticated hierarchical systems.

Consider how your memory files might serve as a foundation for other development tools and processes. The knowledge you encode in memory files might inform code review checklists, documentation standards, or onboarding procedures.

The most effective memory systems grow organically from actual development needs rather than theoretical best practices. Start simple with basic conventions and preferences, then expand your memory files as you discover areas where additional guidance would improve consistency and productivity.

Remember that memory files are tools to enhance your development workflow, not rigid constraints that limit creativity or problem-solving. The goal is to provide Claude Code with enough context to offer relevant, helpful assistance while maintaining the flexibility to adapt to new challenges and requirements as they arise.