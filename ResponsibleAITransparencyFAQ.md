# Azure Resource Manager MCP server: Transparency FAQ

## What is Azure Resource Manager MCP server?

Azure Resource Manager MCP server is an AI-assisted tool that helps you query and manage your Azure
resources using natural language. It can translate requests into Azure Resource Graph (ARG) queries,
manage ARM deployments and resources, inspect resource type metadata, and retrieve Azure cost and
pricing information.

## What can Azure Resource Manager MCP server do?

Azure Resource Manager MCP server provides these core capabilities:
- **Query Azure resources**: Generate, validate, and execute ARG queries
- **Preview ARM deployments**: Show the changes an ARM template deployment would make
- **Manage ARM deployments**: Create, monitor, and cancel resource group deployments
- **Monitor asynchronous operations**: Check the status of long-running ARM resource operations
- **Manage Azure resources**: Create or update individual resources and resource groups
- **Inspect resource types**: Discover resource types, current API versions, and JSON schemas
- **Analyze costs**: Query Azure cost and usage data, including AKS cost breakdowns
- **Retrieve pricing**: Look up public retail prices and download EA or MCA pricesheets

## What are Azure Resource Manager MCP server's intended uses?

The system is designed for Azure administrators, engineers, and operators who need to:
- Query resources and properties across their Azure environment
- Support decision-making through real-time Azure data access
- Reduce time spent learning ARG query syntax
- Enable more users to interact with Azure resources through natural language
- Deploy and manage infrastructure using ARM templates or direct resource operations
- Analyze Azure costs and compare public or negotiated pricing

## How was Azure Resource Manager MCP server evaluated? What metrics are used to measure performance?

The system has been evaluated on the ability to provide syntactically correct ARG queries, the
relevance of generated queries to user prompts, and feedback given through the Azure Copilot
experience in the Azure Portal.

## What are the limitations of Azure Resource Manager MCP server? How can users minimize impact?

**Limitations:**
- ARG queries are limited to resources and properties indexed by Azure Resource Graph
- Results and resource operations depend on your Azure permissions
- Natural language interpretation may occasionally produce unexpected query structures
- Retail prices are public list prices and may differ from negotiated prices

**How to minimize impact:**
- Review generated queries before execution or ask the system to validate them first
- Review deployment previews and resource changes before approving write operations
- Ensure your Azure credentials have appropriate permissions for the intended operation
- Use the validation tool to catch errors before running queries
- Start with specific, well-defined requests rather than overly broad natural language prompts

## What operational factors and settings allow for effective and responsible use?

The system performs optimally when:
- You provide clear, specific requests in natural language
- Your Azure credentials have appropriate permissions for queried resources and requested operations
- You review generated queries, deployment previews, and resource changes before execution
- You use the system within your organization's AI and Azure governance policies
