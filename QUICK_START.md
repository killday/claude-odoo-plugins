# Quick Start: Using Odoo Plugins with Different AI Tools

This guide helps you quickly get started with these Odoo plugins across different AI coding assistants.

## TL;DR

- ✅ **Claude Code**: Native support, install with `claude mcp add`
- ℹ️ **GitHub Copilot**: No direct install, but can use the knowledge (see options below)
- ℹ️ **Cursor/JetBrains**: Can use workspace context
- 🎯 **Best Setup**: Claude Code + GitHub Copilot together

## For Claude Code Users (Native Support)

### Installation
```bash
# Install all 8 Odoo plugins at once
claude mcp add cloud-market https://github.com/ahmed-lakosha/odoo-plugins.git
```

### Usage
```bash
# Upgrade module from Odoo 16 to 17
claude /odoo-upgrade --from=16 --to=17

# Generate tests for a model
claude /odoo-test generate sale.order

# Audit security
claude /odoo-security --layer=all

# Create QWeb report
claude "Create a PDF invoice report with QR code"

# Check i18n completeness
claude /odoo-i18n validate --lang=ar_001
```

**Documentation**: See plugin-specific README files for detailed usage.

---

## For GitHub Copilot Users

### ⚠️ Important Note
These plugins **cannot be directly installed** in GitHub Copilot. They use different architectures.

### Option 1: Use Both Tools Together (Recommended)

Install Claude Code alongside GitHub Copilot:

```bash
# Install Claude Code
npm install -g @anthropic/claude-code

# Install Odoo plugins
claude mcp add cloud-market https://github.com/ahmed-lakosha/odoo-plugins.git
```

**When to use each:**
- **Claude Code**: Complex Odoo tasks (upgrades, migrations, security audits)
- **GitHub Copilot**: Inline code completion, quick refactors

**Example workflow:**
1. Use Claude Code to upgrade module: `claude /odoo-upgrade --from=16 --to=17`
2. Use Copilot to write tests for upgraded code (inline suggestions)
3. Use Claude Code to validate: `claude /odoo-security`

### Option 2: Add Odoo Context to Your Project

Copy the template to your Odoo project:

```bash
# In your Odoo module repository
mkdir -p .github
cp path/to/examples/.github-copilot-instructions-template.md .github/copilot-instructions.md

# Edit to keep only relevant patterns for your project
nano .github/copilot-instructions.md
```

**What this does:**
- GitHub Copilot reads `.github/copilot-instructions.md` automatically
- Provides Odoo-specific context for code suggestions
- Applies to all team members who use the repository

**Example usage in IDE:**
```python
# Just start typing - Copilot will suggest based on instructions
def test_sale_order_creation(self):
    # Copilot will suggest using Form helper pattern (from instructions)
    with Form(self.env['sale.order']) as order_form:
        ...
```

### Option 3: Add Skills to Workspace

For project-specific knowledge:

```bash
# In your project root
mkdir -p .copilot-context

# Copy relevant skills
cp odoo-test-plugin/odoo-test/SKILL.md .copilot-context/testing.md
cp odoo-security-plugin/odoo-security/SKILL.md .copilot-context/security.md

# Reference in Copilot Chat
# In IDE: @workspace Show me testing patterns from testing.md
```

---

## For Cursor IDE Users

Cursor can use workspace context similar to Copilot:

```bash
# In your project root
mkdir -p .cursor

# Copy relevant SKILL.md files
cp odoo-test-plugin/odoo-test/SKILL.md .cursor/odoo-testing.md
cp odoo-upgrade-plugin/odoo-upgrade/SKILL.md .cursor/odoo-upgrade.md

# Cursor will automatically index these files
```

**Usage in Cursor:**
- Press `Cmd+K` (Mac) or `Ctrl+K` (Windows/Linux)
- Type: "Generate tests for sale.order using the patterns in odoo-testing.md"

---

## For JetBrains IDEs (PyCharm, IntelliJ)

JetBrains AI Assistant can use project context:

1. **Enable AI Assistant** in Settings → Tools → AI Assistant
2. **Add context files**:
   ```bash
   mkdir -p .ai-context
   cp odoo-test-plugin/odoo-test/SKILL.md .ai-context/
   ```
