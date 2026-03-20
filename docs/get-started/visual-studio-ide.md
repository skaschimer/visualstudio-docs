---
title: What Is Visual Studio?
titleSuffix: ''
description: Explore Visual Studio, an integrated development environment (IDE) that enables you to develop, edit, debug, version control, and deploy your app.
ms.date: 3/20/2026
ms.subservice: general-ide
ms.topic: overview
ms.update-cycle: 90-days
ms.custom: 
- vs-acquisition
- awp-ai
ai-usage: ai-assisted
f1_keywords:
- vs.startpage
- VS.StartPage.HowDoI
author: anandmeg
ms.author: meghaanand
manager: mijacobs
#customer intent: As a developer, I want to understand the features of Visual Studio so that I can decide which features are useful to me.
---
# What is Visual Studio?

Visual Studio is a powerful integrated development environment (IDE) for Windows that you can use to complete the entire development cycle in one place. You can develop, build, debug, test, and deploy your apps—all in one place. Visual Studio includes compilers, code completion tools, source control, extensions, and many more features to enhance every stage of the software development process. With built-in AI assistance from [GitHub Copilot](../ide/visual-studio-github-copilot-extension.md), you can also accelerate your workflow with intelligent code completions, chat-based guidance, and AI-powered debugging.

> [!NOTE]
> Visual Studio is available for Windows. For a lightweight, cross-platform code editor, see [Visual Studio Code](https://code.visualstudio.com/).

:::image type="content" source="media/visualstudio/visual-studio-overview.png" alt-text="Diagram showing the Visual Studio development cycle: develop, build, debug, test, and deploy, with AI assistance integrated throughout.":::

With the variety of features and language support in Visual Studio, you can grow from writing your first "Hello World" program to developing and deploying apps. For example, build, debug, and test apps in C#, C++, Python, JavaScript, TypeScript, and more. Develop cross-platform mobile and desktop apps with .NET MAUI, build web apps with ASP.NET, or create Node.js services.


## Install Visual Studio

Visual Studio is available in three editions:

- [Community](https://visualstudio.microsoft.com/vs/community/). Free and fully featured for students, open-source developers, and individual developers.
- [Professional](https://visualstudio.microsoft.com/vs/professional/). For individual developers or small teams.
- [Enterprise](https://visualstudio.microsoft.com/vs/enterprise/). For small-to-large business and enterprise organizations.

[Compare features across editions](https://visualstudio.microsoft.com/vs/compare/) to find the edition that best fits your needs.

::: moniker range="vs-2022"

 > [!div class="button"]
 > [Download Visual Studio](https://aka.ms/vs/download/?cid=learn-onpage-download-cta)

::: moniker-end

::: moniker range="visualstudio"

 > [!div class="button"]
 > [Download Visual Studio](https://aka.ms/vs/download/?cid=learn-onpage-download-install-visual-studio-page-cta)

::: moniker-end

For more information, see [Install Visual Studio](../install/install-visual-studio.md).

## Why use Visual Studio?

Visual Studio provides developers with a feature-rich development environment to develop code efficiently and collaboratively.

- Workload-based installer. Install only what you need.
- Powerful coding tools and features. Everything you need to build your apps in one place.
- Multiple-language support. Code in C++, C#, JavaScript, TypeScript, Python, and more.
- Cross-platform development. Build apps for any platform.
- Version control integration. Collaborate on code with teammates.
- AI-assisted development. Write code efficiently with AI assistance.

## Discover Visual Studio

Visual Studio supports different parts of the software development cycle.

### Develop your code

The Visual Studio [code editor](../ide/writing-code-in-the-code-and-text-editor.md) helps you write and manage code with confidence. Use light bulb suggestions for quick fixes, outlining to collapse code blocks, and **Solution Explorer** or **Class View** to navigate your projects.

Learn more about features in the IDE that help you organize and edit content:

- [Code editor](tutorial-editor.md)
- [Tips and tricks](../ide/productivity-features.md)

### Develop with AI

[GitHub Copilot](../ide/visual-studio-github-copilot-get-started.md) and [IntelliCode](../ide/intellicode-visual-studio.md) assist you in writing code faster and with greater accuracy. Use [Copilot Completions](../ide/visual-studio-github-copilot-extension.md) for inline code suggestions as you type, and [Copilot Chat](../ide/visual-studio-github-copilot-chat.md) to ask questions, generate code, or refactor existing code through natural language. These tools also help with other development tasks such as writing unit tests, [debugging](../debugger/debug-with-copilot.md), and profiling.

Learn more about [AI-assisted development in Visual Studio](../ide/ai-assisted-development-visual-studio.md).

### Build your app

You can compile and build your applications to create builds immediately and test them in a debugger. You can run multi-processor builds for C++ and C# projects. Visual Studio also provides several options that you can configure when you build applications. You can create a custom build configuration, use the built-in configurations, hide certain warning messages, or increase build output information.

Learn more about how to [compile and build in Visual Studio](../ide/compiling-and-building-in-visual-studio.md).

### Debug your code

Integrated debugging in Visual Studio enables you to easily debug, profile, and diagnose code. You can step through your code and look at the values stored in variables, set watches on variables to see when values change, and examine the execution path of your code. Visual Studio also provides other ways to debug your code while it runs.

Learn more about debugging in Visual Studio:

- [First look at the debugger](../debugger/debugger-feature-tour.md)
- [Debug with Copilot](../debugger/debug-with-copilot.md)

### Test your code

You can write high-quality code by using comprehensive testing tools in Visual Studio. Unit tests give developers and testers a quick way to find logic errors in code. You can analyze how much code you're testing and see instant results in a test suite. Know the impact of every change you make by using advanced features that test code while you type.

Learn more about the testing tools available in Visual Studio:

- [Use testing tools in Visual Studio](../test/improve-code-quality.md)
- [Get started with unit testing](../test/getting-started-with-unit-testing.md)

### Manage version control

By using the integrated Git features in Visual Studio, you can clone, create, or open your own repositories. The Git tool window provides everything you need to commit and push changes, manage branches, and resolve merge conflicts. If you have a GitHub account, you can manage repos directly within Visual Studio.

Learn more about [version control with Git in Visual Studio](../version-control/git-with-visual-studio.md).

### Collaborate with your team

Visual Studio includes collaboration features to help you work with your team. Use the integrated [Git tooling](../version-control/git-with-visual-studio.md) for code reviews and pull requests, or share your editing session in real time with [Live Share](/visualstudio/liveshare/quickstart/share).

### Deploy your app

When you deploy an application, service, or component, you distribute it for installation on other computers, devices, or servers, or in the cloud. You can choose the appropriate method in Visual Studio for the type of deployment that you need. Share your apps and code by publishing to the web or Azure, or by deploying to a network share or a local folder.

Learn more about how to [deploy your app from Visual Studio](../deployment/deploying-applications-services-and-components.md).

## Get started

Choose a language-specific tutorial to start building your first app:

- [C#](./csharp/tutorial-console.md) — Build a simple console app and learn the basics of C# and .NET.
- [C++](/cpp/get-started/tutorial-console-cpp) — Create a C++ console app and explore the build toolchain.
- [Python](/visualstudio/python/installing-python-support-in-visual-studio) — Set up Python support and write your first script.
- [JavaScript/Node.js](../javascript/tutorial-nodejs.md) — Build a Node.js and Express web app.
- [Visual Basic](./visual-basic/tutorial-console.md) — Create a simple console app with Visual Basic.
- [F#](tutorial-fsharp-web-app.md) — Build a web app with F# and ASP.NET Core.

## Next step

- [Tour the IDE](../ide/quickstart-ide-orientation.md) to get familiar with the IDE features and to learn how to use it for basic tasks.

