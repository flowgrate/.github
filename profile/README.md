# Flowgrate

**Fluent database migrations for any language — without the framework baggage.**

Tired of being forced into EF Core just to manage schema changes? Don't want Django's ORM but still need migrations? Unhappy with how your framework handles versioning? Flowgrate is a standalone migration tool that works independently of any ORM or framework.

Write migrations in a clean fluent API in your language of choice. Flowgrate takes care of the rest.

```csharp
// C# — no EF Core required
Schema.Create("users", table => {
    table.Id();
    table.String("name");
    table.String("email", 100);
    table.Decimal("balance", 10, 2).Default(0);
    table.Timestamps();
});
```

```bash
flowgrate up
# applied: 20260402_163107_CreateUsersTable
```

## Why Flowgrate?

- **No ORM required** — works with any stack, any database library
- **Any language** — C#, Python, and more via a simple JSON contract
- **Familiar API** — fluent, Laravel-inspired, easy to read and write
- **Lightweight** — a single binary CLI, no JVM, no heavy runtime
- **Free alternative** to Flyway, Liquibase, EF Core Migrations, Django migrations

## How it works

Your SDK writes a JSON manifest to stdout → the Flowgrate CLI reads it and executes SQL.

```
Fluent API  →  JSON manifest  →  flowgrate CLI  →  SQL  →  Database
```

This design means any language can integrate with Flowgrate by implementing the [manifest spec](https://github.com/flowgrate/spec).

## Repositories

| Repo | Description |
|------|-------------|
| [core](https://github.com/flowgrate/core) | Go CLI + PostgreSQL adapter |
| [dotnet](https://github.com/flowgrate/dotnet) | C# SDK — fluent Blueprint API |
| [python](https://github.com/flowgrate/python) | Python SDK *(coming soon)* |
| [spec](https://github.com/flowgrate/spec) | JSON manifest spec — implement Flowgrate for any language |

## Quick start

```bash
# 1. Install CLI
curl -L https://github.com/flowgrate/core/releases/latest/download/flowgrate-linux-amd64 -o flowgrate
chmod +x flowgrate && sudo mv flowgrate /usr/local/bin/

# 2. Generate config
flowgrate init --db=postgres://user:pass@localhost/mydb

# 3. Create and run migrations
flowgrate make CreateUsersTable
flowgrate up
```

## Want to build an SDK for your language?

Read the [manifest spec](https://github.com/flowgrate/spec). If your tool can write JSON to stdout, it works with Flowgrate.
