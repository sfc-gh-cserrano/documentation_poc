---
icon: material/lightning-bolt
title: Streaming Ingestion
---

# :material-lightning-bolt: Streaming Ingestion

Low-latency row-level ingestion using the Snowpipe Streaming SDK.

See also: [Ingestion Overview](index.md) | [Snowpipe](snowpipe.md)

## When to Use Streaming vs Snowpipe

| Feature | Snowpipe | Snowpipe Streaming |
|---------|----------|-------------------|
| Latency | 1-5 min | < 10 seconds |
| Input | Files on stage | SDK API calls |
| Ordering | No guarantee | Per-channel ordering |
| Cost model | Per-file credits | Per-second compute |
| Best for | Batch file drops | Real-time event streams |

## Architecture

```mermaid
flowchart LR

    APP[Application / Kafka Connect] -->|insertRows()| CHANNEL[Streaming Channel]

    CHANNEL -->|flush| TABLE[Target Table]

    TABLE -->|stream| DT[Dynamic Table]
```

## SDK Usage (Java)

```java
SnowflakeStreamingIngestChannel channel = client.openChannel(
    OpenChannelRequest.builder("my_channel")
        .setDBName("raw")
        .setSchemaName("public")
        .setTableName("events")
        .build()
);

Map<String, Object> row = new HashMap<>();
row.put("event_id", UUID.randomUUID().toString());
row.put("event_type", "page_view");
row.put("timestamp", Instant.now().toString());

channel.insertRow(row, String.valueOf(offsetToken));
```

## Channel Management

```sql
-- View active channels
SHOW CHANNELS IN TABLE raw.public.events;

-- Check channel offset
SELECT SYSTEM$GET_CHANNEL_STATUS('raw.public.events', 'my_channel');
```
