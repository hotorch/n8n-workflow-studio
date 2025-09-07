# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Repository Overview

This repository is a comprehensive n8n workflow development environment that leverages **MCP (Model Context Protocol) tools** for AI-assisted workflow creation and management. It combines documentation resources with practical workflow examples and development tools.

**⚠️ IMPORTANT FOR AGENTS**: If you're working on a new machine or MCP tools are not available, **YOU MUST READ README.md FIRST** for complete installation instructions. The README contains all necessary setup commands and troubleshooting steps.

## MCP Tools Integration

### Required MCP Servers

This project utilizes two essential MCP servers:

1. **n8n-mcp** - Core tool for n8n workflow development
   - Provides node discovery, validation, and workflow management
   - Enables AI-assisted workflow creation

2. **context7** - Library documentation and context management
   - Provides up-to-date documentation for any library
   - Helps maintain development context across sessions

### MCP Installation Required?

**IMPORTANT**: If MCP tools are not available or working:
- **Refer to README.md** for complete installation instructions
- The README contains all necessary installation commands and setup steps
- Follow the "MCP 도구 설정" section in README.md for detailed guidance

```bash
# To check the installation guide:
cat README.md
# Look for "MCP 도구 설정" section
```

### MCP Setup Verification

Always verify MCP tools are available before starting n8n development:
- Check `.mcp.json` exists in project root
- Ensure Claude Code has been restarted after MCP configuration
- Confirm MCP servers are approved for use
- Run `/mcp list` to verify tools are loaded

### Working on a New Machine?

If you're setting up this project on a new machine or MCP tools are not available:

**→ READ README.md FIRST**

The README.md file contains:
- Complete MCP installation instructions
- Both automatic and manual setup methods
- Troubleshooting steps
- All necessary commands for both n8n-mcp and context7

```bash
# Read the installation guide
cat README.md | grep -A 50 "MCP 도구 설정"
```

**Do NOT proceed with workflow development until MCP tools are properly installed and verified.**

## Project Structure

```
make-n8n-workflow/
├── .mcp.json                          # MCP server configurations
├── README.md                          # User guide (Korean)
├── CLAUDE.md                          # This file (development guidelines)
├── make-workflow-instruction/         # Core development guides
│   ├── mcp-validation-patterns.md    # MCP validation patterns and examples
│   ├── n8n-mcp-guide.md              # Primary MCP workflow process
│   ├── n8n-workflow-creator.md       # Korean language workflow guide
│   └── n8n-workflow-reference.md     # Comprehensive n8n reference
└── [NN]-[workflow-name]/              # Numbered workflow folders
    ├── *.json                         # n8n workflow files
    └── *.md                           # Documentation files
```

## Workflow Organization

### Folder Naming Convention

- **Format**: `[NN]-[descriptive-name]/`
- **Numbering**: Sequential (01, 02, 03, ...)
- **Examples**:
  - `01-reddit-workflow/`
  - `02-email-automation/`
  - `03-data-pipeline/`

### Creating New Workflows

When creating a new workflow:
1. Find the next available number
2. Create folder with format: `[NN]-[workflow-name]/`
3. Place all related files in the folder
4. Include a README.md documenting the workflow

## Development Process with n8n-MCP

### Core Workflow Development Process

**ALWAYS follow this sequence when developing n8n workflows:**

1. **Start with Documentation**
   ```javascript
   tools_documentation()  // Always run first in new conversations
   ```

2. **Discovery Phase**
   - Think deeply about user request and clarify intent if needed
   - Use `search_nodes()` to find appropriate nodes
   - Use `list_nodes()` to browse categories
   - Use `list_ai_tools()` for AI-capable nodes (remember: ANY node can be an AI tool!)
   - Reference `make-workflow-instruction/n8n-mcp-guide.md` for patterns

3. **Configuration Phase**
   - Use `get_node_essentials()` for minimal properties (10-20 essential properties)
   - Use `search_node_properties()` to find specific properties
   - Get templates with `get_node_for_task()`
   - Use `get_node_documentation()` for human-readable docs when needed
   - **ALWAYS use MCP tools to get actual node structures - never hardcode**
   - Consider showing visual workflow architecture to user for feedback

4. **Pre-Validation Phase**
   - Use `validate_node_minimal()` for quick required fields check
   - Use `validate_node_operation()` for full operation-aware validation
   - Fix any validation errors before proceeding
   - Apply automatic fixes from validation responses

