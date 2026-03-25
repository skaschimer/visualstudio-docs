---
title: Use custom agents in GitHub Copilot
description: Learn about built-in agents for debugging, profiling, testing, and code modernization, and how to create custom agents for your team workflows.
ms.date: 03/25/2026
ms.topic: how-to
author: mikejo5000
ms.author: mikejo
ms.manager: mijacobs
ms.subservice: ai-tools
ms.collection: ce-skilling-ai-copilot
ms.custom: awp
ai-usage: ai-assisted
ms.update-cycle: 180-days
monikerRange: '>= vs-2022'
---

# Use built-in and custom agents with GitHub Copilot

Visual Studio includes a set of curated built-in agents that integrate deeply with IDE capabilities like debugging, profiling, and testing. You can also create custom agents tailored to how your team works.

## Prerequisites

+ Visual Studio 2022 [version 17.14](/visualstudio/releases/2022/release-history) or later
+ A [GitHub Copilot subscription](https://docs.github.com/en/copilot/about-github-copilot/what-is-github-copilot#getting-access-to-copilot)

## Access custom agents

:::moniker range="visualstudio"
You can access custom agents in two ways:

+ **Agent picker**: In the Copilot Chat window, select the agent picker dropdown to see available agents. Currently, this option is available only in the Visual Studio 2026 Insiders build.
+ **@ syntax**: Type `@` followed by the agent name in the chat input (for example, `@debugger`).

::: moniker-end

:::moniker range="vs-2022"
You can access custom agents by using **@ syntax**: Type `@` followed by the agent name in the chat input (for example, `@profiler`).
::: moniker-end

:::moniker range="visualstudio"

<!-- TODO: Update screenshot when 18.5 releases -->
:::image type="content" source="media/visualstudio/agent-picker.png" alt-text="Screenshot showing the agent picker with custom agents in Visual Studio.":::

:::moniker-end

:::moniker range="vs-2022"

:::image type="content" source="media/vs-2022/agent-picker.png" alt-text="Screenshot showing the agent picker with custom agents.":::

:::moniker-end

## Built-in agents

Each built-in agent is designed around a specific developer workflow and integrates with Visual Studio's native tooling in ways that a generic assistant can't.

:::moniker range="visualstudio"
| Agent | Description |
|-------|-------------|
| **@debugger** | Goes beyond reading error messages. Uses your call stacks, variable state, and diagnostic tools to walk through error diagnosis systematically across your solution. |
| **@profiler** | Connects to Visual Studio's profiling infrastructure to identify bottlenecks and suggest targeted optimizations grounded in your codebase, not generic advice. |
| **@test** | Generates unit tests tuned to your project's framework and patterns, not boilerplate that your CI will reject. |
| **@modernize** | (.NET and C++ only) Handles framework and dependency upgrades with awareness of your actual project graph. Flags breaking changes, generates migration code, and follows your existing patterns. |
::: moniker-end

:::moniker range="vs-2022"
| Agent | Description |
|-------|-------------|
| **@profiler** | Connects to Visual Studio's profiling infrastructure to identify bottlenecks and suggest targeted optimizations grounded in your codebase, not generic advice. |
::: moniker-end

:::moniker range="visualstudio"

### Use the @debugger agent

The @debugger agent helps you diagnose errors systematically by analyzing your debugging context.

**Example prompts**:

+ `@debugger Why is this exception being thrown?`
+ `@debugger Analyze the current call stack and explain what went wrong`
+ `@debugger What's causing the null reference in this method?`

::: moniker-end

### Use the @profiler agent

The @profiler agent connects to Visual Studio's profiling tools to help identify and fix performance issues.

**Example prompts**:

+ `@profiler Find the performance bottlenecks in my application`
+ `@profiler Why is this method taking so long to execute?`
+ `@profiler Suggest optimizations for the hot path`

:::moniker range="visualstudio"

### Use the @test agent

The @test agent generates unit tests that match your project's testing framework and conventions.

**Example prompts**:

+ `@test Generate unit tests for the selected method`
+ `@test Create tests that cover edge cases for this class`
+ `@test Write integration tests for this API endpoint`

For more comprehensive .NET testing support, see [GitHub Copilot testing for .NET](../test/github-copilot-test-dotnet-overview.md).

::: moniker-end

:::moniker range="visualstudio"

### Use the @modernize agent

The @modernize agent helps with framework migrations and dependency upgrades for .NET and C++ projects.

For .NET modernization workflows, the agent can support a three-stage process:

+ **Assessment**: Review package versions, target framework options, project inventory, and API compatibility risks.
+ **Plan**: Generate a migration plan that aligns with the current assessment and update priorities.
+ **Task execution**: Work through modernization tasks with a dynamic task file you can edit as the work progresses.

**Example prompts**:

+ `@modernize Upgrade this project to .NET 8`
+ `@modernize What breaking changes should I expect when migrating?`
+ `@modernize Update deprecated API calls in this file`
+ `@modernize Assess this solution, generate a migration plan, and create execution tasks`

For end-to-end guidance on GitHub Copilot app modernization for .NET, see [GitHub Copilot app modernization overview](/dotnet/core/porting/github-copilot-app-modernization/overview).

::: moniker-end

## Custom agents

> [!NOTE]
> Custom agents require Visual Studio 2026 version 18.4 or later.

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

<!-- TODO: Uncomment when 18.5 releases
:::moniker range="visualstudio"

You can also define user-level agents that apply across all your projects. User-level agents are stored in `%USERPROFILE%\.github\agents` by default. You can change this location in **Tools** > **Options** > **GitHub** > **Copilot**.

:::moniker-end
-->

### Agent file format

Each agent file uses a simple template with YAML frontmatter followed by Markdown instructions:

```markdown
---
name: Code Reviewer
description: Reviews PRs against our team's coding standards
model: claude-opus-4-6
tools: ["code_search", "readfile", "find_references"]
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
| `name` | No | Display name for the agent in the agent picker. If not specified, the agent name is derived from the filename (for example, `code-reviewer.agent.md` becomes `code-reviewer`). |
| `description` | Yes | Brief description shown when hovering over the agent |
| `model` | No | AI model to use. If not specified, uses the model selected in the model picker. |
| `tools` | No | Array of tool names the agent can use. If not specified, all available tools are enabled. |

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
tools: ["code_search", "readfile"]
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
tools: ["code_search", "readfile", "find_references"]
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
tools: ["code_search", "readfile"]
---

You are a design system expert. When reviewing UI code:

1. Check that standard components are used instead of custom implementations
2. Verify spacing and layout follow the design token system
3. Ensure accessibility requirements are met (ARIA labels, keyboard navigation)
4. Flag any UI drift from established patterns

Reference the component library documentation when suggesting fixes.
```

#### Full-stack development agent with Visual Studio tools

The following example uses Visual Studio-specific tool names:

```markdown
---
name: Full Stack Dev
description: Full-stack development assistant with search, file editing, and terminal access
tools: ["code_search", "readfile", "editfiles", "find_references", "runcommandinterminal", "getwebpages"]
---

You are a full-stack development assistant. Help with:

1. Searching the codebase to understand existing patterns
2. Reading and editing files to implement changes
3. Running build and test commands to verify your work
4. Looking up documentation when needed

Always check existing code conventions before making changes.
```

> [!TIP]
> Select the **Tools** icon in the Copilot Chat window to see all available tool names in your version of Visual Studio.

### .NET development agents

The .NET team maintains curated custom agents for C# and Windows Forms development. You can download these agents from the [awesome-copilot](https://github.com/github/awesome-copilot) repository and add them to your project's `.github/agents/` folder.

To get started:

1. Download [CSharpExpert.agent.md](https://github.com/github/awesome-copilot/blob/main/agents/CSharpExpert.agent.md) and [WinFormsExpert.agent.md](https://github.com/github/awesome-copilot/blob/main/agents/WinFormsExpert.agent.md) from the awesome-copilot repository.
1. Add the files to your repository's `.github/agents/` folder.
1. Open Copilot Chat in agent mode and select the agent from the agent picker.

:::moniker range="visualstudio"

> [!TIP]
> Visual Studio can automatically apply .NET-specific agent instructions for your codebase. Select **Tools** > **Options**, and then enable **Enable project specific .NET instructions such as Windows Forms development when applicable**.

:::moniker-end

#### C# Expert

The C# Expert agent provides guidance on modern C# best practices, including:

+ **Core C# development**: Adheres to modern best practices for syntax, structure, and performance while honoring the conventions of your existing repository.
+ **Code integrity**: Implements minimal code changes and writes efficient code that uses async/await patterns with proper cancellation and exception handling.
+ **Testing best practices**: Supports behavior-driven unit testing, integration testing, and TDD workflows.

The agent avoids generating unused interfaces, methods, or parameters, which reduces technical debt and keeps your code readable.

#### WinForms Expert

The WinForms Expert agent specializes in Windows Forms development on .NET 8 through .NET 10. It covers several critical areas:

+ **Designer code protection**: Keeps `.Designer.cs` files safe from corruption so you can continue using the [Windows Forms Designer](../designers/windows-forms-designer-overview.md) after Copilot edits your code.
+ **UI design patterns**: Implements MVVM and MVP patterns for maintainable and scalable WinForms code, including MVVM data binding with the Community Toolkit.
+ **Modern .NET patterns**: Async/await with the correct `InvokeAsync` overloads, dark mode support, high-DPI awareness, and nullable reference types in the right places.
+ **Layout best practices**: Guidance on `TableLayoutPanel` and `FlowLayoutPanel` for responsive, DPI-aware layouts that work across different screen sizes and scaling factors.
+ **CodeDOM serialization**: Rules for property serialization in the WinForms designer, including `[DefaultValue]` attributes and `ShouldSerialize*()` methods.
+ **Exception handling**: Patterns for async event handlers and application-level exception handling to prevent process crashes.

For more information about the Windows Forms Designer, see [What is Windows Forms Designer?](../designers/windows-forms-designer-overview.md).

### Community configurations

The [awesome-copilot repository](https://github.com/github/awesome-copilot) has community-contributed agent configurations you can use as starting points. When using configurations from this repository, verify tool names work in Visual Studio before deploying to your team.

### Limitations and notes

+ If you don't specify a model, the agent uses whatever model is selected in the model picker.
+ Tool names vary across GitHub Copilot platforms. Verify tool names work in Visual Studio before deploying to your team.

## Share feedback

Share your custom agent configurations in the [awesome-copilot repository](https://github.com/github/awesome-copilot) or file feedback through [Visual Studio Developer Community](https://developercommunity.visualstudio.com/). Your workflows help shape future features.

## Related content

+ [Get started with GitHub Copilot agent mode](copilot-agent-mode.md)
+ [Use MCP servers](mcp-servers.md)
+ [Customize chat responses and set context](copilot-chat-context.md)
+ [GitHub Copilot testing for .NET](../test/github-copilot-test-dotnet-overview.md)
+ [GitHub Copilot app modernization overview](/dotnet/core/porting/github-copilot-app-modernization/overview)
