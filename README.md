# adl-context-vault

A starter template for your personal context vault. Fork this repo and connect it to [adl-context-collector](https://github.com/ammons-datalabs/adl-context-collector) to give any MCP-compatible LLM persistent memory about your work, projects, and knowledge.

## Setup

### 1. Fork or clone this repo

```bash
git clone https://github.com/ammons-datalabs/adl-context-vault.git my-vault
cd my-vault
```

### 2. Configure your environment

```bash
cp .env.example .env
```

Edit `.env` with your database URL and OpenAI API key (or remove the OpenAI key if using Ollama — see the [context-collector docs](https://github.com/ammons-datalabs/adl-context-collector#local-setup-ollama)).

### 3. Create your database

```bash
createdb my_context
psql my_context < /path/to/adl-context-collector/sql/schema.sql
```

### 4. Customize your config

```bash
cp vault-config.example.json vault-config.json
```

Edit `vault-config.json` to customize:
- `serverName` — what shows up as the MCP tool prefix
- `categories` — fact categories relevant to your work
- Tool descriptions — help the LLM understand what your vault contains
- Key examples — guide the LLM on your naming conventions

Update `COLLECTOR_CONFIG` in `.env` to point to your config file.

### 5. Register with Claude Code

```bash
claude mcp add my-vault \
  -e DOTENV_CONFIG_PATH=/path/to/my-vault/.env \
  -- npx tsx /path/to/adl-context-collector/src/index.ts
```

Restart Claude. Your vault tools are now available.

## What goes in a vault

A vault is a directory where you keep:
- **`.env`** — database connection and API keys
- **`vault-config.json`** — tool descriptions and domain configuration
- **`rawdocs/`** — documents to ingest (markdown, PDF, plain text)
- Whatever else is useful for your context (notes, references, etc.)

The vault doesn't contain any code — it's purely configuration and data. The [context-collector](https://github.com/ammons-datalabs/adl-context-collector) engine runs separately.

## Multiple vaults

You can run multiple vaults (e.g., personal and work) pointing at different databases but sharing the same context-collector installation. Each vault has its own `.env`, config, and MCP server registration. See the [context-collector docs](https://github.com/ammons-datalabs/adl-context-collector#multiple-vaults) for details.

## Ingesting documents

Place files in `rawdocs/` and use the `ingest_document` MCP tool, or run the CLI:

```bash
env $(grep -v '^#' .env | xargs) npm run ingest --prefix /path/to/adl-context-collector -- rawdocs/
```

Supported formats: Markdown, PDF, plain text.
