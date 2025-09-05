---

## 🤖 AI Assistant Instructions

When working with this codebase:

1. **Always refer to this CLAUDE.md** for context and conventions
2. **Follow the established patterns** shown in the examples above
3. **Include proper error handling** and logging in all code
4. **Write comprehensive tests** for new features
5. **Update documentation** when adding new functionality
6. **Consider performance implications** of all implementations

### 📋 Work Process Requirements

**MANDATORY workflow for all development tasks:**

1. **Start with TODO Planning**: Always begin by creating a comprehensive TODO list using the TodoWrite tool that includes:
   - All planned implementation steps
   - Clear explanation of what work will be done and why
   - Expected outcomes and deliverables for each step

2. **Step-by-Step Execution**: Complete each TODO item individually:
   - Mark current task as "in_progress" before starting
   - Complete the work for that specific step
   - Mark task as "completed" when finished
   - **STOP and report**: Explain what was accomplished and how to test it
   - Wait for user confirmation before continuing to next step
   - **ALWAYS mark the step as completed✅**, after user confirm to continue

3. **Commit Before Continue**: When user asks to continue work:
   - **ALWAYS create a git commit first** to save previous work
   - Use descriptive commit messages following established patterns
   - Then proceed with next planned TODO item

4. **Testing Instructions**: For each completed step, provide:
   - Clear instructions on how to test the implemented functionality
   - Expected behavior and outcomes
   - Any prerequisites or setup needed for testing

This process ensures transparency, allows for iterative feedback, and maintains a clean git history with logical commit boundaries.

### 🔗 Shared Context Documentation

**MANDATORY for all inter-service communication:**

**Use `@shared/context.md` as the single source of truth** for cross-system information:

1. **Before implementing inter-service features**: Always check `@shared/context.md` first
   - API schemas and endpoints
   - Data models and interfaces
   - Service communication patterns
   - Configuration requirements

2. **When creating/updating inter-service components**: Update the relevant section in `@shared/context.md`
   - Frontend team documents UI state management and component APIs
   - Backend team documents REST/GraphQL APIs, database schemas
   - Database team documents the database schema
   - Everyone documents the configuration changes, like api endpoint or port

3. **Context.md Structure Requirements**:
   - Organize by service/component
   - Include API schemas with examples
   - Document data flow patterns
   - Specify configuration dependencies
   - Maintain version compatibility notes

4. **Update Responsibility**:
   - **Service owners**: Update their section when making changes
   - **Cross-cutting changes**: Update all affected sections
   - **Breaking changes**: Document migration paths and deprecation timelines

**Example Usage:**
- Frontend needs backend API schema → Check `@shared/context.md` Backend APIs section
- Backend needs AI service interface → Check `@shared/context.md` AI Service section
- Memory service needs RAG data format → Check `@shared/context.md` RAG Pipeline section

This eliminates the need to dive into other services' codebases and ensures consistent, up-to-date interface documentation.

Remember: This is a multi-phase project. Consider which phase you're implementing for and ensure compatibility with the overall architecture vision.