3. **Reference in AI Chat**:
   ```
   Generate a test following the patterns in .ai-context/odoo-testing.md
   ```

---

## Comparison Table

| Feature | Claude Code | GitHub Copilot | Cursor | JetBrains AI |
|---------|-------------|----------------|--------|--------------|
| **Native Plugin Support** | ✅ Yes | ❌ No | ❌ No | ❌ No |
| **Can Use Knowledge** | ✅ Full | ⚠️ Manual | ⚠️ Manual | ⚠️ Manual |
| **Inline Completion** | ❌ No | ✅ Yes | ✅ Yes | ✅ Yes |
| **Slash Commands** | ✅ Yes | ❌ No | ✅ Yes | ❌ No |
| **Workspace Context** | ✅ Yes | ✅ Yes | ✅ Yes | ✅ Yes |
| **Best for Odoo** | ✅✅✅ | ✅✅ | ✅✅ | ✅✅ |
| **Best for General** | ✅✅ | ✅✅✅ | ✅✅✅ | ✅✅✅ |

**Legend:**
- ✅✅✅ Excellent
- ✅✅ Very Good
- ✅ Good
- ⚠️ Partial Support
- ❌ Not Supported

---

## Recommended Setups by Use Case

### Solo Developer
**Setup**: Claude Code + GitHub Copilot
- Claude Code for complex Odoo tasks
- Copilot for inline suggestions
- **Cost**: Claude Code subscription + Copilot subscription

### Team Development
**Setup**: Claude Code + GitHub Copilot + `.github/copilot-instructions.md`
- Each developer installs Claude Code individually
- Add Copilot instructions to repository for team-wide context
- **Benefit**: Consistent coding patterns across team

### Enterprise
**Setup**: All of the above + consider building custom Copilot Extension
- See [GITHUB_COPILOT_COMPATIBILITY.md](./GITHUB_COPILOT_COMPATIBILITY.md) Option 4
- **Effort**: 40-80 hours development
- **Benefit**: Native Copilot integration with company-specific Odoo patterns

### Learning Odoo
**Setup**: Just Claude Code
- Most comprehensive Odoo-specific guidance
- Interactive learning with slash commands
- **Cost**: Claude Code subscription only

---

## What Each Tool Is Best For

### Claude Code + Odoo Plugins
✅ **Best for:**
- Module version upgrades (14-19)
- QWeb report creation
- Security auditing
- Test generation with coverage
- i18n extraction and validation
- Docker infrastructure setup
- Complex multi-step Odoo workflows

❌ **Not ideal for:**
- Inline code completion while typing
- Real-time suggestions in IDE

### GitHub Copilot
✅ **Best for:**
- Inline code completion
- Quick refactoring
- Boilerplate code generation
- General Python/JavaScript/XML suggestions

❌ **Not ideal for:**
- Complex Odoo version migrations
- Domain-specific workflows (without context files)

### Using Both Together (Recommended)
✅ **Best of both worlds:**
- Claude Code handles complex Odoo workflows
- Copilot handles inline completion
- Total cost: Both subscriptions (~$40-50/month)
- Productivity gain: Significant

---

## Quick Decision Tree

```
Do you need to work with Odoo code?
│
├─ YES → Do you want inline code completion?
│         │
│         ├─ YES → Install BOTH Claude Code + GitHub Copilot
│         │        Cost: ~$40-50/month
│         │        Best productivity
│         │
│         └─ NO → Install Claude Code only
│                  Cost: ~$20/month
│                  Full Odoo plugin support
│
└─ NO → This repository might not be relevant
         (These are Odoo-specific plugins)
```

---

## Next Steps

1. **Choose your setup** from the options above
2. **Read detailed guide**: [GITHUB_COPILOT_COMPATIBILITY.md](./GITHUB_COPILOT_COMPATIBILITY.md)
3. **Get template**: [examples/.github-copilot-instructions-template.md](./examples/.github-copilot-instructions-template.md)
4. **Explore plugins**: See individual plugin README files for detailed features

---

## Questions?

- **Claude Code issues**: https://github.com/anthropics/claude-code/issues
- **GitHub Copilot support**: https://support.github.com/
- **This repository**: https://github.com/ahmed-lakosha/odoo-plugins/issues

---

*Last Updated: March 26, 2026*
