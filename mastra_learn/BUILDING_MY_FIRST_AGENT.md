# Building My First Finance Agent using TypeScript 

## Financial Assistant Agent

A financial assistant agent that helps users analyze their transaction data. The agent can fetch transaction data from Google Sheets, answer questions about spending patterns, and maintain context across conversations through memory.

## Agent Configuration

```typescript
export const financialAgent = new Agent({
  name: "Financial Assistant Agent",
  instructions: `ROLE DEFINITION
- You are a financial assistant that helps users analyze their transaction data.
- Your key responsibility is to provide insights about financial transactions.

CORE CAPABILITIES
- Analyze transaction data to identify spending patterns.
- Answer questions about specific transactions or vendors.
- Provide basic summaries of spending by category or time period.

BEHAVIORAL GUIDELINES
- Maintain a professional and friendly communication style.
- Keep responses concise but informative.
- Format currency values appropriately.

CONSTRAINTS & BOUNDARIES
- Do not provide financial investment advice.
- Never make assumptions about the user's financial situation beyond what's in the data.

TOOLS
- Use the getTransactions tool to fetch financial transaction data.
- Analyze the transaction data to answer user questions about their spending.`,
  model: openai("gpt-4o"),
  tools: { getTransactionsTool },
  memory: new Memory({
    storage: new LibSQLStore({
      url: "file:../../memory.db",
    }),
  }),
});
```

## Custom Tool

Tool for fetching transaction data from a public Google Sheet:

```typescript
export const getTransactionsTool = createTool({
  id: "get-transactions",
  description: "Get transaction data from Google Sheets",
  inputSchema: z.object({}),
  outputSchema: z.object({
    csvData: z.string(),
  }),
  execute: async () => {
    const url = "<google-sheet-public-csv-url>";
    const response = await fetch(url);
    const data = await response.text();
    return { csvData: data };
  },
});
```

## Memory Configuration

Persistent memory using LibSQLStore for maintaining conversation context:

```typescript
memory: new Memory({
  storage: new LibSQLStore({
    url: "file:../../memory.db", // Persistent file storage
  }),
}),
```

<img width="673" height="729" alt="image" src="https://github.com/user-attachments/assets/507e78c7-e836-4644-b1ef-21b5034934f3" />

<img width="625" height="54" alt="image" src="https://github.com/user-attachments/assets/80ba66d5-b1be-427c-84b4-7b52037d1486" />



