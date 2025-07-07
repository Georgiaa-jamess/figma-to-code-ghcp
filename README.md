# figma-to-code-ghcp
A step-by-step guide to converting Figma wireframes into production-ready code using GitHub Copilot.

# ✨ Figma-To-Code Automation With GitHub Copilot

Welcome to the **Figma-to-Code** journey - where design meets development with the power of **GitHub Copilot**. This guide walks you through the set-up and best practices for turning wireframes into working code, using a streamlined workflow that connects:

- 🎨 **Figma** for wireframing and UI design.
- 🧠 **GitHub Copilot** for intelligent code generation.
- 🛠️ **Visual Studio Code** for building and refining your components.  

Figma to code - no magic, just GitHub Copilot and a sprinkle of MCP.

---

## 📃 Prerequisites

1. Visual Studio Code installed.
2. GitHub Copilot account configured.

## 🔎 Finding Your Figma API Key

To connect your MCP server to Figma, you’ll need your unique API key. Follow the steps below to locate it.

1. Open **Figma**.
2. Click **Account** >> **Settings** >> **Security**.
<img width="189" alt="Screenshot 2025-07-07 155524" src="https://github.com/user-attachments/assets/85e064ae-8aee-4cd1-80fa-465e872d8098" />

3. Scroll to **Personal access tokens** >> **Generate new token**.
<img width="431" alt="Screenshot 2025-07-07 160112" src="https://github.com/user-attachments/assets/be83ebef-0a61-4016-ad41-0f3322ebf60c" />

4. Enter a name for the token and make sure you have **read** permissions on **File content** and **Dev resources**, then click Generate token.
<img width="355" alt="Screenshot 2025-07-07 160507" src="https://github.com/user-attachments/assets/0122e1b1-498c-4d1c-97b8-a749a19d67d6" />

5. Make sure to copy the generated token and save it in a secure, access-controlled environment.

## 🚀 Setting Up The MCP Server

While multiple MCP servers are available, the one shown below was developed by Framelink. (https://www.framelink.ai/docs)

To configure the **figma-developer-mcp** server, simply add the following entry to your **mcp.json** configuration file located in your **.vscode** folder:

## Mac OS/Linux
```bash
{
  "mcpServers": {
    "Framelink Figma MCP": {
      "command": "npx",
      "args": ["-y", "figma-developer-mcp", "--figma-api-key=<YOUR-KEY>", "--stdio"]
    }
  }
}
```
## Windows
```bash
{
  "mcpServers": {
    "Framelink Figma MCP": {
      "command": "cmd",
      "args": ["/c", "npx", "-y", "figma-developer-mcp", "--figma-api-key=<YOUR-KEY>", "--stdio"]
    }
  }
}
```
**Remember to update the Figma API key using your unique token retrieved in the previous step.**

Once the MCP server is up and running, it will automatically extend the available tools in GitHub Copilot to include:

 - **download_figma_images**
 - **get_figma_data**

You can confirm this by opening **GitHub Copilot**, navigating to **Configure Tools**, and scrolling to **MCP Server: Framelink Figma MCP** in the list.

<img width="199" alt="Screenshot 2025-07-07 162443" src="https://github.com/user-attachments/assets/3f8a51e0-dd90-437f-b237-fb20b9766834" />

<img width="439" alt="image" src="https://github.com/user-attachments/assets/21b877fb-d5de-4eb4-b060-32690cd7726a" />





