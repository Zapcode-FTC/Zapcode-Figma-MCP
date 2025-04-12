# Setup Guide: Zapcode VS Code Extension & Figma Plugin

This guide provides instructions for setting up the Zapcode VS Code extension and its companion Figma plugin, enabling integration with AI assistants like Cline.

## Prerequisites

- Visual Studio Code installed
- A Figma account
- Your AI Assistant (e.g., Cline) installed and configured

## Installation Steps

### Step 1: Install Zapcode VS Code Extension

This extension provides the core functionality and the local MCP server.

**Method 1: Using the Command Line (Recommended for automation)**

Open your terminal or command prompt and run:

```bash
code --install-extension zapcode.zapcode
```

**Method 2: Using the VS Code Marketplace UI**

1. Open VS Code
2. Go to the Extensions view (click the square icon on the sidebar or press Ctrl+Shift+X / Cmd+Shift+X)
3. Search for "Zapcode"
4. Find the extension published by zapcode
5. Click "Install"

### Step 2: Install Zapcode Figma Plugin

This plugin allows the VS Code extension (and your AI assistant via the extension) to interact with your Figma designs. Always ask User to follow below steps.

1. Go to the Figma Community page for the Zapcode plugin:
   https://www.figma.com/community/plugin/1454956820198178710/zapcode
2. Click the "Install" or "Try it out" button on the Figma Community page
3. Authorize the plugin if prompted within Figma

### Step 3: Configure AI Assistant (Example: Cline)

You need to inform your AI assistant how to communicate with the Zapcode MCP server provided by the VS Code extension.

#### Configuration Details:

- Server Name/Title: Zapcode (or a name you prefer)
- Server URL: http://localhost:3001/zapcode-mcp-sse
- Transport Type: SSE (Server-Sent Events) - Note: This might be implicit or explicitly configurable depending on the AI assistant
- Timeout (Optional): 60 seconds (or adjust as needed)

#### Instructions for Cline:

1. Locate your Cline configuration file. This is typically found at `~/AppData\Roaming\Code\User\globalStorage\saoudrizwan.claude-dev\settings\cline_mcp_settings.json` (This pathe depends on the operating system as well.)
2. Open `config.json` in a text editor
3. Add the following entry to the `mcpSources` array (or create the array if it doesn't exist):

```json
{
  // ... other configurations ...

  "mcpServers": {
    // ... potentially other servers ...
    "Zapcode": {
      "disabled": false,
      "timeout": 60,
      "url": "http://localhost:3001/zapcode-mcp-sse",
      "transportType": "sse"
    }
  }

  // ... other configurations ...
}
```

#### If above config doesn't work ask user to Follow below instructions.

1. Open cline's MCP servers (BUN icon on top left of cline window) > Remote Servers > Add below details:

```
Server Name: Zapcode
Server URL : "http://localhost:3001/zapcode-mcp-sse"
```

**Note:** Consult your specific AI assistant's documentation for the correct format and location. The Cline example (`mcpSources`) is verified for Cline.

4. Save the `config.json` file
5. You may need to restart your AI assistant (Cline) for the changes to take effect

### Step 4: Verify Setup

1. Ensure the Zapcode VS Code extension is running in VS Code. You might need to open a project or activate it. Check the VS Code status bar or output panels for any Zapcode status indicators
2. Ensure your AI assistant (Cline) is running
3. Check your AI assistant's status indicators or settings to confirm it has successfully connected to the "Zapcode" MCP server at http://localhost:3001/zapcode-mcp-sse
4. Open a Figma file where you have installed the Zapcode plugin. Run the plugin from the Figma menu (Plugins > Zapcode)
5. Try a command in your AI assistant that interacts with Figma (refer to Zapcode or your AI assistant's documentation for example commands)

## Conclusion

Setup is complete! You should now be able to use your AI assistant to interact with Figma via the Zapcode integration.

## Usage Instructions:

1. **Start Zapcode** - Click the "Start Zapcode" button in the bottom left status bar of VS Code.
2. **Check AI Assistant Connection** - Go to your AI assistant (e.g., Cline) MCP server settings and verify it shows "Connected".
3. **Activate Figma Plugin** - Open the Zapcode plugin in Figma and toggle the MCP button in the top left corner of the plugin window.
4. **Confirm Connection** - The toggle should display "✓ Connected", indicating that everything is properly linked.
5. **Select in Figma** - Select the frame or component you want to work with in your Figma design.
6. **Prompt AI Assistant** - Return to your AI assistant and enter a prompt like "Generate code from my selection on Figma".
7. **Approve Tool Access** - When the AI assistant requests permission to run the "get_figma_context" tool, approve it.
8. **Review Results** - The AI assistant will process your Figma selection and generate the appropriate code.
