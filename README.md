# ZapCode Figma MCP Server

<p align="center"><img src="./assets/Zapcode.png" alt="ZapCode Logo" width="400"></p>

Connect your Figma designs directly to your AI coding assistant! This tool acts as a bridge, allowing AI assistants that support the **Model Context Protocol (MCP)** to access real-time context from your selected Figma frames.

This server connects to the Zapcode Figma plugin to retrieve real-time context from your selected Figma frame, including its HTML/CSS structure, a generated image, and any exportable SVG assets. When invoked by an AI model, it provides this rich context, automatically extracts any SVG assets from the selection, saves them to your local workspace, and informs the LLM of their location.

## Quick Install & Usage

This server is designed to be run directly via `npx`, requiring no permanent installation.

### Prerequisites

1.  **Node.js**: Ensure you have Node.js (v16 or higher) installed. You can download it from [nodejs.org](https://nodejs.org/).
2.  **ZapCode Figma Plugin**: You must install the companion plugin from the Figma Community.
    - **Installation Link:** [Zapcode - Figma Plugin](https://www.figma.com/community/plugin/1454956820198178710/zapcode)

### Integration with your AI Assistant

Configure your AI assistant to launch the server automatically. Here are some examples:

#### GitHub Copilot

In your Copilot configuration, add the following:

```json
{
  "servers": {
    "Zapcode stdio mcp": {
      "type": "stdio",
      "command": "npx",
      "args": ["zapcode-figma-mcp"]
    }
  },
  "inputs": []
}
```

#### Claude for Desktop

Open your `claude_desktop_config.json` file and add the following to `mcpServers`:

- **macOS/Linux:** `~/Library/Application Support/Claude/claude_desktop_config.json`
- **Windows:** `%APPDATA%\Claude\claude_desktop_config.json`

````json
{
  "mcpServers": {
    "zapcode-figma-mcp": {
      "command": "npx",
      "args": ["zapcode-figma-mcp"]
    }
  }
}
```**Note:** Restart Claude for Desktop for the changes to take effect.

#### Other MCP Clients (e.g., Cline, Open WebUI)

For other clients, add a server configuration pointing to the `npx` command:

```json
{
  "mcpServers": {
    "zapcode-figma-mcp": {
      "command": "npx",
      "args": ["zapcode-figma-mcp"]
    }
  }
}
````

### Usage Steps

1.  **Run the ZapCode Plugin:** Open your design file in the Figma desktop app and run the ZapCode plugin.
2.  **Use Your AI Assistant:** Select a frame or component in Figma. Go to your code editor and instruct your AI Assistant to perform a task. For example:
    - _"Generate a React component based on the current Figma selection."_
    - _"Create HTML and CSS for the selected Figma frame."_
3.  **Automatic Context Fetching:** Your AI assistant will automatically launch the `zapcode-figma-mcp` server, which will connect to the Figma plugin and fetch the necessary context to complete your request.

---

## Additional Information

### How It Works

Modern AI coding assistants often lack direct insight into your visual design process. This server solves that problem by:

1.  Running as a local process initiated by your MCP-compatible AI assistant.
2.  Establishing a connection with the **ZapCode Figma Plugin** when a request is made.
3.  Receiving context (structure, styles, assets) from the currently selected Figma frame.
4.  Serving this context to the AI assistant via the Model Context Protocol.
5.  Your AI assistant then uses this information to generate code that more accurately reflects your design.

### Features

- **Real-time Connection:** Establishes a direct, local link between the ZapCode Figma Plugin and your AI Assistant.
- **MCP Server:** Hosts a local MCP server discoverable by compatible AI clients.
- **Figma Context Tool:** Provides the `get_figma_context` tool, enabling AI assistants to request data about the currently selected Figma frame(s).
- **Secure & Local:** All communication happens on your machine; no design data is sent to external servers.

### Tool Details: `get_figma_context`

This server exposes a single, powerful tool to the LLM.

- **Description**: Retrieves the selected Figma frame context. Saves any provided SVG assets to the local `assets/svg` directory.
- **Input Schema**: `{}` (No input arguments are required).
- **Output**: A combination of prompts and Figma context.

### Troubleshooting

- `Error: Figma plugin is not connected.`

  - This is the most common error. It means the MCP server is running but cannot find the Zapcode Figma plugin.
  - **Solution:** Make sure you have opened the Figma desktop app and are running the Zapcode plugin on the design file you wish to query.

- `Port Conflict / EADDRINUSE Error`
  - If you see an error that a port is already in use, it means another application is using port `3001` or `32896`.
  - **Solution:** Stop the other application that is occupying the port.

### Enterprise & Custom Integration

Boost your team's development speed and ensure brand consistency by integrating this system directly with your company's workflow.

We offer professional services to:

- Integrate the MCP server with your specific enterprise environment.
- Connect your proprietary design systems for seamless code generation.
- Develop custom features tailored to your team's needs.

Contact us to learn how we can help you accelerate your development lifecycle: **subscribezapcode@gmail.com**

### License

This project is licensed under the MIT License.
