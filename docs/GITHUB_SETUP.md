# GitHub Actions Setup Guide

This guide will help you set up the necessary secrets and permissions for the GitHub Actions workflows.

## Required Secrets

You need to configure the following secrets in your GitHub repository:

### 1. ANTHROPIC_API_KEY
Your Anthropic API key for Claude.

**How to get it:**
1. Go to https://console.anthropic.com/
2. Create an account or sign in
3. Navigate to API Keys
4. Create a new API key

### 2. PAT_TOKEN (Personal Access Token)
A GitHub Personal Access Token with the necessary permissions.

**How to create it:**
1. Go to GitHub Settings → Developer settings → Personal access tokens → Tokens (classic)
2. Click "Generate new token (classic)"
3. Give it a descriptive name like "agentic-mkt-mu-actions"
4. Select the following scopes:
   - `repo` (Full control of private repositories)
   - `workflow` (Update GitHub Action workflows)
   - `write:packages` (Upload packages to GitHub Package Registry)
   - `read:org` (Read org and team membership, read org projects)
5. Click "Generate token"
6. Copy the token immediately (you won't see it again!)

## Adding Secrets to Your Repository

1. Go to your repository on GitHub
2. Click on **Settings** → **Secrets and variables** → **Actions**
3. Click **New repository secret**
4. Add each secret:
   - Name: `ANTHROPIC_API_KEY`
   - Value: Your Anthropic API key
   
   - Name: `PAT_TOKEN`
   - Value: Your GitHub Personal Access Token

## Verifying the Setup

After adding the secrets:

1. Create a new issue or PR
2. Comment with `@claude` to trigger the Claude assistant
3. Check the Actions tab to see if the workflow runs successfully

## Troubleshooting

### "Actor has insufficient permissions" error
- Ensure your PAT_TOKEN has the correct scopes
- Check that the workflow file has the correct permissions block

### "Bad credentials" error
- Regenerate your PAT_TOKEN
- Ensure the secret name matches exactly (case-sensitive)

### Claude doesn't respond
- Check if the workflow is triggered (look in Actions tab)
- Ensure the trigger phrase `@claude` is used correctly
- Verify ANTHROPIC_API_KEY is set correctly

## Security Best Practices

1. **Rotate tokens regularly** - Update your PAT_TOKEN every 90 days
2. **Use least privilege** - Only grant necessary permissions
3. **Monitor usage** - Check the Actions tab for unexpected runs
4. **Limit token scope** - Use repository-specific tokens when possible

## Additional Configuration

### Custom Trigger Phrase
To change the trigger phrase from `@claude` to something else, modify the workflow:

```yaml
- uses: anthropics/claude-code-action@v0.0.7
  with:
    trigger_phrase: "@ai-assistant"  # Your custom phrase
```

### Limiting Claude's Tools
You can restrict which tools Claude can use:

```yaml
- uses: anthropics/claude-code-action@v0.0.7
  with:
    allowed_tools: ["read_file", "list_files", "search_files"]
```

For more information, see the [Claude Code Action documentation](https://github.com/anthropics/claude-code-action).