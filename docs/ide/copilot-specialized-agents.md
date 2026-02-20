---
title: Use specialized agents in GitHub Copilot
description: Learn about built-in agents for debugging, profiling, testing, and Visual Studio help, plus how to create custom agents for your team workflows.
ms.date: 02/20/2026
ms.topic: how-to
author: mikejo5000
ms.author: mikejo
ms.manager: mijacobs
ms.subservice: ai-tools
ms.collection: ce-skilling-ai-copilot
ms.custom: awp
ai-usage: ai-assisted
monikerRange: '>= vs-2022'
---

# Use specialized agents in GitHub Copilot

GitHub Copilot in Visual Studio goes beyond a single general-purpose assistant. Visual Studio includes a set of curated built-in agents that integrate deeply with IDE capabilities like debugging, profiling, and testing. You can also create custom agents tailored to how your team works.

## Prerequisites

+ Visual Studio 2022 [version 17.14](/visualstudio/releases/2022/release-history) or later
+ A [GitHub Copilot subscription](https://docs.github.com/en/copilot/about-github-copilot/what-is-github-copilot#getting-access-to-copilot)

## Access specialized agents

You can access specialized agents in two ways:

+ **Agent picker**: In the Copilot Chat window, select the agent picker dropdown to see available agents.
+ **@ syntax**: Type `@` followed by the agent name in the chat input (for example, `@debug`).

:::moniker range="visualstudio"

:::image type="content" source="media/visualstudio/copilot-specialized-agents/agent-picker.png" alt-text="Screenshot showing the agent picker with specialized agents in Visual Studio.":::

:::moniker-end

:::moniker range="vs-2022"

:::image type="content" source="media/vs-2022/copilot-specialized-agents/agent-picker.png" alt-text="Screenshot showing the agent picker with specialized agents.":::

:::moniker-end

## Built-in agents

Each built-in agent is designed around a specific developer workflow and integrates with Visual Studio's native tooling in ways that a generic assistant can't.

| Agent | Description |
|-------|-------------|
| **@debug** | Goes beyond reading error messages. Uses your call stacks, variable state, and diagnostic tools to walk through error diagnosis systematically across your solution. |
| **@profiler** | Connects to Visual Studio's profiling infrastructure to identify bottlenecks and suggest targeted optimizations grounded in your codebase, not generic advice. |
| **@test** | Generates unit tests tuned to your project's framework and patterns, not boilerplate that your CI will reject. |
| **@vs** | Answers questions about Visual Studio itself, including features, settings, shortcuts, and workflows you might not know existed. |
| **@modernize** | (.NET and C++ only) Handles framework and dependency upgrades with awareness of your actual project graph. Flags breaking changes, generates migration code, and follows your existing patterns. |

### Use the @debug agent

The @debug agent helps you diagnose errors systematically by analyzing your debugging context.

**Example prompts**:

+ `@debug Why is this exception being thrown?`
+ `@debug Analyze the current call stack and explain what went wrong`
+ `@debug What's causing the null reference in this method?`

### Use the @profiler agent

The @profiler agent connects to Visual Studio's profiling tools to help identify and fix performance issues.

**Example prompts**:

+ `@profiler Find the performance bottlenecks in my application`
+ `@profiler Why is this method taking so long to execute?`
+ `@profiler Suggest optimizations for the hot path`

### Use the @test agent

The @test agent generates unit tests that match your project's testing framework and conventions.

**Example prompts**:

+ `@test Generate unit tests for the selected method`
+ `@test Create tests that cover edge cases for this class`
+ `@test Write integration tests for this API endpoint`

For more comprehensive .NET testing support, see [GitHub Copilot testing for .NET](../test/github-copilot-test-dotnet-overview.md).

### Use the @vs agent

The @vs agent answers questions about Visual Studio features, settings, and workflows.

**Example prompts**:

+ `@vs How do I enable line numbers in the editor?`
+ `@vs What's the keyboard shortcut for Go to Definition?`
+ `@vs How do I configure code cleanup settings?`

### Use the @modernize agent

The @modernize agent helps with framework migrations and dependency upgrades for .NET and C++ projects.

**Example prompts**:

+ `@modernize Upgrade this project to .NET 8`
+ `@modernize What breaking changes should I expect when migrating?`
+ `@modernize Update deprecated API calls in this file`

## Custom agents (Preview)

> [!NOTE]
> Custom agents are a preview feature. The format of agent files may change as the feature evolves to support different capabilities.

The built-in agents cover common workflows, but your team knows your workflow best. Custom agents let you build your own using the same foundation: workspace awareness, code understanding, your preferred AI model, and your own tools.

Custom agents become especially powerful when combined with [MCP (Model Context Protocol)](mcp-servers.md). You can connect agents to external knowledge sources like internal documentation, design systems, APIs, and databases, so the agent isn't limited to what's in your repository.

### Create a custom agent

Custom agents are defined as `.agent.md` files in your repository's `.github/agents/` folder:

```text
your-repo/
└── .github/
    └── agents/
        └── code-reviewer.agent.md
```

### Agent file format

Each agent file uses a simple template with YAML frontmatter followed by Markdown instructions:

```markdown
---
name: Code Reviewer
description: Reviews PRs against our team's coding standards
model: claude-opus-4-6
tools: ["codebase_search", "read_file", "find_references"]
---

You are a code reviewer for our team. When reviewing changes, check for:

- Naming conventions: PascalCase for public methods, camelCase for private
- Error handling: all async calls must have try/catch with structured logging
- Test coverage: every public method needs at least one unit test

Flag violations clearly and suggest fixes inline.
```

#### Frontmatter properties

| Property | Required | Description |
|----------|----------|-------------|
| `name` | Yes | Display name for the agent in the agent picker |
| `description` | Yes | Brief description shown when hovering over the agent |
| `model` | No | AI model to use. If not specified, uses the model selected in the model picker. |
| `tools` | No | Array of tool names the agent can use |

### Specify tools

Tools extend what your custom agent can do. You can specify which tools the agent should use in the `tools` array.

> [!IMPORTANT]
> Tool names vary across GitHub Copilot platforms. Check the tools available in Visual Studio specifically to make sure your agent works as expected. Select the **Tools** icon in the chat window to see available tool names.

### Connect to external sources with MCP

With [MCP servers](mcp-servers.md), your custom agents can access external knowledge sources:

+ Internal documentation and wikis
+ Design systems and component libraries
+ APIs and databases
+ Style guides and ADR repositories

For example, a code review agent can check PRs against your actual conventions by connecting to your style guide via MCP.

### Example custom agents

#### Code review agent

```markdown
---
name: Code Reviewer
description: Reviews code against our team's coding standards
tools: ["codebase_search", "read_file"]
---

You are a code reviewer for our team. Review changes for:

1. **Naming conventions**: PascalCase for public methods, camelCase for private fields
2. **Error handling**: All async calls must have try/catch with structured logging
3. **Test coverage**: Every public method needs at least one unit test
4. **Documentation**: Public APIs must have XML documentation comments

Flag violations clearly and suggest fixes inline.
```

#### Planning agent

```markdown
---
name: Feature Planner
description: Helps plan features before writing code
tools: ["codebase_search", "read_file", "find_references"]
---

You are a planning assistant. When asked about a feature:

1. Gather requirements by asking clarifying questions
2. Identify affected files and components in the codebase
3. Break down the work into discrete tasks
4. Flag potential risks or dependencies
5. Create a structured plan that can be handed off for implementation

Focus on understanding scope before suggesting solutions.
```

#### Design system agent

```markdown
---
name: Design System
description: Enforces UI design patterns and component usage
tools: ["codebase_search", "read_file"]
---

You are a design system expert. When reviewing UI code:

1. Check that standard components are used instead of custom implementations
2. Verify spacing and layout follow the design token system
3. Ensure accessibility requirements are met (ARIA labels, keyboard navigation)
4. Flag any UI drift from established patterns

Reference the component library documentation when suggesting fixes.
```

### Community configurations

The [awesome-copilot repository](https://github.com/github/awesome-copilot) has community-contributed agent configurations you can use as starting points. When using configurations from this repository, verify tool names work in Visual Studio before deploying to your team.

### Limitations and notes

+ This is a preview feature; the format of agent files may change to support different capabilities.
+ If you don't specify a model, the agent uses whatever model is selected in the model picker.
+ Tool names vary across GitHub Copilot platforms. Verify tool names work in Visual Studio.
+ Configurations from the awesome-copilot repo are great starting points, but verify tool names before using them in Visual Studio.

## Share feedback

Share your custom agent configurations in the [awesome-copilot repository](https://github.com/github/awesome-copilot) or file feedback through [Visual Studio Developer Community](https://developercommunity.visualstudio.com/). Your workflows help shape future features.

## Related content

+ [Get started with GitHub Copilot agent mode](copilot-agent-mode.md)
+ [Use MCP servers](mcp-servers.md)
+ [Customize chat responses and set context](copilot-chat-context.md)
+ [GitHub Copilot testing for .NET](../test/github-copilot-test-dotnet-overview.md)
