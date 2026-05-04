# Azure Management MCP Server: Transparency FAQ

## What is Azure Management MCP Server?

Azure Management MCP Server is an AI-assisted tool that helps you query and manage your Azure
resources using natural language. It takes your questions or requirements in plain English and
converts them into Azure Resource Graph (ARG) queries—the language Azure uses to find and retrieve
information about your resources.

## What can Azure Management MCP Server do?

Azure Management MCP Server provides six core capabilities:
- **Generate queries**: Convert natural language requests into valid ARG queries
- **Validate queries**: Check queries for correctness, syntax, and security before execution
- **Execute queries**: Runs queries against your Azure environment and returns results
- **Create ARM template deployments**: Deploy infrastructure as code using ARM templates
- **Get ARM template deployment status**: Check the progress and outcome of your deployments
- **Cancel ARM template deployments**: Stop in-progress deployments if needed

## What are Azure Management MCP Server's intended uses?

The system is designed for Azure administrators, engineers, and operators who need to:
- Query resources and properties across their Azure environment
- Support decision-making through real-time Azure data access
- Reduce time spent learning ARG query syntax
- Enable more users to interact with Azure resources through natural language
- Easily deploy and manage infrastructure using ARM templates

## How was Azure Management MCP Server evaluated? What metrics are used to measure performance?

The system has been evaluated on the ability to provide syntactically correct ARG queries, the
relevance of generated queries to user prompts, and feedback given through the Azure Copilot
experience in the Azure Portal.

## What are the limitations of Azure Management MCP Server? How can users minimize impact?

**Limitations:**
- The system generates queries based on ARG capabilities; requests outside ARG scope cannot be fulfilled
- Query results depend on your Azure permissions—the system can only return data you have access to
- Natural language interpretation may occasionally produce unexpected query structures

**How to minimize impact:**
- Review generated queries before execution or ask the system to validate them first
- Ensure your Azure credentials have appropriate permissions for your intended queries
- Use the validation tool to catch errors before running queries
- Start with specific, well-defined requests rather than overly broad natural language prompts

## What operational factors and settings allow for effective and responsible use?

The system performs optimally when:
- You provide clear, specific requests in natural language
- Your Azure credentials have appropriate permissions for queried resources
- You review and validate generated queries before execution
- You use the system within your organization's AI and Azure governance policies
