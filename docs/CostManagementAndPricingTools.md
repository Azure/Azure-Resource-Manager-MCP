# Cost Management & Pricing tools

The Azure Resource Manager MCP server ships an optional **Cost Management & Pricing**
tool surface that lets agents answer cost, budget, savings, and pricing questions
in natural language, on behalf of the signed-in user.

These tools are **off by default** — enable them per client (see below).

## What you can ask

Once enabled, you can ask the agent things like:

- *"What did I spend on Azure this month, broken down by service?"*
- *"Forecast my subscription cost for the rest of the month."*
- *"How much would a Standard_E4s_v5 VM cost in East US?"*
- *"Show me my reserved instance utilization for the last 30 days."*

## Toolsets

The server groups tools into **toolsets**:

| Toolset          | What it includes                                                |
|------------------|-----------------------------------------------------------------|
| `CostManagement` | Cost & usage queries, budgets, alerts, savings, AKS cost split  |
| `Pricing`        | Public retail prices and negotiated pricesheet downloads        |

## Enabling the toolsets

Opt in per client by adding the `x-mcp-toolset` header on the MCP connection to
the Azure Resource Manager MCP server. The header value is a comma-separated list
of toolset names — enable one or both, e.g. `x-mcp-toolset: CostManagement,Pricing`.

### VS Code (GitHub Copilot Chat)

MCP servers are configured in one of two files:

- **Workspace**: `.vscode/mcp.json` in your repo (applies only to that workspace).
- **User**: open the Command Palette (<kbd>Ctrl+Shift+P</kbd> / <kbd>Cmd+Shift+P</kbd>),
  run **MCP: Open User Configuration**, and edit the `mcp.json` it opens.
  On Windows this lives at `%APPDATA%\Code\User\mcp.json`, on macOS at
  `~/Library/Application Support/Code/User/mcp.json`, on Linux at
  `~/.config/Code/User/mcp.json`.

Add (or update) the Azure Resource Manager MCP server entry with `headers`:

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

Save the file, then restart the server: open the Command Palette and run
**MCP: List Servers**, pick `azure-resource-manager-mcp`, and choose **Restart**.
The new tools will appear under **Configure Tools** in Chat.

![VS Code workflow: open MCP: List Servers, pick ARM MCP, choose Show Configuration, add the x-mcp-toolset header to mcp.json, and save](media/ARMMCP_CostPricing_Enable_Demo.gif)

### GitHub Copilot CLI

Edit `~/.copilot/mcp-config.json` and add (or update) the server entry with `headers`:

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

Restart the MCP server to pick up the change. In Copilot CLI today this means
exiting and relaunching `copilot`. Verify the server is running with
`copilot mcp list`.

## Cost Management tools

Toolset: `CostManagement`

The **Scopes** column shows which Azure scope types each tool accepts:

- **Subscription** — `/subscriptions/{id}` or
  `/subscriptions/{id}/resourceGroups/{name}`
- **Management group** — `/providers/Microsoft.Management/managementGroups/{id}`
- **Billing** — Enterprise Agreement (EA) or Microsoft Customer Agreement (MCA)
  billing scopes, rooted at
  `/providers/Microsoft.Billing/billingAccounts/{id}` (and their child scopes
  such as billing profiles or invoices).

For best performance when comparing costs across multiple subscriptions, make a
single query against a **billing** scope and filter by subscriptions rather than
calling each subscription individually.

### Query & forecast

