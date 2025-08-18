# n8n Workflow Studio 🚀

**English** | [한국어](README.ko.md)

AI-powered n8n workflow development environment with MCP tools integration for creating, validating, and managing workflows through Claude Code.

## 🚀 Quick Start

### Installation

1. **Clone the repository**
   ```bash
   git clone https://github.com/yourusername/n8n-workflow-studio.git
   cd n8n-workflow-studio
   ```

2. **Install MCP tools**
   ```bash
   # Install n8n-mcp (core workflow tool)
   claude mcp add n8n-mcp -- npx n8n-mcp
   
   # Install context7 (documentation tool)
   claude mcp add --transport http context7 https://mcp.context7.com/mcp
   ```

3. **Restart Claude Code completely** (critical for MCP tools to work)

4. **Verify installation**
   ```bash
   /mcp list  # Should show: n8n-mcp, context7
   ```

## 📁 Project Structure

```
n8n-workflow-studio/
├── CLAUDE.md                          # Development guidelines
├── make-workflow-instruction/         # Core development guides
└── [NN]-[workflow-name]/              # Your workflows (local only)
```

> Workflow folders are excluded from Git for privacy.

## 🛠 Usage

Ask Claude Code to create workflows:
```
Create an email automation workflow using n8n-mcp tools.
```

Workflows are organized as: `01-workflow-name/`, `02-another-workflow/`, etc.

## 📚 Documentation

- [n8n MCP Guide](make-workflow-instruction/n8n-mcp-guide.md) - Complete usage guide
- [n8n Workflow Reference](make-workflow-instruction/n8n-workflow-reference.md) - Feature reference

## 🐛 Troubleshooting

**MCP tools not working?**
1. Check: `/mcp list` should show `n8n-mcp` and `context7`
2. Try: `claude mcp reset-project-choices` then reinstall
3. Ensure: Complete Claude Code restart after installation

## 📄 License

MIT License