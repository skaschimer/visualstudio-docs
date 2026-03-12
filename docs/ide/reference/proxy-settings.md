---
title: Configure proxy settings in Visual Studio
description: Set a custom proxy server, port, and authentication for Visual Studio to connect through enterprise networks.
ms.date: 03/12/2026
ms.topic: how-to
f1_keywords:
- VS.ToolsOptionsPages.Environment.ProxySettings
monikerRange: 'visualstudio'
author: ghogen
ms.author: ghogen
ms.subservice: general-ide
---

# Configure proxy settings in Visual Studio

By default, Visual Studio uses your Windows proxy configuration. The IDE doesn't override system settings unless you choose to set a custom proxy. If your enterprise network requires a different proxy configuration for Visual Studio, you can set one directly in the IDE through the **Proxy Settings** options page.

> [!NOTE]
> In this first release, the custom proxy settings apply to **GitHub Copilot experiences** and **sign-in flows for Entra ID and GitHub** within Visual Studio. A restart may be required for some features to pick up new proxy settings.

## Prerequisites

- Visual Studio installed. If you don't have it, see [Install Visual Studio](../../install/install-visual-studio.md).

## Open the Proxy Settings page

1. Select **Tools** > **Options** from the menu bar.
1. Select **Proxy Settings** to open the proxy configuration page.

<!-- TODO: Screenshot of the Proxy Settings page
![Screenshot of the Proxy Settings page under Tools > Options.](../../media/proxy-settings.png)
-->

## Default behavior

Out of the box, Visual Studio uses your Windows proxy configuration. You don't need to change any settings unless you require a proxy configuration that differs from your system default.

## Set a custom proxy

If you need a different proxy for Visual Studio:

1. Open the **Proxy Settings** page (**Tools** > **Options** > **Proxy Settings**).
1. Select **Use custom proxy settings**.
1. Enter the **proxy server URL** and **port**.
1. Choose an authentication method:
   - **Use the logged-in Windows account** — uses your current Windows credentials for integrated authentication (NTLM or Kerberos).
   - **Use alternate credentials** — provide a **username** and **password** for the proxy.
1. Select **OK**.
1. Restart Visual Studio if prompted.

> [!TIP]
> If your proxy requires Basic authentication, choose **Use alternate credentials** and enter the credentials your proxy expects.

## Related content

- [Troubleshoot proxy and firewall issues in Visual Studio](proxy-firewall-troubleshoot.md)
- [Install and use Visual Studio behind a firewall or proxy server](../../install/install-and-use-visual-studio-behind-a-firewall-or-proxy-server.md)