| Tool | Scope | Input | Output | Purpose | Example AI Use Case |
|------|-------|-------|--------|---------|---------------------|
| `query_costs` | Subscription, Management group, Billing | Timeframe (or from/to), granularity, groupBy dimensions, optional filter, metric | Cost & usage rows (up to 100) | Query actual or amortized Azure cost and usage data | "What did I spend this month, broken down by service?" |
| `query_aks_costs` | Subscription only — no RG | Timeframe (or from/to), granularity, groupBy dimensions, optional filter, metric | AKS container-level cost rows (up to 100) | Break down AKS costs by cluster, namespace, idle vs service utilization, and service category | "Which AKS namespace cost the most last month?" |
| `forecast_costs` | Subscription, Management group, Billing | From, to, granularity, metric | Actual + forecasted cost rows through end of period (up to 100) | Forecast Azure cost for the current or a custom period | "What will my subscription cost by end of month?" |
| `list_dimensions` | Subscription, Management group, Billing | — | Supported cost dimensions for the scope | Discover dimensions available for grouping or filtering cost queries | "What dimensions can I group costs by?" |

### Budgets & alerts

| Tool | Scope | Input | Output | Purpose | Example AI Use Case |
|------|-------|-------|--------|---------|---------------------|
| `list_budgets` | Subscription, Management group, Billing | — | All budgets at the scope with current spend vs limit | List active Cost budgets | "Do I have any budgets close to their limit?" |
| `get_budget` | Subscription, Management group, Billing | Budget name | Budget detail with current spend, forecast, notification rules | Inspect a specific budget | "Show me the details of the `prod-monthly` budget." |
| `create_budget` *(write)* | Subscription | Amount, contact emails or notifications, optional name / time grain / start & end dates | Created budget object | Create a monthly / quarterly / annual Cost budget with threshold notifications | "Set a $5,000 monthly budget on subscription X and email me at 80%." |
| `list_alerts` | Subscription, Management group, Billing | — | Cost alerts and anomaly notifications | Surface threshold alerts and detected anomalies | "Are there any unusual cost spikes this month?" |

### Reservations & Savings Plans

| Tool | Scope | Input | Output | Purpose | Example AI Use Case |
|------|-------|-------|--------|---------|---------------------|
| `list_benefit_utilization` | Billing | — | Reservation and Savings Plan utilization metrics | Check how well reservations and savings plans are being used | "How well-utilized are my reservations?" |
| `get_benefit_recommendations` | Subscription, Billing | — | Recommended Reservation or Savings Plan purchases with projected savings | Identify opportunities to save with reservations or savings plans | "Which reservations would save me money based on my recent usage?" |
| `list_reservation_transactions` | Billing | `from` (required), optional `to` | Purchase, refund, and exchange transactions (up to 100) | Audit Reservation and Savings Plan transactions in a date range | "Show me all reservation purchases since January 1." |

## Pricing tools

Toolset: `Pricing`

| Tool | Scope | Input | Output | Purpose | Example AI Use Case |
|------|-------|-------|--------|---------|---------------------|
| `get_retail_prices` | Public — no scope, no auth | Optional service name, ARM SKU, region, meter name, price type, currency | Public retail price records (consumption, reservation, savings plan, dev/test) | Look up public Azure retail (pay-as-you-go) pricing | "How much is a Standard_D4s_v5 VM in East US?" |
| `start_pricesheet_download` | Billing | Agreement type (EA / MCA billing profile / MCA invoice), billing period (EA only) | Operation status URL to poll | Kick off an asynchronous download of your negotiated pricesheet | "Start downloading our enterprise pricesheet for April 2025." |
| `get_pricesheet_status` | n/a (operation URL) | Operation status URL from `start_pricesheet_download` | In-progress status (with retry-after) or a time-limited SAS download URL | Poll a pricesheet download until the SAS URL is ready | "Is the pricesheet I requested ready yet?" |

## Example: a pricing prompt end-to-end

Asking *"How much would an Av2 VM cost per month in East US?"* — the agent calls
`get_retail_prices` and returns a breakdown across OS and pricing tiers
(Regular vs Spot, Linux vs Windows):

![End-to-end demo: typing a pricing prompt in VS Code Chat, the agent invoking get_retail_prices on the ARM MCP server, and returning a pricing table for Standard_A2_v2 in East US](media/ARMMCP_Pricing_Prompt_Demo.gif)