5. **Building Phase**
   - Create workflow using validated configurations from step 4
   - Connect nodes with proper structure
   - Add error handling appropriately
   - Use expressions like `$json`, `$node["NodeName"].json`
   - Use standard nodes over Code nodes when possible
   - Build workflow in an artifact for easy editing (unless user requests n8n instance creation)
   - **Reference `mcp-validation-patterns.md` for validation patterns**

6. **Workflow Validation Phase**
   - Run `validate_workflow()` for complete validation including connections
   - Check connections with `validate_workflow_connections()`
   - Verify expressions with `validate_workflow_expressions()`
   - Fix any issues found before deployment

7. **Deployment Phase** (if n8n API configured)
   - Deploy with `n8n_create_workflow()`
   - Use `n8n_validate_workflow({id: 'workflow-id'})` for post-deployment validation
   - Use `n8n_update_partial_workflow()` for incremental updates (80-90% token savings)
   - Test webhook workflows with `n8n_trigger_webhook_workflow()`

### Critical Development Rules

#### Never Hardcode - Always Use Dynamic Configuration
```javascript
// ❌ WRONG: Never hardcode versions or structures
const node = {
  typeVersion: 1.4,  // Don't guess!
  parameters: {
    options: {
      systemMessage: "..."  // Don't assume structure!
    }
  },
  credentials: {
    googleGenerativeAiApi: {...}  // Don't guess credential keys!
  }
}

// ✅ RIGHT: Get actual structure from MCP
const essentials = await get_node_essentials(nodeType)
const node = {
  typeVersion: essentials.version,  // Always current
  parameters: essentials.commonProperties,  // Real structure
  credentials: essentials.credentials  // Correct credential keys
}
```

#### Core Rules
- **ALWAYS use MCP tools**: Never hardcode versions, parameters, or structures
- **Reference guides in order**:
  1. `make-workflow-instruction/mcp-validation-patterns.md` - Validation patterns and examples
  2. `make-workflow-instruction/n8n-mcp-guide.md` - MCP tool usage
  3. `make-workflow-instruction/n8n-workflow-creator.md` - Korean workflow guide  
  4. `make-workflow-instruction/n8n-workflow-reference.md` - Technical reference
- **Validate early and often**: Pre-validate before building, post-validate after
- **Use templates**: Start with `get_node_for_task()` for common patterns
- **Apply auto-fixes**: Use validation.fixes from MCP responses
- **Prefer standard nodes**: Only use Code nodes when necessary
- **Use diff updates**: Leverage partial updates for efficiency (80-90% token savings)
- **Document everything**: Create README for each workflow

## Using Reference Documentation

### Priority Order for Documentation

1. **mcp-validation-patterns.md** - Validation patterns and common mistakes
2. **n8n-mcp-guide.md** - Primary process guide
3. **n8n-workflow-creator.md** - For Korean language requests
4. **n8n-workflow-reference.md** - For detailed feature reference

### When to Reference Each Guide

- **mcp-validation-patterns.md**: For validation examples and patterns
- **n8n-mcp-guide.md**: ALWAYS for new workflow development
- **n8n-workflow-creator.md**: When user requests in Korean or needs consulting
- **n8n-workflow-reference.md**: For advanced features and architecture

## Best Practices

### Workflow Design Principles

- Sequential processing for step-by-step data flow
- Conditional branching using IF/Switch nodes
- Parallel execution for concurrent operations
- Merge patterns for synchronizing branches
- Error handling with Error Trigger nodes
- Reusable workflows via Execute Workflow nodes

### Code Quality Standards

- **Always validate with MCP tools** - Use `validate_node_operation()` and `validate_workflow()`
- **Get actual structures** - Use `get_node_essentials()` instead of guessing
- **Check credential keys** - Verify actual credential names in essentials
- Use descriptive node names
- Add Sticky Notes for complex sections
- Implement proper error handling (Continue On Fail, Error Trigger)
- Test workflows thoroughly before saving
- Use batching for high-volume processing

### Validation Strategy

#### Before Building:
1. `validate_node_minimal()` - Check required fields
2. `validate_node_operation()` - Full configuration validation
3. Fix all errors before proceeding

#### After Building:
1. `validate_workflow()` - Complete workflow validation
2. `validate_workflow_connections()` - Structure validation
3. `validate_workflow_expressions()` - Expression syntax check

