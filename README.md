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

To connect your MCP server to Figma, you’ll need your unique API key. Follow the steps below to locate it:

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
  "servers": {
    "Framelink Figma MCP": {
      "command": "cmd",
      "args": [
        "/c",
        "npx",
        "-y",
        "figma-developer-mcp",
        "--figma-api-key=<YOUR-KEY>",
        "--stdio"
      ]
    }
  }
}
```
**Remember to update the Figma API key using your unique token retrieved in the previous step.**

Once the MCP server is up and running, it will automatically extend the available tools in GitHub Copilot to include:

 - **download_figma_images** - Downloads SVG and PNG images used in a Figma file based on image or icon node IDs.
 - **get_figma_data** - Fetches information about a Figma file or a specific node within a file.

You can confirm this by opening **GitHub Copilot**, navigating to **Configure Tools**, and scrolling to **MCP Server: Framelink Figma MCP** in the list.

<img width="199" alt="Screenshot 2025-07-07 162443" src="https://github.com/user-attachments/assets/3f8a51e0-dd90-437f-b237-fb20b9766834" />

<img width="439" alt="image" src="https://github.com/user-attachments/assets/21b877fb-d5de-4eb4-b060-32690cd7726a" />


## 🔗 Generating Code From A Figma Design

Here comes the fun bit - generating code! Just follow the steps below to get GitHub Copilot working its magic on your Figma wireframes:

1. In **Figma**, navigate to your design.
2. Select the wireframe you intend to use. **Right click** >> **Copy/paste as** >> **Copy link to selection**.
<img width="482" alt="Screenshot 2025-07-07 164537" src="https://github.com/user-attachments/assets/582b0689-e431-4cb4-b1fb-e6de7dd81e08" />

3. After copying the Figma link, create a prompt in **GitHub Copilot Agent Mode** using that link.
<img width="377" alt="Screenshot 2025-07-07 165105" src="https://github.com/user-attachments/assets/e801977a-a1f0-4605-af1e-a40d0754c6e3" />

**Need tips for prompt engineering? Refer to the Best Practices section below.**

## 💪 Best Practices

To ensure high-quality, consistent code generation from your Figma designs using GitHub Copilot and MCP, follow these best practices:

## 🧠 Prompt Engineering

Crafting effective prompts is key to getting high-quality, production-ready code from GitHub Copilot. Here’s how to guide the model with precision:

#### 🎯 Be Specific and Context-Rich
- Include the Figma link, desired framework, and output format in your prompt.
  - Example prompt: **Generate a responsive React 18 component using Tailwind CSS based on this Figma frame: https://www.figma.com/file/xyz123**

#### 🧩 Specify Coding Language & Version
- Always mention the language and version you want Github Copilot to use (e.g. React 18, TypeScript 5.3). This helps the model align with your project setup and avoid deprecated syntax.
- Include a package.json and tsconfig.json in your workspace to give GitHub Copilot additional context.
  
#### 🎨 Guide Styling Choices
- Prefer external styling over inline styles? Mention your preferred method:
  - Tailwind CSS for utility-first styling.
  - CSS Modules or styled-components for scoped styles.
- If you have your own custom CSS or SCSS files, you can reference them directly in your prompt:
  - Example Prompt: **Use styles from ./styles/components/ but do not generate new styles unless needed**

#### 🧠 Model Selection & Prompt Scope
- If available, choose a model optimised for front-end generation (e.g. gpt-4-turbo).
- For complex UIs, break prompts into smaller parts (e.g. header, sidebar, footer) and stitch them together.
  
#### 🗂️ Use File Context to Your Advantage
- Copilot uses surrounding code and file structure to improve its predictions.
- Utilise a folder structure to organise generated code.

## 📁 Folder Structure
- Create a dedicated folder (e.g. /figma-wireframes/) to store:
  - Figma links and metadata
  - Generated components
  - Associated assets (SVGs, PNGs)
- Use a consistent naming convention for components (e.g. ButtonPrimary.tsx, NavHeader.tsx) to make reuse and testing easier.

## 🧪 Testing & Validation
- Always review generated code for:
1. Accessibility (ARIA roles, keyboard navigation)
2. Semantic HTML
3. Performance (avoid unnecessary re-renders)
   
**Make sure to validate component behaviour visually and functionally.**

## 🔐 Security & API Keys
- Never hardcode your Figma API key. Use environment variables or .env files and add them to .gitignore.
- Rotate tokens regularly and limit their scope to read-only access.

## ✨ Making it work in the Enterprise
-  MCP 5000 Port needs to be open on the network for Visual Studio Code to access MCP servers. VPN access should allow in order to communicate with MCP servers.
- MCP.json should not be excluded with code exclusions. How to do it: **Excluding content from GitHub Copilot: https://docs.github.com/en/enterprise-cloud@latest/copilot/how-tos/content-exclusion/excluding-content-from-github-copilot**
