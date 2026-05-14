# Cost Management & Pricing tools

The Azure Resource Manager MCP server ships an optional **Cost Management & Pricing**
tool surface that lets agents answer cost, budget, savings, and pricing questions
on behalf of the signed-in user — for example *"what did I spend this month?"*,
*"forecast the rest of the month"*, or *"how much would a Standard_D4s_v5 cost in West US 2?"*.

These tools are **off by default**. You opt in per client by sending the
`x-mcp-toolset` header on the MCP connection (see [Enabling the toolsets](#enabling-the-toolsets)
below).

## Toolsets

The server groups tools into **toolsets**. To use a tool you must enable its
toolset via the `x-mcp-toolset` header. The two toolsets covered by this doc:

| Toolset          | Header value     | What it includes                                                |
|------------------|------------------|-----------------------------------------------------------------|
| `CostManagement` | `CostManagement` | Cost & usage queries, budgets, alerts, savings, AKS cost split  |
| `Pricing`        | `Pricing`        | Public retail prices and negotiated pricesheet downloads        |

You can enable one or both. Header values are comma-separated, e.g.
`x-mcp-toolset: CostManagement,Pricing`.

Tools in the core ARM/ARG set (`generate_query`, `validate_query`, `execute_query`,
`create_template_deployment`, `get_arm_template_deployment_status`,
`cancel_arm_template_deployment`) are always on and do not require this header.

## Cost Management tools

Toolset: `CostManagement`

| Tool                            | Purpose                                                                                          |
|---------------------------------|--------------------------------------------------------------------------------------------------|
| `query_costs`                   | Query Azure cost and usage data.                          |
| `query_aks_costs`               | Query AKS container-level cost data.                      |
| `forecast_costs`                | Forecast Azure costs.                                     |
| `list_dimensions`               | List available cost dimensions for grouping or filtering. |
| `list_budgets`                  | List Cost budgets.                                        |
| `get_budget`                    | Get details for a single Cost budget.                     |
| `create_budget`                 | Create a Cost budget.                                     |
| `list_alerts`                   | List cost alerts and anomalies.                           |
| `list_benefit_utilization`      | Show Reservation and Savings Plan utilization.            |
| `get_benefit_recommendations`   | Get Reservation and Savings Plan purchase recommendations.|
| `list_reservation_transactions` | List Reservation and Savings Plan transactions.           |

## Pricing tools

Toolset: `Pricing`

| Tool                        | Purpose                                                                |
|-----------------------------|------------------------------------------------------------------------|
| `get_retail_prices`         | Look up public Azure retail prices for any service, SKU, and region.   |
| `start_pricesheet_download` | Start an asynchronous download of your negotiated pricesheet.          |
| `get_pricesheet_status`     | Poll the status of a pricesheet download and get the download URL.     |

## Enabling the toolsets

You enable a toolset by adding the `x-mcp-toolset` header to your client's MCP
configuration for the Azure Resource Manager MCP server.

### VS Code (GitHub Copilot Chat)

Add `headers` to the existing Azure Resource Manager MCP server entry in your
MCP configuration (`.vscode/mcp.json` or the user-level MCP config):

```jsonc
{
  "servers": {
    "azure-resource-manager-mcp": {
      "type": "http",
      "url": "https://mcp.management.azure.com",
      "headers": {
        "x-mcp-toolset": "CostManagement,Pricing"
      }
    }
  }
}
```

Restart VS Code (or reconnect the server) and the new tools will appear under
**Configure Tools** in Chat.

### GitHub Copilot CLI

Edit `~/.copilot/mcp-config.json` and add `headers` to the server entry:

```jsonc
{
  "mcpServers": {
    "azure-resource-manager-mcp": {
      "type": "http",
      "url": "https://mcp.management.azure.com",
      "headers": {
        "x-mcp-toolset": "CostManagement,Pricing"
      }
    }
  }
}
```

Restart `copilot` to pick up the change.

## Example prompts

Once enabled, you can ask the agent things like:

- *"What did I spend on Azure this month, broken down by service?"*
- *"Forecast my subscription cost for the rest of the month."*
- *"Which resource groups drove the spike on May 8?"*
- *"How much would a Standard_E4s_v5 VM cost in East US?"*
- *"Show me my reserved instance utilization for the last 30 days."*
- *"Create a $500 monthly budget on this subscription and alert me at 80%."*
