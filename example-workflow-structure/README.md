# Workflow Folder Structure Example

This is an example of how your workflow folders should be structured.

## Folder Naming Convention

```
[NN]-[descriptive-name]/
├── workflow.json           # The n8n workflow file
├── README.md              # Documentation for this workflow
├── test-data/             # Sample data for testing (optional)
│   └── sample.json
└── assets/                # Screenshots or diagrams (optional)
    └── workflow-diagram.png
```

## Examples

- `01-reddit-monitoring/`
- `02-email-automation/`
- `03-data-pipeline/`
- `04-slack-integration/`
- `05-api-webhook/`

## Important Notes

1. **These folders are LOCAL ONLY** - They will not be pushed to GitHub
2. Keep your workflows organized with sequential numbering
3. Always include a README.md in each workflow folder
4. Store any sensitive data or credentials in environment variables, not in the workflow files

## Creating a New Workflow Folder

```bash
# Example: Creating a new workflow folder
mkdir 01-my-first-workflow
cd 01-my-first-workflow
touch workflow.json
touch README.md
```