# @akasha-os/connector-sdk

Build connectors for [Akasha](https://github.com/Akasha-os/akasha) — the self-hosted second brain.

A connector is a data source that feeds into Akasha's knowledge graph. This SDK gives you everything you need to build one and publish it as an npm package.

---

## Install

```bash
npm install @akasha-os/connector-sdk
```

---

## Quickstart

```typescript
import { WebhookConnector, NormalizedEvent } from '@akasha-os/connector-sdk';
import { z } from 'zod';

const ConfigSchema = z.object({
  apiKey: z.string(),
});

export class NotionConnector extends WebhookConnector {
  manifest = {
    id:          'notion',
    name:        'Notion',
    description: 'Ingest pages and databases from Notion',
    version:     '1.0.0',
    author:      'your-name',
    type:        'webhook' as const,
    triggers:    ['event.normalized.notion'],
    configSchema: ConfigSchema,
    requiresAuth: true,
    authType:    'apikey' as const,
  };

  normalize(raw: unknown, workspaceId: string): NormalizedEvent {
    // transform your source payload into a NormalizedEvent
    return { ... };
  }
}
```

---

## Connector types

| Type | Description |
|---|---|
| `WebhookConnector` | Platform exposes an HTTP endpoint, source pushes to it |
| `PollerConnector` | Connector fetches data on a schedule |
| `DeviceConnector` | Data pushed from a local device or app |
| `ImportConnector` | Bulk one-time or periodic import |
| `SyncConnector` | Bidirectional — import + export + live sync |

---

## Publishing

Name your package `@akasha-os/connector-[name]` and publish to npm:

```bash
npm publish --access public
```

Then open a PR to add it to the [community registry](https://github.com/Akasha-os/akasha/blob/main/connectors/community/README.md).

---

## Official connectors

Built and maintained by the Akasha team:

- Mail
- Slack
- Calendar
- Browser
- Terminal
- Watch
- Location
- Obsidian
- Notion

---

## Links

- [Akasha](https://github.com/Akasha-os/akasha)
- [Documentation](https://github.com/Akasha-os/docs)
- [Connector authoring guide](https://github.com/Akasha-os/docs)