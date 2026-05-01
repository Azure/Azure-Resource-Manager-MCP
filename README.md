# Azure Management MCP Server

This is a repository to track features, bugs, and suggestions for the Azure Management MCP Server.

## Overview
Azure Resource Manager (ARM) is the control plane of Azure. Every operation that creates, updates,
or deletes Azure resources flows through ARM, regardless of whether it comes from the Azure portal,
CLI, PowerShell, REST APIs, or SDKs.

AI agents introduce a new kind of Azure client that needs a consistent, centralized way to interact
with ARM. The **Azure Management MCP Server** is designed to provide that access layer through the Model
Context Protocol (MCP), the standard protocol agents use to perform actions and retrieve dynamic
data.

In practice, the **Azure Management MCP Server** equips agents with tools to generate, validate, and
execute Azure Resource Graph (ARG) queries, and to deploy and manage ARM templates. Its core purpose
is to enable both AI agents to interact with Azure resources seamlessly, just like other ARM clients.

## Features
The **Azure Management MCP Server** provides the following key features:
- Generate ARG queries dynamically based on user or agent input.
- Validate ARG queries for correctness and security.
- Execute ARG queries against your Azure environment.
- Deploy ARM templates to Azure.
- Check ARM template deployment status.
- Cancel ARM template deployments in progress.

Below is a table showing the tools provided by the Azure Management MCP Server:

| Tool            | Input                                      | Output                                      | Purpose                                      | Example AI Use Case                         |
|-----------------|--------------------------------------------|---------------------------------------------|----------------------------------------------|---------------------------------------------|
| execute_query   | ARG query parameters        | Query results                        | Runs queries and returns results             | Fetching user-requested data                |
| generate_query  | Natural language prompt or requirements     | Generated ARG query        | Creates queries from natural language        | Translating user questions into queries     |
| validate_query  | ARG query                  | Validation result (success/error message)   | Checks queries for correctness and safety    | Ensuring queries are valid before execution |
| create_template_deployment  | Subscription ID, resource group, deployment name, ARM template definition | Deployment initiation response | Starts an ARM template deployment in a target resource group | Deploying infrastructure requested by a user |
| get_arm_template_deployment_status  | Subscription ID, resource group, deployment name | Current deployment status and details | Monitors deployment progress and outcome | Checking whether a deployment succeeded or failed |
| cancel_arm_template_deployment  | Subscription ID, resource group, deployment name | Cancellation result | Stops an in-progress ARM template deployment | Halting a deployment after validation or policy concerns |


## Getting Started

### Prerequisites
- VS Code installed 
- Valid Azure Account

### Installation

#### 1. Installing the MCP Server
1. Open: **https://aka.ms/JoinAzMgmtMCP**. VS Code will launch automatically. 

2. When prompted inside VS Code, click **Install** under **Azure Management MCP Server** to add it to your MCP server configuration.

3. You will be prompted to sign in with your Azure credentials. 

#### 2. Open the Chat Interface
1. In VS Code, go to **View > Chat**, or click the chat icon to the right of the center toolbar
   header.
2. In the Chat window, click the **Configure Tools** icon.  
3. Ensure **Azure Management MCP Server** is checked. You can click the dropdown icon to see the available tools under
   it:
  - **execute_query**   
  - **generate_query**  
  - **validate_query**
  - **create_template_deployment**
  - **get_arm_template_deployment_status**
  - **cancel_arm_template_deployment**

## Usage

1. Open the Chat interface in VS Code.
2. Ensure the Azure Management MCP Server tools are enabled.
3. Type your query or request in natural language.

![Demo GIF](./docs/media/AzMgmtDemo.gif)

## Troubleshooting

See the [Troubleshooting Guide](./docs/Troubleshooting.md) for common issues and solutions when
using the Azure Management MCP Server.

## Governance

The Azure Management MCP Server uses the same authentication and authorization context as the signed-in user in VS Code. This means that all tool calls are made on behalf of that user and are subject to the same permissions and access controls defined in Azure. 

### Blocking Template requests
To prevent any deployments from being made via the ARM MCP server you can apply an Azure Policy to
the relevant scope (subscription or resource group) that denies request the deployment tool
(`create_template_deployment`). To see an example of such a policy, please refer to [this sample
policy](./docs/BlockingDeploymentsPolicy.json). You will need to specifically block the AppID of the
MCP server, which is `22bfbae3-f4e7-485f-be43-8cee15065084`.

## Contributing

This repository is dedicated solely to gathering feedback from users and contributors. While
contributions aimed at clarifying wording or improving documentation details are welcome, the
primary purpose of this repository is to facilitate feedback through the creation of issues. Please
use issues to share your thoughts, suggestions, or concerns, as this helps us better understand and
address your problems!

## Code of Conduct

This project has adopted the [Microsoft Open Source Code of Conduct](https://opensource.microsoft.com/codeofconduct/). For more information, see the [CODE_OF_CONDUCT.md](./docs/CODE_OF_CONDUCT.md) file.

## Transparency FAQ

For more information about how the Azure Management MCP Server works, its limitations, and best practices for use, please refer to our [Transparency FAQ](./docs/TransparencyFAQ.md).

## License
This project is licensed under the MIT License. See [LICENSE](LICENSE) for details.

## Trademarks

This project may contain trademarks or logos for projects, products, or services. Authorized use of
Microsoft trademarks or logos is subject to and must follow Microsoft’s Trademark & Brand
Guidelines. Use of Microsoft trademarks or logos in modified versions of this project must not cause
confusion or imply Microsoft sponsorship. Any use of third-party trademarks or logos are subject to
those third-party’s policies.

