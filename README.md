# n8n Workflow Studio 🚀

**English** | [한국어](README.ko.md)

<p align="center">
  <img src="https://img.shields.io/badge/n8n-workflow-blue" alt="n8n">
  <img src="https://img.shields.io/badge/MCP-enabled-green" alt="MCP">
  <img src="https://img.shields.io/badge/AI-powered-purple" alt="AI">
  <img src="https://img.shields.io/badge/license-MIT-blue" alt="License">
</p>

# n8n MCP Workflow Development Project

## 📌 Project Overview

This project is a template repository for efficiently developing and managing n8n workflows using **n8n-MCP (Model Context Protocol)** tools. It enables AI-assisted workflow development through Claude Code and MCP tools.

## 🚀 Quick Start Guide

> **Important**: This section is a complete guide for setting up the project on a new PC.
> Claude Code agents can reference this section to install and configure MCP tools.

### 1. MCP Tools Setup

This project uses two essential MCP tools:

#### n8n-mcp (Required)
- **Purpose**: n8n workflow creation and management tool
- **GitHub**: [https://github.com/czlonkowski/n8n-mcp](https://github.com/czlonkowski/n8n-mcp)
- **Features**: 
  - Node search and exploration
  - Workflow validation
  - Template management
  - AI-assisted workflow creation
- **Installation Commands**:
  ```bash
  # Method 1: Local server connection (recommended - most stable)
  claude mcp add n8n-mcp -- npx -y @czlonkowski/n8n-mcp
  
  # Method 2: Project scope (project-specific management)
  claude mcp add n8n-mcp --scope project "npx @czlonkowski/n8n-mcp"
  ```

#### context7 (Required)
- **Purpose**: Library documentation and context management tool
- **GitHub**: [https://github.com/upstash/context7](https://github.com/upstash/context7)
- **Features**:
  - Latest library documentation
  - Code examples and references
  - Development context maintenance
- **Installation Commands**:
  ```bash
  # Method 1: Remote server connection (HTTP - fastest setup)
  claude mcp add --transport http context7 https://mcp.context7.com/mcp
  
  # Method 2: SSE transport (real-time streaming)
  claude mcp add --transport sse context7 https://mcp.context7.com/sse
  
  # Method 3: Local server connection (offline capable)
  claude mcp add context7 -- npx -y @upstash/context7-mcp
  ```

#### Automatic vs Manual Setup

**Automatic Setup** (when `.mcp.json` file exists):
- Project already includes `.mcp.json` file
- MCP tools automatically activate when Claude Code restarts
- No additional installation commands needed

**Manual Setup** (new environment or when `.mcp.json` is missing):
- Execute the installation commands above
- Choose one method for each tool
- Claude Code restart required after installation

### 2. Claude Code Restart
To activate MCP tools, you must restart Claude Code:
1. Close Claude Code
2. Restart Claude Code
3. Open the project folder
4. Approve MCP servers when prompted

## 📁 Project Structure

```
make-n8n-workflow/
├── .mcp.json                          # MCP tools configuration file
├── .gitignore                         # Git ignore rules (excludes workflow folders)
├── README.md                          # English documentation (main)
├── README.ko.md                       # Korean guide
├── CLAUDE.md                          # Claude Code development guidelines
├── make-workflow-instruction/         # n8n development guide documents
│   ├── mcp-validation-patterns.md    # MCP validation patterns
│   ├── n8n-mcp-guide.md              # n8n-MCP tool usage guide
│   ├── n8n-workflow-creator.md       # Korean workflow creation guide
│   └── n8n-workflow-reference.md     # n8n features reference
├── example-workflow-structure/        # Example folder structure (included in Git)
│   └── README.md                      # Structure documentation
└── [number]-[workflow-name]/          # User workflow folders (local only - Git excluded)
    ├── *.json                         # n8n workflow files
    └── *.md                           # Workflow documentation files
```

> ⚠️ **Note**: Numbered workflow folders (`01-*/`, `02-*/`, etc.) are automatically excluded from Git and stored only on your local computer.

### Workflow Folder Management Rules

- **Numbering System**: `01-`, `02-`, `03-` ... sequential numbering
- **Folder Names**: `[number]-[descriptive-name]` format
- **Storage Location**: Local only (not pushed to Git)
- **Examples**: 
  - `01-reddit-workflow/` - Reddit monitoring workflow
  - `02-email-automation/` - Email automation workflow
  - `03-data-pipeline/` - Data pipeline workflow

> 💡 **Privacy First**: Your workflows are stored only on your local computer, protecting your business logic and sensitive data.

## 🛠 Workflow Development Guide

### Development Process Using MCP Tools

1. **Check Documentation**
   - Reference guide documents in `make-workflow-instruction/` folder
   - Follow the process in `n8n-mcp-guide.md` especially

2. **Create Workflow**
   ```
   Example request to Claude:
   "Please create an email automation workflow using n8n-mcp tools.
   Please refer to the guides in the make-workflow-instruction folder."
   ```

3. **Save Workflow**
   - Save new workflows in new numbered folders
   - Manage with related documentation

### Claude Code Usage Tips

1. **Check MCP Tools**
   ```
   /mcp list
   ```

2. **Start Workflow Development**
   - Check n8n-mcp tool documentation first: `tools_documentation()`
   - Search nodes: `search_nodes()`
   - Validate workflow: `validate_workflow()`

3. **Use Guide Documents**
   - Always reference documents in `make-workflow-instruction/` folder
   - Use `n8n-workflow-creator.md` for Korean work

## 📚 Reference Documentation

### In-Project Documents
- `make-workflow-instruction/n8n-mcp-guide.md` - Detailed MCP tool guide
- `make-workflow-instruction/n8n-workflow-creator.md` - Korean workflow creation guide
- `make-workflow-instruction/n8n-workflow-reference.md` - Complete n8n features reference

### External Resources
- [n8n-mcp GitHub](https://github.com/czlonkowski/n8n-mcp)
- [context7 GitHub](https://github.com/upstash/context7)
- [n8n Official Documentation](https://docs.n8n.io)
- [Claude Code MCP Documentation](https://docs.anthropic.com/en/docs/claude-code/mcp)

## 🔄 Workflow Examples

### 01-reddit-workflow
Reddit community monitoring and Telegram notification workflow
- Monitors 13 AI/Tech subreddits in rotation
- Metadata-based score normalization
- AI quality filtering
- Automatic Telegram forwarding

## 🤝 Collaboration Guide

### Using the Project on Another PC (Complete Guide)

#### Step 1: Clone Repository
```bash
git clone [repository URL]
cd make-n8n-workflow
```

#### Step 2: Check `.mcp.json` File
```bash
# Check if file exists
ls -la .mcp.json
```

#### Step 3: Install MCP Tools

**Case A: When `.mcp.json` file exists**
1. Restart Claude Code
2. Open project folder
3. Select "Approve" in MCP server approval prompt
4. Tools automatically activate

**Case B: When `.mcp.json` file is missing or manual installation is needed**

```bash
# Required tool 1: Install n8n-mcp
claude mcp add n8n-mcp -- npx -y @czlonkowski/n8n-mcp

# Required tool 2: Install context7 (choose one below)
# Option A: Remote server (requires internet, fastest)
claude mcp add --transport http context7 https://mcp.context7.com/mcp

# Option B: Local server (offline capable)
claude mcp add context7 -- npx -y @upstash/context7-mcp
```

#### Step 4: Restart Claude Code
1. Completely close Claude Code (close all windows)
2. Restart Claude Code
3. Open project folder

#### Step 5: Verify MCP Tools
```bash
# Run inside Claude Code
/mcp list

# Should display:
# - n8n-mcp
# - context7
```

#### Step 6: Installation Verification
Enter the following message in Claude Code:
```
Please check if n8n-mcp tools are properly installed.
Please run the tools_documentation() command.
```

#### Step 7: Start Development
- Reference development guidelines in CLAUDE.md file
- Use guide documents in make-workflow-instruction/ folder
- Create new workflows in numbered folders

## ⚠️ Important Notes

1. **MCP Tools Activation**
   - Claude Code restart is mandatory
   - Check project scope settings

2. **Workflow Validation**
   - Always run `validate_workflow()` before deployment
   - Include error handling logic

3. **Folder Structure Compliance**
   - New workflows must be saved in numbered folders
   - Manage with related documentation

## 👥 Contributing

Contributions are welcome! Please refer to our [Contributing Guidelines](CONTRIBUTING.md).

## 📝 License

MIT License - see the [LICENSE](LICENSE) file for details.

## 🆘 Troubleshooting

### When MCP Tools Are Not Recognized

#### Diagnostic Steps
1. **Check Current Status**
   ```bash
   # Inside Claude Code
   /mcp list
   ```

2. **Check `.mcp.json` File**
   ```bash
   cat .mcp.json
   ```

3. **Manual Reinstallation**
   ```bash
   # Reset existing settings
   claude mcp reset-project-choices
   
   # Reinstall n8n-mcp
   claude mcp add n8n-mcp -- npx -y @czlonkowski/n8n-mcp
   
   # Reinstall context7
   claude mcp add --transport http context7 https://mcp.context7.com/mcp
   ```

4. **Complete Claude Code Restart**
   - Close all Claude Code windows
   - Check Claude processes in task manager
   - Restart Claude Code

5. **Resolve Permission Issues**
   ```bash
   # Clear npx cache
   npx clear-npx-cache
   
   # Clear npm cache
   npm cache clean --force
   ```

### Workflow Validation Errors
1. Run `validate_node_minimal()` first
2. Check required fields
3. Verify connection structure
4. Check expression syntax

## 🔄 Update History

- 2025.01: Project structure improvement and MCP tools integration
- 2025.01: Reddit workflow example added
- 2025.01: Multilingual guide documents added

## 💬 Support and Community

- [GitHub Issues](https://github.com/yourusername/n8n-workflow-studio/issues) - Bug reports and feature requests
- [Discussions](https://github.com/yourusername/n8n-workflow-studio/discussions) - Questions and idea sharing

## 🌟 Star This Project

If this project helped you, please give it a ⭐!