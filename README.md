# ARM MCP Server

The **ARM MCP Server** is a powerful Model Context Protocol (MCP) server that enables AI-driven applications to interact with Azure Resource Manager through natural language queries. This server provides intelligent query management, validation, and execution capabilities for Azure Resource Graph (ARG) queries.

## Project Overview

This repository tracks features, bugs, and suggestions for the ARM (Azure Resource Manager) MCP Server. The ARM MCP Server integrates with Visual Studio Code to provide seamless access to Azure resources through natural language interactions.

### Getting Access

To use the ARM MCP Server, you will need to submit your **tenant ID** to our enrollment form (link TBD). Once your tenant is approved, we will send you the installation link to get started.

---

# ARM MCP Server – Internal Onboarding Guide

This guide walks you through prerequisites, installation, configuration, and first‑use steps for onboarding to the ARM MCP Server inside Visual Studio Code (VS Code).

---

## Prerequisites
Before starting, ensure **Visual Studio Code (VS Code)** is installed.  

The onboarding link opens into VS Code and requires it to already be present.  

---

## Installation & Setup

### 1. Join the ARM MCP Program
1. Open: **https://aka.ms/JoinARMMCP**  
VS Code will launch automatically. 

2. When prompted inside VS Code, click **Install** under **ARM MCP Server** to add it to your MCP server configuration.  

---

## Configure Tools in VS Code

### 2. Open the Chat Interface
1. In VS Code, go to **View > Chat**, or click the chat icon to the right of the center toolbar header.



### 3. Configure MCP Tools
1. In the Chat window, click the **Configure Tools** icon.  
2. Ensure **ARM MCP Server** is checked. You can click the dropdown icon to see three tools under it:  
   - **execute_query**   
   - **generate_query**  
   - **validate_query**  
3. Click **Update Tools** and sign in with your **work profile** if prompted.  

---

## First Use

### 4. Use Chat in Agent Mode
Switch Chat into **Agent mode**, then ask a question involving **ARG** (Azure Resource Graph).  

Example: *"Show me all VMs in my subscription using ARG."*  

Example: *"How many virtual machines are in my sub 'mySub'?"*  

You are now onboarded and ready to experiment with ARG‑backed natural language queries using the ARM MCP Server inside VS Code. To submit feedback, please follow the instructions on the [feedback page](TODO link).

---


# ARM MCP Server Feature Set

The **ARM MCP Server** provides a suite of tools designed to facilitate advanced query management
and validation for AI-driven applications. The following tools are available under the ARM MCP
Server:

## 1. execute_query

**Description:**  
Executes a given query against the ARM MCP database and returns the results.

**Example Use Cases:**  
- Retrieving specific data records based on user input.
- Running scheduled reports or analytics queries.
- Fetching real-time metrics for dashboards.

**AI Usage Scenario:**  
An AI assistant receives a user request for the latest system logs. It uses `generate_query` to
create the appropriate query, then calls `execute_query` to retrieve and present the results.

---

## 2. generate_query

**Description:**  
Automatically generates a valid query based on a natural language prompt or structured requirements.

**Example Use Cases:**  
- Translating user questions into database queries.
- Assisting users who are unfamiliar with query syntax.
- Automating report generation based on high-level instructions.

**AI Usage Scenario:**  
A user asks, "Show me all failed login attempts in the past 24 hours." The AI uses `generate_query` to convert this request into a valid query for execution.

---

## 3. validate_query

**Description:**  
Checks the syntax and logic of a query before execution to ensure correctness and prevent errors.

**Example Use Cases:**  
- Preventing malformed queries from reaching the database.
- Providing feedback to users on query issues.
- Ensuring compliance with security and data access policies.

**AI Usage Scenario:**  
Before executing a user-generated query, the AI uses `validate_query` to confirm the query is safe and correct, reducing the risk of runtime errors or security breaches.

---

## Summary Table

| Tool             | Purpose                                   | Example AI Use Case                                      |
|------------------|-------------------------------------------|----------------------------------------------------------|
| execute_query    | Runs queries and returns results           | Fetching user-requested data                             |
| generate_query   | Creates queries from natural language      | Translating user questions into queries                  |
| validate_query   | Checks queries for correctness and safety  | Ensuring queries are valid before execution              |

The ARM MCP Server tools enable seamless, safe, and intelligent query management for AI-powered solutions.
