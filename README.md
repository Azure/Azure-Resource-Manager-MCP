# <img src="./docs/media/ARM.png" alt="ARM Icon" width="24" height="24"> ARM MCP Server

This is a repository to track features/bugs/suggestions for the ARM (Azure Resource Manager) MCP Server

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
The ARM MCP Server is designed to give your AI Agent the tools necessary to generate, validate, and
execute Azure Resource Graph (ARG) queries. It acts as a backend service that enables AI agent
mode to access real-time, relevant data from your Azure environment, improving automation and
decision-making capabilities.

## Features
The ARM MCP Server provides the following key features:
- Generate ARG queries dynamically based on user or agent input.
- Validate ARG queries for correctness and security.
- Execute ARG queries against your Azure environment.

Below is a table showing the tools provided by the ARM MCP Server:

| Tool            | Input                                      | Output                                      | Purpose                                      | Example AI Use Case                         |
|-----------------|--------------------------------------------|---------------------------------------------|----------------------------------------------|---------------------------------------------|
| execute_query   | ARG query parameters        | Query results                        | Runs queries and returns results             | Fetching user-requested data                |
| generate_query  | Natural language prompt or requirements     | Generated ARG query        | Creates queries from natural language        | Translating user questions into queries     |
| validate_query  | ARG query                  | Validation result (success/error message)   | Checks queries for correctness and safety    | Ensuring queries are valid before execution |


## Getting Started

### Prerequisites
We are currently in a **limited public preview** for the ARM MCP Server. To gain access, you will
need to have your Azure Tenant allowlisted. Please fill out the [access request
form](https://aka.ms/arm-mcp-server-access-request) to get started.

Other prerequisites include:
- VS Code installed 
- Valid Azure Account

### Installation

> ![Important](https://img.shields.io/badge/Important-Read%20Before%20You%20Begin-red)
> You will need to have your Azure Tenant allowlisted to use the ARM MCP Server. Please fill out the [access request form](https://aka.ms/arm-mcp-server-access-request) before proceeding with installation.

#### 1. Join the ARM MCP Program
1. Open: **https://aka.ms/JoinARMMCP**. VS Code will launch automatically. 

2. When prompted inside VS Code, click **Install** under **ARM MCP Server** to add it to your MCP server configuration.

3. You will be prompted to sign in with your Azure credentials. Use the same account that has access
   to your allowlisted tenant.

#### 2. Open the Chat Interface
1. In VS Code, go to **View > Chat**. or click the chat icon to the right of the center toolbar
   header.
2. In the Chat window, click the **Configure Tools** icon.  
3. Ensure **ARM MCP Server** is checked. You can click the dropdown icon to see three tools under
   it:
   - **execute_query**   
   - **generate_query**  
   - **validate_query**  

## Usage

1. Open the Chat interface in VS Code.
2. Ensure the ARM MCP Server tools are enabled.
3. Type your query or request in natural language.

[Demo GIF](./docs/media/ARM_MCP_Server_Demo1.gif)

## Contributing

This repository is dedicated solely to gathering feedback from users and contributors. While
contributions aimed at clarifying wording or improving documentation details are welcome, the
primary purpose of this repository is to facilitate feedback through the creation of issues. Please
use issues to share your thoughts, suggestions, or concerns, as this helps us better understand and
address your problems!

## Troubleshooting
- Ensure your Azure credentials are correct and have sufficient permissions.
- Verify that your Azure Tenant is allowlisted for the ARM MCP Server. By checking the email you
  requested the access with, you should have received a confirmation once your tenant was approved.
- If you encounter issues, please create an issue in this repository with detailed information about
  the problem

## License
This project is licensed under the MIT License. See [LICENSE](LICENSE) for details.