#### After Deployment:
1. `n8n_validate_workflow({id})` - Validate deployed workflow
2. `n8n_list_executions()` - Monitor execution status
3. `n8n_update_partial_workflow()` - Fix issues using diffs

### AI Integration Guidelines

- Utilize LangChain nodes for AI-powered workflows
- Implement vector database integrations
- Build chatbots using Chat Trigger nodes
- Create AI agents that use n8n nodes as tools
- Design human-in-the-loop flows

## Error Handling Strategy

1. **Use Continue On Fail** options strategically
2. **Implement error branches** where appropriate
3. **Validate at multiple stages**:
   - Node-level validation
   - Workflow-level validation
   - Post-deployment validation
4. **Log errors appropriately** for debugging

## Security Considerations

- Never hardcode credentials in workflows
- Use n8n's credential management system
- Validate all external inputs
- Implement rate limiting where necessary
- Follow defensive programming practices
- Only assist with legitimate automation tasks

## Collaboration Guidelines

### When Working on Existing Workflows

1. Check the numbered folder for existing documentation
2. Review workflow structure before modifications
3. Validate changes don't break existing functionality
4. Update documentation after changes

### When Creating New Workflows

1. Follow folder naming convention strictly
2. Include comprehensive documentation
3. Add example data where helpful
4. Document any required credentials or setup

## Important Notes

- This is both a documentation and implementation project
- Always use MCP tools when available for n8n development
- Reference guides are authoritative - follow their patterns
- Maintain backward compatibility when updating workflows
- Focus on defensive security practices

## Command Reminders

### Essential n8n-MCP Commands

```javascript
// Always start with:
tools_documentation()

// Discovery:
search_nodes({query: 'email'})
list_nodes({category: 'trigger', limit: 200})  // Use limit:200 for all
list_ai_tools()  // 263 AI-optimized nodes

// Configuration:
get_node_essentials('nodes-base.slack')  // 10-20 essential properties
search_node_properties('nodes-base.httpRequest', 'auth')
get_node_for_task('send_slack_message')  // Pre-validated templates

// Pre-Validation:
validate_node_minimal('nodes-base.webhook', {})
validate_node_operation('nodes-base.slack', config, 'runtime')

// Workflow:
validate_workflow(workflow)  // Complete validation
validate_workflow_connections(workflow)  // Structure only
validate_workflow_expressions(workflow)  // Expressions only

// Deployment (if configured):
n8n_create_workflow(workflow)
n8n_validate_workflow({id: 'workflow-id'})
n8n_update_partial_workflow({workflowId: id, operations: [...]})
```

## Development Checklist

When developing any n8n workflow, ensure:

- [ ] MCP tools are available and working
- [ ] Started with `tools_documentation()` in new conversations
- [ ] Clarified user intent and requirements fully
- [ ] Referenced `mcp-validation-patterns.md` for validation patterns
- [ ] Used `get_node_essentials()` to get actual node structures
- [ ] Pre-validated with `validate_node_minimal()` before building
- [ ] Used `validate_node_operation()` for each node configuration
- [ ] Applied automatic fixes from validation responses
- [ ] Used `validate_workflow()` for complete workflow validation
- [ ] Fixed all validation errors before deployment
- [ ] Used proper folder structure (numbered folders)
- [ ] Created documentation for the workflow
- [ ] Tested error handling paths
- [ ] Used diff operations for updates (80-90% token savings)
- [ ] Followed security best practices

## Common Pitfalls to Avoid

### ❌ Never Do This:
- Hardcode `typeVersion` numbers
- Assume parameter structures (especially for LangChain nodes)
- Guess credential key names
- Deploy unvalidated workflows
- Use Code nodes when standard nodes exist
- Skip pre-validation phase

### ✅ Always Do This:
- Use `get_node_essentials()` for actual structures
- Validate before AND after building
- Apply MCP-provided fixes automatically
- Use templates from `get_node_for_task()`
- Test with `validate_workflow_expressions()`
- Use diff updates for modifications

## Korean Language Support

When user requests are in Korean:
1. Reference `make-workflow-instruction/n8n-workflow-creator.md` for Korean workflow guide
2. Follow the 2-phase process:
   - Phase 1: Requirements gathering and consulting
   - Phase 2: Workflow blueprint generation with MCP validation
3. Use the Workflow Prompt Framework to gather requirements systematically
4. Always validate with MCP tools before generating blueprints