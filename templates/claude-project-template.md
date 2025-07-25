# [Project Name] Development Guide

## Project Overview
[Brief description of what this project does]
[Target audience and main use cases]
[Key business requirements]

## Architecture Decisions
### Overall Architecture
[Describe the high-level architecture]
[Example: Microservices with API Gateway pattern]

### Technology Stack
- Runtime: .NET [version]
- Framework: ASP.NET Core [version]
- Database: [Database choice and version]
- Message Queue: [If applicable]
- Cache: [If applicable]

## C# Coding Standards
### Naming Conventions
- Classes: PascalCase (e.g., CustomerService)
- Interfaces: IPascalCase (e.g., IRepository)
- Methods: PascalCase (e.g., GetCustomerById)
- Private fields: _camelCase (e.g., _customerRepository)
- Parameters/locals: camelCase (e.g., customerId)

### Code Organization
- One class per file
- Namespace matches folder structure
- Related classes grouped in folders
- [Specific organization patterns for this project]

### C# Language Features
- Target C# version: [version]
- Nullable reference types: [enabled/disabled]
- Pattern matching: [usage guidelines]
- LINQ usage: [preferences]
- Async/await patterns: [specific patterns used]

### Dependency Injection
[DI container choice and configuration patterns]
[Service lifetime conventions]

## Testing Strategy
### Unit Testing
- Framework: [xUnit/NUnit/MSTest]
- Naming: MethodName_Scenario_ExpectedResult
- Mocking: [Moq/NSubstitute preferences]
- Coverage target: [percentage]

### Integration Testing
[Integration testing approach]
[Test data management strategy]

## Error Handling
### Exception Strategy
[When to throw vs return error codes]
[Custom exception types and usage]
[Logging requirements for exceptions]

### Validation Approach
[Input validation strategy]
[Business rule validation patterns]

## Database Conventions
### Entity Framework Patterns
[Code-first vs database-first]
[Migration strategy]
[Repository pattern usage]

### SQL Naming
[Table and column naming conventions]
[Stored procedure conventions if used]

## API Design
### RESTful Conventions
[URL patterns and naming]
[HTTP verb usage]
[Status code standards]

### API Versioning
[Versioning strategy]
[Backward compatibility requirements]

## Security Requirements
[Authentication approach]
[Authorization patterns]
[Data protection requirements]
[Specific security concerns for this domain]

## Performance Considerations
[Performance targets and SLAs]
[Caching strategies]
[Known bottlenecks and mitigations]

## Deployment
### Environments
- Development: [details]
- Staging: [details]
- Production: [details]

### CI/CD Pipeline
[Build process overview]
[Deployment strategy]
[Rollback procedures]

## Common Gotchas
[Project-specific issues to watch out for]
[Historical decisions that might seem odd]
[Areas that need refactoring]
