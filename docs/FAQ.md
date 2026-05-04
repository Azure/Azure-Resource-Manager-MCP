# Azure Management MCP Server - Frequently Asked Questions
This FAQ provides answers to common questions about the Azure Management MCP Server, including its
features, usage, troubleshooting, and governance. If you have a question that is not answered here,
please open an issue to ask or suggest improvements to this FAQ!

## What is the difference between Azure Management MCP Server and Azure MCP Server?

The Azure ecosystem includes two MCP servers with complementary roles:

**Azure MCP Server**
- Local MCP server that runs on the client machine.
- Provides a gateway to broader Azure tools and services.

**Azure Management MCP Server**
- Remote MCP server that runs in the cloud.
- Provides direct access to Azure Resource Manager (ARM) APIs and operations.

Both can easily work together to meet your agentic needs!

## Setup & Requirements

### What are the minimum requirements to use the Azure Management MCP Server?

To use the Azure Management MCP Server, you need:

1. **VS Code** installed on your client machine.
2. **A valid Azure Account** with access to at least one Azure tenant and subscription.
3. **Internet connectivity** to reach the cloud-hosted Azure Management MCP Server.
4. An MCP-compatible AI agent or chat interface in VS Code (such as GitHub Copilot Chat).

### Do I need special permissions or roles in Azure to use the server?

Your Azure role and permissions on the account you use are is what is determined for what the MCP
server returns.

### Can I use this with multiple Azure tenants?

Currently you can only query one tenant at a time, there is no way to specify the particular tenant
per the logged in user. The logged in account will default to the default tenant for that account.
To work around this we suggest adding an account with subscription write access to the desired
tenant and switching to that account in VS Code when you want to run queries against that tenant.

## Client Integration

### Which clients are supported?

The Azure Management MCP Server currently works with GitHub Copilot Chat in VS Code and GitHub
Copilot CLI. We are working to expand usage to other clients in the future.

## Reliability & Availability

### What happens if the remote server is unavailable?

If the Azure Management MCP Server becomes temporarily unavailable:

1. **Tool calling operations will fail** with an error indicating connectivity or service
   unavailability.
2. You will receive an error message in your AI chat or client interface.


### Can I use this offline or in disconnected scenarios?

No, the Azure Management MCP Server requires internet connectivity because it is a cloud-hosted
remote service. All tool calling operations must connect to the remote server to access
Azure APIs.

## Security & Data Handling

### What data does the remote server log or retain?

The Azure Management MCP Server captures operational data for tracking tool calls, diagnostics, support,
and security. No input or output data from your tool calls are collected or stored by the server.

### Can I restrict which resources an agent can query or deploy?

The Azure Management MCP Server respects Azure's authorization layer—if your account lacks
permissions to query or deploy a resource, the server will deny the operation.

You can explicitly block any deployment from the Azure Management MCP Server by applying an Azure
Policy that denies deployments from that service, see the [README
Governance](./README.md#governance) for more details.
