# Azure Management MCP Server

This is a repository to track features/bugs/suggestions for the Azure Management MCP Server

## Table of Contents
- [Overview](#overview)
- [Features](#features)
- [Getting Started](#getting-started)
    - [Prerequisites](#prerequisites)
    - [Installation](#installation)
- [Usage](#usage)
- [Contributing](#contributing)
- [Troubleshooting](#troubleshooting)
- [Roadmap](#roadmap)
- [License](#license)

## Overview
The Azure Management MCP Server is designed to give your AI Agent the tools necessary to generate, validate, and
execute Azure Resource Graph (ARG) queries. It acts as a backend service that enables AI agent
mode to access real-time, relevant data from your Azure environment, improving automation and
decision-making capabilities.

## Features
The Azure Management MCP Server provides the following key features:
- Generate ARG queries dynamically based on user or agent input.
- Validate ARG queries for correctness and security.
- Execute ARG queries against your Azure environment.

Below is a table showing the tools provided by the Azure Management MCP Server:

| Tool            | Input                                      | Output                                      | Purpose                                      | Example AI Use Case                         |
|-----------------|--------------------------------------------|---------------------------------------------|----------------------------------------------|---------------------------------------------|
| execute_query   | ARG query parameters        | Query results                        | Runs queries and returns results             | Fetching user-requested data                |
| generate_query  | Natural language prompt or requirements     | Generated ARG query        | Creates queries from natural language        | Translating user questions into queries     |
| validate_query  | ARG query                  | Validation result (success/error message)   | Checks queries for correctness and safety    | Ensuring queries are valid before execution |


## Getting Started

### Prerequisites
- VS Code installed 
- Valid Azure Account

### Installation

#### 1. Installing the MCP Server
1. Open: **https://aka.ms/JoinARMMCP**. VS Code will launch automatically. 

2. When prompted inside VS Code, click **Install** under **Azure Management MCP Server** to add it to your MCP server configuration.

3. You will be prompted to sign in with your Azure credentials. Use the same account that has access
   to your allowlisted tenant.

#### 2. Open the Chat Interface
1. In VS Code, go to **View > Chat**, or click the chat icon to the right of the center toolbar
   header.
2. In the Chat window, click the **Configure Tools** icon.  
3. Ensure **Azure Management MCP Server** is checked. You can click the dropdown icon to see three tools under
   it:
   - **execute_query**   
   - **generate_query**  
   - **validate_query**  

## Usage

1. Open the Chat interface in VS Code.
2. Ensure the Azure Management MCP Server tools are enabled.
3. Type your query or request in natural language.

[Demo GIF](./docs/media/Azure_Management_MCP_Server_Demo1.gif)

## Contributing

This repository is dedicated solely to gathering feedback from users and contributors. While
contributions aimed at clarifying wording or improving documentation details are welcome, the
primary purpose of this repository is to facilitate feedback through the creation of issues. Please
use issues to share your thoughts, suggestions, or concerns, as this helps us better understand and
address your problems!

## Troubleshooting
- Ensure your Azure credentials are correct and have sufficient permissions.
- If you encounter issues, please create an issue in this repository with detailed information about
  the problem.
- Check the logs in the `Output` panel, attached to the MCP or GitHub Copilot chat session in VSCode
  for a detailed view of the operations and any errors.

## Transparency FAQ

For more information about how the Azure Management MCP Server works, its limitations, and best practices for use, please refer to our [Transparency FAQ](./docs/media/TransparencyFAQ.md).

## License
This project is licensed under the MIT License. See [LICENSE](LICENSE) for details.


