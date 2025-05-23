# Contributing to Agentic Marketing Workflow System

Thank you for your interest in contributing to the Agentic Marketing Workflow System! This document provides guidelines for contributing to the project.

## 🤝 Code of Conduct

By participating in this project, you agree to maintain a respectful and inclusive environment for all contributors.

## 🚀 Getting Started

1. **Fork the repository** and clone it locally
2. **Set up your development environment**:
   ```bash
   cp .env.example .env
   # Fill in your credentials
   docker-compose up -d
   ```
3. **Create a feature branch**: `git checkout -b feature/your-feature-name`

## 📋 Contribution Guidelines

### Workflow Development

When creating or modifying n8n workflows:

1. **Follow naming conventions**:
   - Use descriptive names: `Agentic_Marketing___[Agent_Name].json`
   - Keep consistency with existing patterns

2. **Security best practices**:
   - Never commit API keys or credentials
   - Use n8n's credential system
   - Test for exposed secrets before committing

3. **Code quality**:
   - Validate JSON syntax before committing
   - Ensure proper error handling in all nodes
   - Add meaningful descriptions to complex nodes

### Commit Messages

Follow conventional commits format:
```
type(scope): description

[optional body]

[optional footer]
```

Types:
- `feat`: New feature
- `fix`: Bug fix
- `docs`: Documentation changes
- `style`: Code style changes
- `refactor`: Code refactoring
- `test`: Test additions/modifications
- `chore`: Maintenance tasks

Examples:
```
feat(agent): add budget optimization to Marketing Manager
fix(security): remove hardcoded API key from Graphic Designer workflow
docs: update README with deployment instructions
```

### Pull Request Process

1. **Before submitting**:
   - Run workflow validation: `npm run validate`
   - Test all affected workflows
   - Update documentation if needed
   - Ensure CI checks pass

2. **PR description template**:
   ```markdown
   ## Description
   Brief description of changes

   ## Type of Change
   - [ ] Bug fix
   - [ ] New feature
   - [ ] Breaking change
   - [ ] Documentation update

   ## Testing
   - [ ] Tested locally with n8n
   - [ ] All workflows execute successfully
   - [ ] No hardcoded credentials

   ## Checklist
   - [ ] My code follows project conventions
   - [ ] I've updated relevant documentation
   - [ ] I've added tests if applicable
   ```

3. **Review process**:
   - PRs require at least one approval
   - Address all review comments
   - Keep PRs focused and small

## 🧪 Testing

### Manual Testing
1. Import modified workflows into n8n
2. Test with sample data
3. Verify all agent communications
4. Check error handling scenarios

### Automated Testing
```bash
# Validate JSON syntax
npm run validate

# Check for security issues
npm run security-check

# Run integration tests
npm run test:integration
```

## 📁 Project Structure

```
agentic-mkt-mu/
├── Agentic_Marketing___*.json  # Workflow files
├── .github/                    # GitHub Actions
├── docs/                       # Documentation
├── scripts/                    # Utility scripts
├── tests/                      # Test files
├── CLAUDE.md                   # AI assistant instructions
├── README.md                   # Project overview
└── CONTRIBUTING.md            # This file
```

## 🔧 Development Tips

### Working with n8n Workflows

1. **Use sub-workflows** for reusable components
2. **Implement caching** for expensive operations
3. **Add logging** for debugging
4. **Use environment variables** for configuration

### Agent Development

1. **Clear role definition**: Each agent should have a specific purpose
2. **Structured outputs**: Use consistent JSON schemas
3. **Error handling**: Gracefully handle API failures
4. **Performance**: Optimize prompts and minimize API calls

### Best Practices

1. **DRY Principle**: Don't repeat yourself - extract common patterns
2. **KISS Principle**: Keep it simple - avoid over-engineering
3. **Documentation**: Document complex logic and decisions
4. **Version Control**: Make atomic commits with clear messages

## 🐛 Reporting Issues

1. **Check existing issues** first
2. **Use issue templates** when available
3. **Provide detailed information**:
   - n8n version
   - Workflow export (without credentials)
   - Error messages
   - Steps to reproduce

## 💡 Feature Requests

1. **Open a discussion** first for major features
2. **Provide use cases** and benefits
3. **Consider backward compatibility**
4. **Be open to feedback** and alternative approaches

## 📞 Getting Help

- **Documentation**: Check CLAUDE.md and README.md
- **Issues**: Search existing issues
- **Discussions**: Start a discussion for questions
- **Community**: Join our community channels

## 🏆 Recognition

Contributors will be recognized in:
- Release notes
- Contributors list
- Project documentation

Thank you for contributing to make marketing automation better! 🚀