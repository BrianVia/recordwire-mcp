# Recordwire MCP server

U.S. business-registry data and change events for agents. Search companies, read their history,
and get told when they change: new formations, name changes, status changes (dissolved, revoked,
reinstated), address, registered-agent, and officer changes. Data comes from official state
sources: bulk files and open data where states publish them, and the state's own public business
search where they do not.

- **Server:** `https://api.recordwirehq.com/mcp` (Streamable HTTP)
- **Auth:** `Authorization: Bearer <key>`. Get a key at https://recordwirehq.com/app.
- **Docs:** https://recordwirehq.com/mcp and https://recordwirehq.com/docs
- **Same data over REST:** `https://api.recordwirehq.com/v1/...`

## Connect

Claude Code:

```sh
claude mcp add recordwire --transport http https://api.recordwirehq.com/mcp \
  --header "Authorization: Bearer $RECORDWIRE_API_KEY"
```

Cursor, Claude Desktop, or any client that takes a JSON config:

```json
{
  "mcpServers": {
    "recordwire": {
      "url": "https://api.recordwirehq.com/mcp",
      "headers": { "Authorization": "Bearer YOUR_KEY" }
    }
  }
}
```

`initialize` and `tools/list` work without a key, so you can see the tools before signing up.

## Tools

| Tool | What it does |
|---|---|
| `search_businesses` | Find companies by name prefix, state, entity type, status, or formation date range |
| `get_business` | One company's current record: name, type, status, dates, addresses, registered agent, officers where published |
| `get_business_events` | One company's change history, oldest to newest |
| `search_events` | Change events across a state or all states, by type and date (e.g. every new formation since Monday) |
| `list_sources` | Coverage: each state, its source, cadence, company count, and last file date |
| `create_subscription` | Get signed webhook POSTs when matching companies change |
| `list_subscriptions` | Your webhook subscriptions and their health |
| `delete_subscription` | Stop a subscription |

## Coverage

11 states: Florida, New York, Colorado, Pennsylvania, Virginia, Connecticut, and Oregon (official
bulk files and open data, full change events), plus Massachusetts, Idaho, Wyoming, and Missouri
(read from each state's public search, new formations). About 26 million companies. Live coverage
and freshness: https://recordwirehq.com/states

## Example prompts

- "List Florida LLCs formed this week whose names contain Holdings."
- "Has ACME LOGISTICS LLC in Virginia changed its registered agent or name since 2020?"
- "Which Colorado companies were dissolved in the last 30 days?"
- "Watch every new Massachusetts company with 'Merger Sub' in its name and tell me when it changes."

## Pricing

Flat monthly plans, no per-call metering: $100/month for one state, $200 for any three, $500 for
every covered state. See https://recordwirehq.com/#pricing.

## Contact

brian@recordwirehq.com
