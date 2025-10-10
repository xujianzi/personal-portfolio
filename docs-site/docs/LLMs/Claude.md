---
tags:
  - AI
  - LLM
  - Claude
  - Tutorial
  - CLI
---

# Claude AI - Complete Usage Guide

## 1. Overview

!!! abstract "What is Claude?"
    [Claude](https://claude.ai/) is an advanced AI assistant developed by Anthropic. It excels at natural language understanding, code generation, analysis, creative writing, and complex reasoning tasks. Claude is available both as a web interface and as a command-line tool (Claude Code).

**Official Resources**:

* Web Interface: [https://claude.ai/](https://claude.ai/)
* Claude Code (CLI): [https://claude.com/code](https://claude.com/code)
* API Documentation: [https://docs.anthropic.com/](https://docs.anthropic.com/)

**Key Features**:

* Natural conversation and context understanding
* Code generation and debugging across multiple programming languages
* Document analysis and summarization (supports PDF, images, text files)
* Long-form content creation
* Multi-turn conversations with context retention
* Command-line interface for developers (Claude Code)

---

## 2. Getting Started

### 2.1 Claude Web Interface

1. Visit [https://claude.ai/](https://claude.ai/)
2. Sign up using email, Google account, or other supported methods
3. Verify your email if required
4. Start chatting immediately after login

!!! note "Free vs Pro Plans"
    Claude offers both free and paid subscription tiers. Claude Pro provides higher usage limits, priority access, and early access to new features.

### 2.2 Claude Code (CLI)

!!! abstract "Claude Code CLI"
    Claude Code is a command-line interface that brings Claude AI directly into your terminal and development workflow. It's designed for developers who prefer working in the command line.

**Installation**: Visit [https://claude.com/code](https://claude.com/code) for installation instructions.

---

## 3. Claude Code Commands

!!! tip "Essential Commands"
    These commands help you manage your Claude Code sessions effectively.

### 3.1 Project Management

| Command | Description |
|---------|-------------|
| `/init` | Create the `CLAUDE.md` file in your project |
| `/compact` | Compress the `CLAUDE.md` file to make the AI more focused |
| `/clear` | Clear conversation history and free up context |

!!! important "CLAUDE.md File"
    The `CLAUDE.md` file provides project-specific instructions to Claude Code. Use `/init` to create it and customize it with your project guidelines.

### 3.2 Session Control

| Command | Description |
|---------|-------------|
| `claude -p` | Start a temporary conversation session |
| `/resume` | Resume a previous conversation |
| `/agents` | Create a sub-agent for the project |
| `/ide` | Launch IDE integration mode |

### 3.3 Conversation Modifiers

When interacting with Claude Code, you can use special keywords to enhance responses:

| Modifier | Effect |
|----------|--------|
| `think` | Ask AI to think about the question |
| `think hard` | Request deeper analysis |
| `think harder` | Request even more thorough reasoning |
| `ultra think` | Maximum reasoning depth |

!!! example "Using Modifiers"
    ```bash
    # Basic question
    How should I structure this API?

    # With thinking modifier
    think hard: How should I structure this RESTful API for scalability?
    ```

### 3.4 Special Symbols

| Symbol | Purpose | Example |
|--------|---------|---------|
| `!` | Bash mode - informs AI of installed apps to avoid repeat installations | `! I've already installed Docker` |
| `#` | Add to memory - creates long-term memory for the AI | `# This project uses Python 3.11` |

!!! tip "Memory Management"
    Use `#` to save important project context that should persist across sessions. This helps Claude remember key decisions and setup details.

---

## 4. MCP (Model Context Protocol) Commands

!!! abstract "What is MCP?"
    MCP (Model Context Protocol) allows Claude to integrate with external tools and services, extending its capabilities beyond the core AI functionality.

### 4.1 Basic MCP Commands

| Command | Description |
|---------|-------------|
| `claude mcp add <mcpname>` | Add a new MCP server |
| `claude mcp list` | View all installed MCP servers |
| `claude mcp remove <mcpname>` | Remove an MCP server |

!!! note "Finding MCP Servers"
    Discover available MCP servers at: [Awesome MCP Servers](https://github.com/punkpeye/awesome-mcp-servers/blob/main/README-zh.md)

### 4.2 MCP Examples

```bash
# Add a database MCP
claude mcp add neon

# List all MCPs
claude mcp list

# Remove an MCP
claude mcp remove neon
```

### 4.3 MCP Permissions

When working with MCPs, you can manage permissions:

* **Allow**: Grant permission for MCP to execute actions
* **Deny**: Block MCP from executing actions

!!! example "Using MCP in Conversation"
    You can reference MCPs directly in your prompts:
    ```
    Use mcp__neon to query the database for user statistics
    ```

---

## 5. Custom Slash Commands

!!! tip "Create Your Own Commands"
    Claude Code allows you to create custom slash commands tailored to your workflow.

### 5.1 Setup

1. Navigate to your `.claude` directory
2. Create a `commands` folder if it doesn't exist
3. Create markdown files for each command
4. The filename becomes the command name

### 5.2 Command Structure

Create a file in `.claude/commands/` with natural language instructions:

**Example: `.claude/commands/code_review.md`**
```markdown
对比这个分支 $ARGUMENTS，与 main 分支的差异，提出 review 意见
```

**Usage**:
```bash
/code_review feature-branch
```

### 5.3 Variables in Commands

| Variable | Description |
|----------|-------------|
| `$ARGUMENTS` | Passes arguments to the command |
| `$PROJECT_PATH` | Current project directory path |
| `$FILE` | Current file being worked on |

### 5.4 Example Custom Commands

**`.claude/commands/test.md`**
```markdown
Run all unit tests for the current project and report any failures.
If tests fail, suggest fixes for the failing tests.
```

**`.claude/commands/deploy.md`**
```markdown
1. Run build command
2. Check for build errors
3. If successful, provide deployment checklist
4. Remind about environment variables and secrets
```

**`.claude/commands/refactor.md`**
```markdown
Analyze the file $FILE and suggest refactoring improvements:
- Code organization
- Performance optimizations
- Best practices
- Potential bugs
```

!!! important "Command Best Practices"
    - Use clear, descriptive filenames
    - Write detailed instructions in natural language
    - Include expected inputs and outputs
    - Test commands before relying on them in production workflows

---

## 6. Core AI Capabilities

### 6.1 Code Generation

Claude excels at generating code across multiple programming languages.

**Supported Languages**:

* Python, JavaScript, TypeScript, Java, C++, C#, Go, Rust
* HTML, CSS, SQL
* Shell scripting (Bash, PowerShell)
* And many more

!!! example "Code Generation Request"
    ```
    Write a Python function to validate email addresses using regex,
    with comprehensive error handling and unit tests
    ```

### 6.2 Code Review and Debugging

Claude can analyze existing code and suggest improvements.

**Capabilities**:

* Bug detection and fixes
* Performance optimization suggestions
* Code style and best practice recommendations
* Security vulnerability identification

!!! important "Always Test Generated Code"
    While Claude provides high-quality code, always review and test it thoroughly before deploying to production.

### 6.3 Document Analysis

Upload and analyze various document types:

* PDFs
* Images (code screenshots, diagrams)
* Text files
* Markdown files
* Code repositories

**Example Workflow**:
```bash
# Attach file and ask
Analyze this API documentation and create a Python client library
```

---

## 7. Advanced Usage Tips

### 7.1 Effective Prompting

!!! tip "Writing Better Prompts"
    The quality of responses depends on how you phrase questions.

**Be Specific**:
```
❌ "Fix my code"
✅ "This Python function raises a KeyError when the 'age' key is missing.
   Add error handling and return None for missing keys. Code: [paste]"
```

**Provide Context**:
```
❌ "How do I deploy this?"
✅ "I have a Node.js Express app with PostgreSQL database.
   How should I deploy it to AWS using Docker containers?"
```

**Request Step-by-Step**:
```
I need to build a REST API. Please:
1. Recommend a tech stack for Python
2. Show project structure
3. Provide example endpoints for CRUD operations
4. Include authentication middleware
5. Add error handling best practices
```

### 7.2 Multi-Turn Problem Solving

Claude excels at iterative problem-solving:

```bash
# Initial query
How do I scrape product prices from an e-commerce site?

# Follow-up 1
It's for daily price tracking. What tools should I use?

# Follow-up 2
Show me how to handle pagination

# Follow-up 3
How do I store the data efficiently?
```

!!! note "Context Retention"
    Claude remembers the conversation context, so you can build on previous responses without repeating information.

### 7.3 Using Claude as a Learning Tool

* **Ask "Why" and "How"**: Understand the reasoning, not just the solution
* **Request Analogies**: "Explain Kubernetes using a restaurant analogy"
* **Progressive Learning**: Start simple, then go deeper
* **Practice Problems**: Ask for exercises with solutions

---

## 8. Project-Specific Configuration

### 8.1 CLAUDE.md File Structure

Create a `CLAUDE.md` file in your project root to provide context:

```markdown
# Project Name

## Overview
Brief description of the project

## Tech Stack
- Frontend: React + TypeScript
- Backend: Python FastAPI
- Database: PostgreSQL
- Deployment: Docker + AWS

## Code Style
- Use ESLint and Prettier for JavaScript/TypeScript
- Follow PEP 8 for Python
- All functions must have docstrings

## Important Notes
- API keys are stored in .env file
- Never commit credentials to git
- Run tests before committing: `npm test`

## Common Commands
- Start dev server: `npm run dev`
- Run tests: `npm test`
- Build for production: `npm run build`
```

!!! tip "Keep CLAUDE.md Updated"
    Regularly update this file as your project evolves. Use `/compact` to optimize it when it gets too large.

### 8.2 Git Integration

Claude Code can work with Git:

```bash
# Review changes
Show me the diff for the last commit

# Analyze branch
Compare feature-branch with main and suggest improvements

# Generate commit message
Create a commit message for these changes: [describe changes]
```

---

## 9. Limitations and Considerations

!!! warning "What Claude Cannot Do"

### 9.1 No Real-Time Data Access

* Cannot browse the internet in real-time
* Knowledge cutoff: **January 2025**
* Cannot provide current weather, stock prices, or live news

### 9.2 No Code Execution

* Cannot run or test code directly
* Cannot install packages or verify functionality
* You must test generated code in your own environment

### 9.3 Accuracy Considerations

!!! important "Always Verify"
    * Verify critical facts from authoritative sources
    * Test code before deploying to production
    * Cross-check technical specifications
    * Review security-sensitive code carefully

---

## 10. Privacy and Security

!!! warning "Data Privacy"
    **Never share**:

    * Passwords or API keys
    * Private credentials
    * Sensitive personal information
    * Proprietary business data

**Best Practices**:

* Use placeholders for sensitive data (e.g., `YOUR_API_KEY_HERE`)
* Sanitize code before sharing (remove real credentials, database URLs)
* Review Anthropic's privacy policy: [https://www.anthropic.com/privacy](https://www.anthropic.com/privacy)

---

## 11. Claude API (For Developers)

!!! abstract "Programmatic Access"
    Integrate Claude into your applications using the API.

### 11.1 Getting Started

1. Visit [https://console.anthropic.com/](https://console.anthropic.com/)
2. Sign up for API access
3. Generate API keys
4. Review documentation and pricing

### 11.2 Basic API Example (Python)

```python
import anthropic

client = anthropic.Anthropic(
    api_key="your-api-key-here",
)

message = client.messages.create(
    model="claude-3-5-sonnet-20241022",
    max_tokens=1024,
    messages=[
        {"role": "user", "content": "Explain async/await in Python"}
    ]
)

print(message.content)
```

### 11.3 Available Models

| Model | Description | Best For |
|-------|-------------|----------|
| Claude 3.5 Sonnet | Balanced performance and capability | Complex tasks, coding, analysis |
| Claude 3 Opus | Highest intelligence | Most difficult reasoning tasks |
| Claude 3 Haiku | Fastest, most compact | Simple queries, high-volume tasks |

!!! tip "API Documentation"
    Complete API docs: [https://docs.anthropic.com/](https://docs.anthropic.com/)

---

## 12. Troubleshooting

| Issue | Possible Cause | Solution |
|-------|----------------|----------|
| **Response too generic** | Prompt lacks specificity | Add more context and details |
| **Code doesn't work** | Environment differences | Review, test, provide error messages |
| **Response incomplete** | Hit length limit | Ask Claude to continue |
| **Wrong information** | Hallucination or outdated knowledge | Verify from authoritative sources |
| **Context lost** | Too many messages | Start new conversation with summary |

!!! tip "Getting Unstuck"
    If Claude's responses aren't helpful:

    1. Rephrase your question with more context
    2. Break the problem into smaller parts
    3. Provide examples of what you're looking for
    4. Use modifiers like `think hard` for complex problems

---

## 13. Best Practices Summary

!!! success "Maximize Effectiveness"
    1. **Be Clear and Specific**: Detailed context gets better results
    2. **Iterate and Refine**: Use follow-up questions
    3. **Verify Critical Information**: Double-check important facts
    4. **Leverage Context**: Reference previous messages
    5. **Use Structured Prompts**: Break complex tasks into steps
    6. **Provide Examples**: Show what you're looking for
    7. **Test Generated Code**: Never deploy untested code
    8. **Protect Sensitive Data**: Don't share credentials
    9. **Use Custom Commands**: Automate repetitive workflows
    10. **Keep CLAUDE.md Updated**: Maintain project context

---

## 14. Resources

### Official Resources

* **Claude Web**: [https://claude.ai/](https://claude.ai/)
* **Claude Code**: [https://claude.com/code](https://claude.com/code)
* **Anthropic**: [https://www.anthropic.com/](https://www.anthropic.com/)
* **API Docs**: [https://docs.anthropic.com/](https://docs.anthropic.com/)
* **Support**: Available through the Claude interface

### Community Resources

* **Discord**: Check Anthropic's website for community links
* **Twitter/X**: [@AnthropicAI](https://twitter.com/AnthropicAI)
* **MCP Servers**: [Awesome MCP Servers](https://github.com/punkpeye/awesome-mcp-servers)

---

## 15. Conclusion

Claude AI, whether through the web interface, CLI (Claude Code), or API, is a powerful tool for developers, writers, researchers, and learners. By mastering commands, custom workflows, and effective prompting techniques, you can significantly enhance your productivity and problem-solving capabilities.

!!! success "Key Takeaways"
    * Start with basic commands and gradually explore advanced features
    * Customize with `CLAUDE.md` and slash commands for your projects
    * Use MCP servers to extend capabilities
    * Always verify and test AI-generated code
    * Protect sensitive information
    * Experiment and iterate to find what works best for you

---

**Last Updated**: 2025-10-07
**Version**: 1.0
**Author**: Jian Xu
