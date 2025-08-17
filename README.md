# n8n Workflow Studio 🚀

**English** | [한국어](README.ko.md)

<p align="center">
  <img src="https://img.shields.io/badge/n8n-workflow-blue" alt="n8n">
  <img src="https://img.shields.io/badge/MCP-enabled-green" alt="MCP">
  <img src="https://img.shields.io/badge/AI-powered-purple" alt="AI">
  <img src="https://img.shields.io/badge/license-MIT-blue" alt="License">
  <img src="https://img.shields.io/badge/PRs-welcome-brightgreen.svg" alt="PRs Welcome">
</p>

<p align="center">
  <strong>AI-powered n8n workflow development environment with MCP tools integration</strong>
</p>

## 🌟 Features

- **🤖 AI-Assisted Development**: Create n8n workflows with Claude Code and MCP tools
- **✅ Real-time Validation**: Validate nodes and workflows before deployment
- **📚 Smart Documentation**: Access up-to-date documentation for any library
- **🔍 Intelligent Search**: Find the right nodes and templates quickly
- **🎯 Pre-configured Templates**: Start with battle-tested workflow patterns
- **🌐 Multi-language Support**: English and Korean documentation

## 🚀 Quick Start

### Prerequisites

- [Claude Code](https://claude.ai/code) installed
- n8n instance (optional, for deployment)
- Node.js 18+ (for local MCP servers)

### Installation

#### 1. Clone the Repository

```bash
git clone https://github.com/yourusername/n8n-workflow-studio.git
cd n8n-workflow-studio
```

#### 2. Set Up MCP Tools

This project requires two essential MCP tools:

##### n8n-mcp (Required)
The core tool for n8n workflow development.

```bash
# Option 1: Local server (recommended - most stable)
claude mcp add n8n-mcp -- npx -y @czlonkowski/n8n-mcp

# Option 2: Project-scoped
claude mcp add n8n-mcp --scope project "npx @czlonkowski/n8n-mcp"
```

##### context7 (Required)
For library documentation and context management.

```bash
# Option 1: Remote server (HTTP - fastest setup)
claude mcp add --transport http context7 https://mcp.context7.com/mcp

# Option 2: SSE transport (real-time streaming)
claude mcp add --transport sse context7 https://mcp.context7.com/sse

# Option 3: Local server (offline capable)
claude mcp add context7 -- npx -y @upstash/context7-mcp
```

#### 3. Restart Claude Code

After installing MCP tools:
1. Completely close Claude Code
2. Reopen Claude Code
3. Open the project folder
4. Approve MCP servers when prompted

#### 4. Verify Installation

```bash
# In Claude Code
/mcp list

# Should display:
# - n8n-mcp
# - context7
```

## 📁 Project Structure

```
n8n-workflow-studio/
├── .mcp.json                          # MCP server configurations
├── .gitignore                         # Git ignore rules (excludes workflow folders)
├── README.md                          # This file (English)
├── README.ko.md                       # Korean documentation
├── CLAUDE.md                          # Development guidelines for Claude Code
├── make-workflow-instruction/         # Core development guides
│   ├── mcp-validation-patterns.md    # MCP validation patterns
│   ├── n8n-mcp-guide.md              # Primary MCP workflow process
│   ├── n8n-workflow-creator.md       # Korean workflow guide
│   └── n8n-workflow-reference.md     # Comprehensive n8n reference
├── example-workflow-structure/        # Example folder structure (tracked)
│   └── README.md                      # Structure documentation
└── [NN]-[workflow-name]/              # Your workflow folders (LOCAL ONLY - not tracked)
    ├── *.json                         # n8n workflow files
    └── *.md                           # Documentation files
```

> ⚠️ **Note**: Numbered workflow folders (`01-*/`, `02-*/`, etc.) are automatically excluded from Git and remain local to your machine for privacy and security.

## 🛠 Usage

### Creating a New Workflow

1. **Start with documentation**
   ```javascript
   tools_documentation()  // Always run first in new conversations
   ```

2. **Search for nodes**
   ```javascript
   search_nodes({query: 'webhook'})
   list_nodes({category: 'trigger', limit: 200})
   ```

3. **Validate configuration**
   ```javascript
   validate_node_minimal('nodes-base.webhook', {})
   validate_node_operation('nodes-base.slack', config, 'runtime')
   ```

4. **Build and validate workflow**
   ```javascript
   validate_workflow(workflow)
   validate_workflow_connections(workflow)
   ```

### Example Request to Claude Code

```
Create an email automation workflow using n8n-mcp tools.
Please follow the guides in make-workflow-instruction folder.
```

### Workflow Organization

- **Naming Convention**: `[NN]-[descriptive-name]/`
- **Numbering**: Sequential (01, 02, 03, ...)
- **Storage**: LOCAL ONLY (automatically excluded from Git)
- **Examples**:
  - `01-reddit-workflow/` - Reddit monitoring workflow
  - `02-email-automation/` - Email automation workflow
  - `03-data-pipeline/` - Data pipeline workflow

> 💡 **Privacy First**: Your workflows stay on your local machine and are never pushed to GitHub, protecting your business logic and sensitive data.

## 📚 Documentation

### In-Project Guides

- [MCP Validation Patterns](make-workflow-instruction/mcp-validation-patterns.md) - Common patterns and validation examples
- [n8n MCP Guide](make-workflow-instruction/n8n-mcp-guide.md) - Complete MCP tool usage guide
- [n8n Workflow Reference](make-workflow-instruction/n8n-workflow-reference.md) - Comprehensive n8n features reference

### External Resources

- [n8n-mcp GitHub](https://github.com/czlonkowski/n8n-mcp)
- [context7 GitHub](https://github.com/upstash/context7)
- [n8n Documentation](https://docs.n8n.io)
- [Claude Code MCP Documentation](https://docs.anthropic.com/en/docs/claude-code/mcp)

## 🔄 Example Workflows

### 01-reddit-workflow
Reddit community monitoring with Telegram notifications
- Monitors 13 AI/Tech subreddits
- Metadata-based score normalization
- AI quality filtering
- Automatic Telegram forwarding

## 🤝 Contributing

We welcome contributions! Please see our [Contributing Guidelines](CONTRIBUTING.md) for details.

### How to Contribute

1. Fork the repository
2. Create your feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit your changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

## 🐛 Troubleshooting

### MCP Tools Not Recognized

1. **Check current status**
   ```bash
   /mcp list
   ```

2. **Verify `.mcp.json` exists**
   ```bash
   cat .mcp.json
   ```

3. **Manual reinstall**
   ```bash
   # Reset project choices
   claude mcp reset-project-choices
   
   # Reinstall n8n-mcp
   claude mcp add n8n-mcp -- npx -y @czlonkowski/n8n-mcp
   
   # Reinstall context7
   claude mcp add --transport http context7 https://mcp.context7.com/mcp
   ```

4. **Clear caches if needed**
   ```bash
   npx clear-npx-cache
   npm cache clean --force
   ```

### Workflow Validation Errors

1. Use `validate_node_minimal()` first
2. Check required fields
3. Verify connection structure
4. Validate expression syntax

## 🗺 Roadmap

- [ ] Visual workflow builder integration
- [ ] More pre-built workflow templates
- [ ] Enhanced AI suggestions
- [ ] Workflow marketplace integration
- [ ] Performance optimization tools
- [ ] Advanced debugging features

## 📊 Stats

- **525** total nodes available
- **263** AI-capable nodes
- **104** trigger nodes
- **87%** documentation coverage
- **399** community templates

## 📄 License

MIT License - see the [LICENSE](LICENSE) file for details.

## 💬 Support

- [GitHub Issues](https://github.com/yourusername/n8n-workflow-studio/issues) - Bug reports and feature requests
- [Discussions](https://github.com/yourusername/n8n-workflow-studio/discussions) - Questions and ideas
- [Discord Community](https://discord.gg/n8n) - Real-time chat with the community

## 🌟 Star History

If this project helps you, please give it a ⭐!

[![Star History Chart](https://api.star-history.com/svg?repos=yourusername/n8n-workflow-studio&type=Date)](https://star-history.com/#yourusername/n8n-workflow-studio&Date)

## 🙏 Acknowledgments

- [n8n](https://n8n.io) - The workflow automation platform
- [Claude Code](https://claude.ai/code) - AI-powered code assistant
- [MCP](https://modelcontextprotocol.io) - Model Context Protocol
- All contributors and community members

---

<p align="center">
  Made with ❤️ by the n8n community
</p>