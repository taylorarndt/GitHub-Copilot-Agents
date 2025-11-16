# GitHub Copilot Custom Agents - Dev Team

> **DISCLAIMER**: AI always makes mistakes. This project is NOT endorsed by Microsoft or GitHub. Use at your own risk. These agents are experimental and may produce incorrect, incomplete, or unexpected results. Always review and verify any code changes before committing them.

A collection of GitHub Copilot custom agents that simulate a professional development team workflow inside VS Code. These agents work together to plan, implement, and review code changes with the rigor of a senior engineering team.

## Why Does This Exist?

Because vibe coding is broken. AI tools often delete code unexpectedly, make changes without explanation, and create a chaotic, non-seamless development experience. There has to be a better way - one that is accessible, collaborative, and actually helps developers maintain control.

This project creates a structured workflow where:
- The developer agent thinks before acting and asks for approval
- All changes are verified before being marked complete
- A reviewer agent provides quality gates just like a real team
- You maintain full visibility and control over what happens

No more mysterious deletions. No more "AI did something weird." Just clear, deliberate, collaborative development.

## What Are These Agents?

These are custom GitHub Copilot chat agents (also called chat participants) that extend Copilot's capabilities with specialized roles:

- **Developer Agent** (`@developer`) - A professional implementation engineer that handles full reasoning, planning, and execution of development tasks
- **Reviewer Agent** (`@reviewer`) - A senior code reviewer that ensures quality, correctness, and adherence to engineering standards

Together, they create a collaborative workflow where the developer implements features and the reviewer provides structured feedback - just like a real dev team.

**Coming Soon**: I plan to add many more specialized agents including Designer, Security Reviewer, Accessibility Checker, and more to create a complete AI-powered development team.

## Key Features

- **Full Reasoning & Planning** - Developer agent thinks through problems systematically before implementing
- **Automatic Code Review** - Built-in handoff workflow sends completed work to the reviewer agent
- **Internet Research** - Agents can search the web for up-to-date documentation and best practices
- **Structured Feedback** - Reviews follow a professional rubric with blocking issues and suggestions
- **Quality Gates** - Ensures verification of builds, tests, and file existence before marking work complete

## IMPORTANT: Current Limitations

**Automatic agent handoffs are NOT working yet in VS Code Insiders.** Even with the correct settings configured from the built-in plan agent, the automatic switching from `@developer` to `@reviewer` does not occur. This is a known limitation that I am actively working on.

For now, when the developer agent completes its work, you will see a "Request Code Review" button. Click that button, then press Enter to send the message to the reviewer agent.

## Warning: Premium Request Consumption

**These agents have the potential to consume MANY premium requests.** The developer and reviewer agents use advanced reasoning, web searches, and multi-step workflows that can quickly burn through your monthly allowance. If you run out of premium requests, don't blame me - you've been warned!

Consider:
- Pro plan: 300 premium requests/month
- Pro+ plan: 1500 premium requests/month
- Additional requests: $0.04 each

Use these agents wisely, especially if you're on the Pro plan.

## How to Use These Agents in VS Code

### Prerequisites

1. **VS Code** - Install [Visual Studio Code](https://code.visualstudio.com/)
2. **GitHub Copilot Subscription** - You need an active Copilot subscription:
   - Free tier: 50 agent mode or chat requests/month
   - Pro ($10/month or $100/year): Unlimited chats, 300 premium requests/month (additional requests $0.04 each)
   - Pro+ ($39/month or $390/year): Unlimited chats, 1500 premium requests/month (5x more than Pro), access to all models including Claude Opus 4.1

3. **GitHub Copilot Extension** - Install from the [VS Code Marketplace](https://marketplace.visualstudio.com/items?itemName=GitHub.copilot)

### Installation Steps

You have two options for installing these agents:

#### Option 1: User Profile (Recommended - Use agents across all workspaces)

1. **Download the agent files** from this repository
2. **Copy to your VS Code user profile folder**:
   
   **Windows:**
   ```
   %APPDATA%\Code\User\globalStorage\github.copilot-chat\agents\
   ```
   
   **macOS:**
   ```
   ~/Library/Application Support/Code/User/globalStorage/github.copilot-chat/agents/
   ```
   
   **Linux:**
   ```
   ~/.config/Code/User/globalStorage/github.copilot-chat/agents/
   ```

3. **Restart VS Code** to load the agents

4. **Verify agents are available** - The agents will now appear in any workspace you open

#### Option 2: Workspace-Specific (For team sharing)

1. **Download the agent files** from this repository
2. **Copy to your workspace** - Place the `.agent.md` files in a `.github/agents` folder in your project:
   ```
   your-project/
   ├── .github/
   │   └── agents/
   │       ├── developer.agent.md
   │       └── reviewer.agent.md
   └── your-code-files...
   ```
3. **Open VS Code in your workspace**
   ```bash
   code .
   ```
4. **Verify agents are loaded**
   - Open GitHub Copilot Chat (Ctrl+Shift+I / Cmd+Shift+I)
   - Click the agent dropdown in the chat input
   - You should see `@developer` and `@reviewer` in the list

**Note**: You can also create agents directly in VS Code by running the command "Chat: New Custom Agent" (Ctrl+Shift+P) and choosing either "Workspace" or "User profile" as the location.

### Using the Agents

**Developer Agent (@developer)**

Ask the developer agent to implement features, fix bugs, or plan solutions:

```
@developer Create a new user authentication module with JWT tokens
```

```
@developer Fix the memory leak in the data processing pipeline
```

The developer will:
1. Research the problem (including web searches if needed)
2. Explain their approach
3. Ask for approval before making changes
4. Implement the solution
5. Verify it works
6. Automatically hand off to reviewer

**Reviewer Agent (@reviewer)**

The reviewer agent automatically receives handoffs from the developer, but you can also invoke it directly:

```
@reviewer Check the implementation in src/auth/jwt.ts
```

The reviewer will:
1. Verify all referenced files exist
2. Review code quality, correctness, and testing
3. Provide structured feedback with blocking issues and suggestions
4. Hand back to developer if changes are needed

## Agent Workflow

Here's how the agents are designed to work together (note: automatic handoffs not yet functional):

```
User Request → @developer
                    ↓
            Plan & Implement
                    ↓
            Verify & Test
                    ↓
            Handoff → @reviewer
                    ↓
            Code Review
                    ↓
        ┌───────────┴───────────┐
        ↓                       ↓
    APPROVE              REQUEST_CHANGES
        ↓                       ↓
    Complete            Handoff → @developer
                               ↓
                        Apply Fixes
                               ↓
                        Back to Review
```

## Customizing the Agents

You can modify the `.agent.md` files to customize:

- **Tone and style** - Adjust the voice and communication preferences
- **Tools available** - Enable/disable specific capabilities (search, edit, fetch, etc.)
- **Review criteria** - Modify the reviewer's focus areas and standards
- **Handoff behavior** - Change when and how agents collaborate

Example customization in `developer.agent.md`:
```yaml
tools:
  - search        # Internet research
  - edit          # File editing
  - fetch         # Web fetching
  - runSubagent   # Spawn sub-agents for complex tasks
  - problems      # Check for errors
```

## Contributing

Want to add more agents to the dev team or improve existing ones? Contributions are welcome!

### How to Contribute

1. **Submit a Pull Request (PR)** with:
   - New agents (create a new `.agent.md` file)
   - Edits to existing agents (improve instructions, fix bugs, add features)
   - Documentation improvements
   - Bug fixes

2. **Open an Issue** to:
   - Report bugs or unexpected behavior
   - Suggest new agent ideas
   - Request features or improvements
   - Ask questions about usage

### Adding a New Agent

1. **Create a new `.agent.md` file** (e.g., `tester.agent.md`)
2. **Define the agent metadata**:
   ```yaml
   ---
   name: tester
   description: QA specialist that writes comprehensive test suites
   argument-hint: Describe what needs testing
   tools:
     - search
     - edit
     - problems
   handoffs:
     - label: Send to Developer
       agent: developer
       send: false
   ---
   ```

3. **Write the agent instructions** - Define the role, responsibilities, and workflow
4. **Test the agent** - Invoke it with `@tester` in Copilot Chat
5. **Submit a pull request** - Share your agent with the community!

### Agent Ideas

Here are some agents you could create:

- **@tester** - QA specialist for test coverage and test case generation
- **@architect** - System design expert for architectural decisions
- **@security** - Security auditor for vulnerability scanning
- **@docs** - Documentation specialist for README and API docs
- **@performance** - Performance engineer for optimization recommendations
- **@accessibility** - Accessibility expert ensuring WCAG compliance

### Contribution Guidelines

1. Keep agent instructions clear and focused on a single responsibility
2. Include examples in the agent instructions
3. Document all available tools and handoffs
4. Test thoroughly before submitting
5. Update this README with your new agent

## Learn More

- [VS Code Copilot Documentation](https://code.visualstudio.com/docs/copilot/overview)
- [GitHub Copilot Features](https://github.com/features/copilot)
- [Chat Agents/Participants API](https://code.visualstudio.com/api/extension-guides/chat)
- [AI Extensibility in VS Code](https://code.visualstudio.com/docs/copilot/copilot-extensibility-overview)

## License

[MIT License](LICENSE) - Feel free to use and modify these agents for your projects.

## Acknowledgments

Built for GitHub Copilot using the Chat Participants extensibility model. These agents leverage Copilot's AI capabilities to create specialized team member personas that enhance your development workflow.

---

**Note**: These agents require an active GitHub Copilot subscription and work within VS Code using the `.agent.md` file format for custom chat participants.
