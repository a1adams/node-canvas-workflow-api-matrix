# Node-based AI workflow API matrix: runs, webhooks, idempotency and MCP across 8 canvases

A maintained dataset of **node-based ai workflow api** options: what each one connects to, where it stops, how to run it, and a link to the vendor's own pricing page rather than a price that will be wrong by the time you read it.

The tables below are generated from [`data/tools.json`](data/tools.json). Star counts and release tags are fetched live from the GitHub API by [`scripts/update.js`](scripts/update.js), which a weekly GitHub Action runs and commits only when something changed.

<!-- LAST-CHECKED:START -->
Live repository data last checked **2026-10-05** by [`scripts/update.js`](scripts/update.js), which runs weekly via GitHub Actions.
<!-- LAST-CHECKED:END -->

Maintained by [a1adams](https://github.com/a1adams). Corrections welcome — see [CONTRIBUTING.md](CONTRIBUTING.md).

## Contents

- [The data](#the-data)
- [Capability scores](#capability-scores)
- [The tools](#the-tools)
  - [Wireflow](#1-wireflow)
  - [Figma Weave](#2-figma-weave)
  - [Flora](#3-flora)
  - [Krea Nodes](#4-krea-nodes)
  - [Comfy Cloud](#5-comfy-cloud)
  - [ComfyUI (self-hosted)](#6-comfyui-self-hosted)
  - [Freepik Spaces](#7-freepik-spaces)
  - [n8n](#8-n8n)
- [Decision this list supports](#decision-this-list-supports)
- [Scope and evidence](#scope-and-evidence)
- [What each column means](#what-each-column-means)
- [Evidence by cell](#evidence-by-cell)
- [Selection notes](#selection-notes)
- [Acceptance recipe](#acceptance-recipe)
- [Evaluation record](#evaluation-record)
- [How this list is maintained](#how-this-list-is-maintained)
- [Contributing](#contributing)
- [License](#license)

## The data

One row per tool, one column per thing people actually check before committing. Columns with nothing verified behind them are dropped rather than filled with guesses.

<!-- DATA-TABLE:START -->
| Tool | Claude connection | REST API | Free tier | Model support | Pricing | Open-source SDK / MCP |
|---|---|---|---|---|---|---|
| **[Wireflow](#1-wireflow)** | Hosted MCP, Streamable HTTP, OAuth 2.1 | Yes | [check](https://www.wireflow.ai/pricing) | Image, video and audio model nodes | [pricing](https://www.wireflow.ai/pricing) | — |
| **[Figma Weave](#2-figma-weave)** | Weave tools through the Figma MCP server | — | [check](https://weave.figma.com/pricing) | Image and video model nodes | [pricing](https://weave.figma.com/pricing) | — |
| **[Flora](#3-flora)** | Hosted MCP, Streamable HTTP, OAuth 2.1 | Yes | [check](https://flora.ai/pricing) | Image, video, audio and text generations | [pricing](https://flora.ai/pricing) | — |
| **[Krea Nodes](#4-krea-nodes)** | Hosted MCP, Streamable HTTP, OAuth or API token | Yes | — | Image, video, audio and 3D model endpoints | — | — |
| **[Comfy Cloud](#5-comfy-cloud)** | Hosted MCP (public beta), OAuth or API key | Yes | [check](https://comfy.org/pricing) | ComfyUI nodes plus partner models | [pricing](https://comfy.org/pricing) | — |
| **[ComfyUI (self-hosted)](#6-comfyui-self-hosted)** | comfy-mcp, local stdio server | Yes | — | Models and custom nodes you install | — | [Comfy-Org/ComfyUI](https://github.com/Comfy-Org/ComfyUI) — 136,155 ★, v0.38.0 |
| **[Freepik Spaces](#7-freepik-spaces)** | Magnific MCP, Streamable HTTP, OAuth | — | [check](https://docs.magnific.com/pricing) | Image, video and audio model endpoints | [pricing](https://docs.magnific.com/pricing) | — |
| **[n8n](#8-n8n)** | Instance-level MCP server and MCP Server Trigger node | Yes | [check](https://n8n.io/pricing/) | Workflow automation with AI nodes | [pricing](https://n8n.io/pricing/) | [n8n-io/n8n](https://github.com/n8n-io/n8n) — 206,707 ★, n8n@2.41.7 |
<!-- DATA-TABLE:END -->

## Capability scores

The score counts how many of the checks in [`data/tools.json`](data/tools.json) → `capabilityChecks` a tool passes. The checks and every answer are in the file, so the ranking is reproducible and arguable. Disagree with a cell? Open an issue naming the tool, the check and the evidence.

<!-- CAPABILITY-SCORES:START -->
| Tool | Run workflow via API | Async job + polling | Webhook trigger URL | Completion webhook | Idempotency key | Cost in run response | MCP server | Scoped permissions | Self-host | Score |
|------|---|---|---|---|---|---|---|---|---|-------|
| **[Wireflow](#1-wireflow)** | ✅ | ✅ | ✅ | — | ✅ | ✅ | ✅ | ✅ | — | **7/9** |
| **[Flora](#3-flora)** | ✅ | ✅ | — | ✅ | ✅ | ✅ | ✅ | ✅ | — | **7/9** |
| **[ComfyUI (self-hosted)](#6-comfyui-self-hosted)** | ✅ | ✅ | — | ❌ | ✅ | — | ✅ | — | ✅ | **5/9** |
| **[n8n](#8-n8n)** | ✅ | — | ✅ | — | — | — | ✅ | ✅ | ✅ | **5/9** |
| **[Comfy Cloud](#5-comfy-cloud)** | ✅ | ✅ | — | ❌ | ✅ | — | ✅ | — | — | **4/9** |
| **[Krea Nodes](#4-krea-nodes)** | ✅ | ✅ | — | — | — | — | ✅ | — | — | **3/9** |
| **[Figma Weave](#2-figma-weave)** | — | — | — | — | — | — | ✅ | — | — | **1/9** |
| **[Freepik Spaces](#7-freepik-spaces)** | — | — | — | — | — | — | ✅ | — | — | **1/9** |
<!-- CAPABILITY-SCORES:END -->

## The tools

### 1. Wireflow

- **What it is:** A hosted node canvas for image, video and audio models. A saved workflow runs by ID through the REST API, and a hosted MCP connector exposes the same workflows to agents. See the [Wireflow workflow API](https://www.wireflow.ai/ai-workflow-api) overview.
- **Limits:** The webhook is an inbound trigger URL and results come back by polling; a completion callback is not documented. The Idempotency-Key header is documented on the execute route. The API overview says there is no official SDK yet, and self-hosting is not documented.
- **Note:** Documentation review 2026-09-28; product and account behaviour were not tested.
- **Links:**
  - [Homepage](https://www.wireflow.ai/ai-node-editor-with-api)
  - [Docs](https://www.wireflow.ai/docs/api)
  - [Pricing](https://www.wireflow.ai/pricing)
  - [Wireflow workflow API](https://www.wireflow.ai/ai-workflow-api)
  - [Official source 1](https://www.wireflow.ai/docs/api/run)
  - [Official source 2](https://www.wireflow.ai/docs/api/executions)
  - [Official source 3](https://www.wireflow.ai/docs/api/webhooks)
  - [Official source 4](https://www.wireflow.ai/docs/api/authentication)
  - [Official source 5](https://www.wireflow.ai/docs/mcp)

Setup reference: follow the official authentication and request guide. This is a documentation URL, not an executed API example.
```text
https://www.wireflow.ai/docs/api
```

### 2. Figma Weave

- **What it is:** Figma's node-based canvas for AI image and video workflows. Published Weave workflows, called Weave tools, can be listed and run from an agent through the Figma MCP server.
- **Limits:** The pricing page lists "Run workflows through API" as coming soon on the Enterprise plan, so there is no public REST API to call today. Running a Weave tool through MCP needs a paid standalone Weave account, spends Weave credits and asks the agent to confirm the credit cost first.
- **Note:** Documentation review 2026-09-28; product and account behaviour were not tested.
- **Links:**
  - [Homepage](https://weave.figma.com)
  - [Docs](https://developers.figma.com/docs/figma-mcp-server/tools-and-prompts/)
  - [Pricing](https://weave.figma.com/pricing)

Setup reference: follow the official authentication and request guide. This is a documentation URL, not an executed API example.
```text
https://developers.figma.com/docs/figma-mcp-server/tools-and-prompts/
```

### 3. Flora

- **What it is:** A node canvas whose saved workflows are called Techniques. The REST API runs a Technique by slug and returns a run to poll, and FLORA MCP exposes the same API surface to agents.
- **Limits:** The API runs Techniques but does not create or edit them. Output URLs are long-lived but not permanent, so download what you need to keep. Self-hosting is not documented.
- **Note:** Documentation review 2026-09-28; product and account behaviour were not tested.
- **Links:**
  - [Homepage](https://flora.ai)
  - [Docs](https://developer.flora.ai/api/)
  - [Pricing](https://flora.ai/pricing)
  - [Official source 2](https://developer.flora.ai/platform/webhooks/)
  - [Official source 3](https://developer.flora.ai/platform/idempotency/)
  - [Official source 4](https://developer.flora.ai/platform/authentication/)
  - [Official source 5](https://developer.flora.ai/mcp/)

Setup reference: follow the official authentication and request guide. This is a documentation URL, not an executed API example.
```text
https://developer.flora.ai/api/
```

### 4. Krea Nodes

- **What it is:** Krea's node workflow canvas. A node app built in Nodes runs by version ID through the Krea API and returns a job that you track by ID.
- **Limits:** The node-app execute reference lists no webhook header, idempotency key or cost field; webhooks are documented for generation requests. API calls draw on a separate USD API balance, and only workspace owners and admins can create API tokens.
- **Note:** Documentation review 2026-09-28; product and account behaviour were not tested.
- **Links:**
  - [Homepage](https://www.krea.ai/nodes)
  - [Docs](https://www.krea.ai/docs/developers/introduction)
  - [Official source 1](https://www.krea.ai/docs/api-reference/node-apps/execute-a-node-app)
  - [Official source 2](https://www.krea.ai/docs/developers/job-lifecycle)
  - [Official source 3](https://www.krea.ai/docs/developers/webhooks)
  - [Official source 4](https://www.krea.ai/docs/developers/mcp)
  - [Official source 5](https://www.krea.ai/docs/developers/api-keys-and-billing)

Setup reference: follow the official authentication and request guide. This is a documentation URL, not an executed API example.
```text
https://www.krea.ai/docs/developers/introduction
```

### 5. Comfy Cloud

- **What it is:** Comfy's hosted ComfyUI service. Comfy API v2, in beta, runs an API-format workflow graph as a durable job that you poll by ID, and the older v1 Cloud API accepts the same graph at /api/prompt.
- **Limits:** The API takes the exported graph in the request body; the v2 design notes say saved workflows are not in the first version, although the Cloud MCP server can run a saved workflow by name. The v2 spec rejects webhook_url today. API access needs a paid Cloud subscription, and spend is reported from invoices by a usage endpoint rather than in the job response.
- **Note:** Documentation review 2026-09-28; product and account behaviour were not tested. Comfy API v2 is in beta.
- **Links:**
  - [Homepage](https://comfy.org/cloud)
  - [Docs](https://docs.comfy.org/api-reference/v2/overview)
  - [Pricing](https://comfy.org/pricing)
  - [Official source 2](https://docs.comfy.org/development/api-development/sdks-design)
  - [Official source 3](https://docs.comfy.org/openapi-v2.yaml)
  - [Official source 4](https://docs.comfy.org/development/cloud/overview)
  - [Official source 5](https://docs.comfy.org/agent-tools/mcp)

Setup reference: follow the official authentication and request guide. This is a documentation URL, not an executed API example.
```text
https://docs.comfy.org/api-reference/v2/overview
```

### 6. ComfyUI (self-hosted)

- **What it is:** The open-source ComfyUI server on your own hardware. POST /prompt queues an API-format graph and returns a prompt_id, and /history plus the /ws WebSocket report results.
- **Limits:** The native server routes document no idempotency, scopes or webhooks. The Comfy API v2 contract, with its Idempotency-Key, reaches a self-hosted server only through the beta comfy-api-proxy. Models, custom nodes and GPUs are yours to install and maintain.
- **Note:** Documentation review 2026-09-28; product and account behaviour were not tested.
- **Links:**
  - [Homepage](https://github.com/Comfy-Org/ComfyUI)
  - [Docs](https://docs.comfy.org/development/comfyui-server/comms_routes)
  - [Official source 2](https://docs.comfy.org/api-reference/v2/overview)
  - [Official source 3](https://docs.comfy.org/agent-tools/mcp)

Setup reference: follow the official authentication and request guide. This is a documentation URL, not an executed API example.
```text
https://docs.comfy.org/development/comfyui-server/comms_routes
```

### 7. Freepik Spaces

- **What it is:** Freepik's node canvas, now sold under the Magnific name. The Magnific REST API covers individual model endpoints, and Magnific MCP can list and inspect Spaces.
- **Limits:** Running a saved Space by API is not documented, and the MCP tool list has no tool that runs a Space, only spaces_list and spaces_view. The REST API authenticates with private server-side API keys only.
- **Note:** Documentation review 2026-09-28; product and account behaviour were not tested.
- **Links:**
  - [Homepage](https://www.magnific.com/spaces)
  - [Docs](https://docs.magnific.com/introduction)
  - [Pricing](https://docs.magnific.com/pricing)
  - [Official source 2](https://docs.magnific.com/modelcontextprotocol)
  - [Official source 3](https://docs.magnific.com/webhooks)
  - [Official source 4](https://docs.magnific.com/authentication)

Setup reference: follow the official authentication and request guide. This is a documentation URL, not an executed API example.
```text
https://docs.magnific.com/introduction
```

### 8. n8n

- **What it is:** A workflow automation platform with AI nodes, available as a cloud service or self-hosted. A published workflow gets its own HTTP endpoint through a Webhook trigger node, and the instance-level MCP server can run workflows that are enabled for MCP.
- **Limits:** The public REST API manages workflows and executions but has no endpoint that starts a run. With the Immediately response mode, the Webhook node answers "Workflow got started" rather than a job ID to poll. API key scopes are an Enterprise plan feature, and the API is not available during the free trial.
- **Note:** Documentation review 2026-09-28; product and account behaviour were not tested.
- **Links:**
  - [Homepage](https://n8n.io)
  - [Docs](https://docs.n8n.io/connect/n8n-api)
  - [Pricing](https://n8n.io/pricing/)
  - [n8n-io/n8n](https://github.com/n8n-io/n8n)
  - [Official source 2](https://docs.n8n.io/connect/n8n-api/authentication)
  - [Official source 3](https://docs.n8n.io/integrations/builtin/core-nodes/n8n-nodes-base.webhook)
  - [Official source 4](https://docs.n8n.io/connect/connect-to-n8n-mcp-server)
  - [Official source 5](https://docs.n8n.io/deploy/host-n8n)

Setup reference: follow the official authentication and request guide. This is a documentation URL, not an executed API example.
```text
https://docs.n8n.io/connect/n8n-api
```

## Decision this list supports

You built a workflow on a node canvas and now want to call it from code. This matrix shows, per canvas, whether a documented API can start the run, how you get the result back, how retries and permissions work, and whether an MCP server or a self-hosted runtime exists.

## Scope and evidence

Documentation reviewed on 2026-09-28. This is a Wireflow-maintained resource dataset. Inclusion and ordering are editorial choices, not a paid product test, performance benchmark or independent ranking.

Every cell comes from the vendor's own documentation, and the Evidence by cell section links the page for each one. A check means the vendor documents the capability. A cross means the vendor's docs say it is not available today. A dash means not published: the docs reviewed do not document it, which is not proof that it is absent.

The weekly repository job refreshes GitHub metadata. It does not re-check vendor features, pricing or plan limits. Follow the official links for current terms.

## What each column means

- **Run workflow via API:** an HTTP endpoint starts a run of a workflow built on the canvas, either by saved ID or by posting the exported graph. The evidence line says which.
- **Async job + polling:** the run returns a job or execution ID that you can poll for status and outputs.
- **Webhook trigger URL:** a workflow gets its own URL that starts a run when called.
- **Completion webhook:** the platform calls your URL when a run finishes.
- **Idempotency key:** a documented key that stops a retried request from starting a duplicate run.
- **Cost in run response:** the run or execution record reports what the run cost.
- **MCP server:** a documented Model Context Protocol server that agents can use to reach the workflows.
- **Scoped permissions:** API keys or OAuth grants can be limited to specific actions or workspaces.
- **Self-host:** the vendor documents running the runtime on your own infrastructure.

## Evidence by cell

**Wireflow**

- Run workflow via API: yes. POST /api/v1/workflows/{id}/run runs the saved workflow with only the input values you override and returns 202 with an executionId. [Run Workflows](https://www.wireflow.ai/docs/api/run)
- Async job + polling: yes. GET /api/v1/workflows/executions/{executionId}/poll until the status is COMPLETED or FAILED. [Executions](https://www.wireflow.ai/docs/api/executions)
- Webhook trigger URL: yes. POST /api/v1/workflow/{webhookId}/trigger starts a run without an API key and returns an executionId; polling that execution needs a key. [Webhooks](https://www.wireflow.ai/docs/api/webhooks)
- Completion webhook: not published. The Webhooks page documents polling for results and no callback URL. [Webhooks](https://www.wireflow.ai/docs/api/webhooks)
- Idempotency key: yes. An Idempotency-Key header on the execute route returns the original response for the same key within 24 hours. [Executions](https://www.wireflow.ai/docs/api/executions)
- Cost in run response: yes. The execution record includes creditsUsed, and a 402 response lists required credits per node before a run starts. [Executions](https://www.wireflow.ai/docs/api/executions)
- MCP server: yes. Streamable HTTP endpoint with OAuth 2.1, PKCE and dynamic client registration. [Claude Connector (MCP)](https://www.wireflow.ai/docs/mcp)
- Scoped permissions: yes. API keys take scopes such as workflows:read, workflows:execute and executions:read, and MCP clients get read and run scopes by default with write scopes opt-in. [Authentication](https://www.wireflow.ai/docs/api/authentication) and [Claude Connector (MCP)](https://www.wireflow.ai/docs/mcp)
- Self-host: not published. [API Reference](https://www.wireflow.ai/docs/api)

**Figma Weave**

- Run workflow via API: coming soon. The Enterprise plan lists "Run workflows through API" as coming soon. [Pricing](https://weave.figma.com/pricing)
- Async job + polling: not published for a REST API. Through MCP, weave_run_tool returns run IDs that you poll with weave_get_tool_run_output. [Figma MCP tools](https://developers.figma.com/docs/figma-mcp-server/tools-and-prompts/)
- Webhook trigger URL: not published. [Pricing](https://weave.figma.com/pricing)
- Completion webhook: not published. [Figma MCP tools](https://developers.figma.com/docs/figma-mcp-server/tools-and-prompts/)
- Idempotency key: not published. [Figma MCP tools](https://developers.figma.com/docs/figma-mcp-server/tools-and-prompts/)
- Cost in run response: not published for a REST API. Through MCP, weave_run_tool returns the credit cost and waits for confirmation before it runs. [Figma MCP tools](https://developers.figma.com/docs/figma-mcp-server/tools-and-prompts/)
- MCP server: yes. The Figma MCP server lists, inspects and runs published Weave tools and needs a paid standalone Weave account. [Figma MCP tools](https://developers.figma.com/docs/figma-mcp-server/tools-and-prompts/)
- Scoped permissions: not published. [Figma MCP tools](https://developers.figma.com/docs/figma-mcp-server/tools-and-prompts/)
- Self-host: not published. [Pricing](https://weave.figma.com/pricing)

**Flora**

- Run workflow via API: yes. POST /techniques/{slug}/runs runs a saved Technique. [Getting Started](https://developer.flora.ai/api/)
- Async job + polling: yes. The run returns a run_id and poll_url; poll every 2 to 5 seconds until completed or failed. [Getting Started](https://developer.flora.ai/api/)
- Webhook trigger URL: not published. [Webhooks](https://developer.flora.ai/platform/webhooks/)
- Completion webhook: yes. Pass callback_url on a run and FLORA posts an HMAC-SHA256 signed payload when the run reaches a terminal state. [Webhooks](https://developer.flora.ai/platform/webhooks/)
- Idempotency key: yes. idempotency_key is stored for 24 hours; the same key and body return the original response. [Idempotency](https://developer.flora.ai/platform/idempotency/)
- Cost in run response: yes. A completed run reports charged_cost, and Technique details list run_cost in USD before you run. [Getting Started](https://developer.flora.ai/api/)
- MCP server: yes. Streamable HTTP at agents.flora.ai with OAuth 2.1 and PKCE. [FLORA MCP](https://developer.flora.ai/mcp/)
- Scoped permissions: yes. Each API key gets read, write and billing permissions per workspace. [Authentication](https://developer.flora.ai/platform/authentication/)
- Self-host: not published. [Getting Started](https://developer.flora.ai/api/)

**Krea Nodes**

- Run workflow via API: yes. POST /node-apps/{id}/execute runs a node app version with inputs that match its schema. [Execute a node app](https://www.krea.ai/docs/api-reference/node-apps/execute-a-node-app)
- Async job + polling: yes. The execute call returns a job; track it with GET /jobs/{id}. [Job Lifecycle](https://www.krea.ai/docs/developers/job-lifecycle)
- Webhook trigger URL: not published. [Execute a node app](https://www.krea.ai/docs/api-reference/node-apps/execute-a-node-app)
- Completion webhook: not published for node apps. The X-Webhook-URL header is documented for generation requests, and the node-app execute reference does not list it. [Webhooks](https://www.krea.ai/docs/developers/webhooks)
- Idempotency key: not published. [Execute a node app](https://www.krea.ai/docs/api-reference/node-apps/execute-a-node-app)
- Cost in run response: not published. A separate workspace usage endpoint reports compute units per completed job. [List workspace usage](https://www.krea.ai/docs/api-reference/usage/list-workspace-usage)
- MCP server: yes. Streamable HTTP at api.krea.ai/mcp with an execute_node_app tool, using OAuth or an API token. [MCP server](https://www.krea.ai/docs/developers/mcp)
- Scoped permissions: not published. Only workspace owners and admins can create API tokens, and the docs list no token scopes. [API keys and billing](https://www.krea.ai/docs/developers/api-keys-and-billing)
- Self-host: not published. [Krea API introduction](https://www.krea.ai/docs/developers/introduction)

**Comfy Cloud**

- Run workflow via API: yes, by graph. POST /api/v2/jobs submits an API-format workflow graph; the UI-format export is rejected. [openapi-v2.yaml](https://docs.comfy.org/openapi-v2.yaml)
- Async job + polling: yes. GET /api/v2/jobs/{id} is the authoritative status and output view. [Design notes](https://docs.comfy.org/development/api-development/sdks-design)
- Webhook trigger URL: not published. [Comfy API v2 overview](https://docs.comfy.org/api-reference/v2/overview)
- Completion webhook: no. The v2 spec reserves webhook_url for later and rejects it if present today. [openapi-v2.yaml](https://docs.comfy.org/openapi-v2.yaml)
- Idempotency key: yes. Idempotency-Key is single use and expires after 24 hours; a reused key is rejected with 422 rather than replayed. [openapi-v2.yaml](https://docs.comfy.org/openapi-v2.yaml)
- Cost in run response: not published. Spend is reported by a usage endpoint drawn from invoices. [v1 Cloud API overview](https://docs.comfy.org/development/cloud/overview)
- MCP server: yes. Hosted at cloud.comfy.org/mcp in public beta, with OAuth or an API key, including a run_saved_workflow tool. [Comfy MCP](https://docs.comfy.org/agent-tools/mcp)
- Scoped permissions: not published. [v1 Cloud API overview](https://docs.comfy.org/development/cloud/overview)
- Self-host: not published for the Cloud service. The same v2 API runs on self-hosted ComfyUI through comfy-api-proxy. [Comfy API v2 overview](https://docs.comfy.org/api-reference/v2/overview)

**ComfyUI (self-hosted)**

- Run workflow via API: yes, by graph. POST /prompt validates an API-format graph and queues it. [Server routes](https://docs.comfy.org/development/comfyui-server/comms_routes)
- Async job + polling: yes. POST /prompt returns a prompt_id; read results from /history/{prompt_id} or progress from /ws. [Server routes](https://docs.comfy.org/development/comfyui-server/comms_routes)
- Webhook trigger URL: not published. [Server routes](https://docs.comfy.org/development/comfyui-server/comms_routes)
- Completion webhook: no. The native routes use the /ws WebSocket, and the v2 contract served by comfy-api-proxy rejects webhook_url today. [openapi-v2.yaml](https://docs.comfy.org/openapi-v2.yaml)
- Idempotency key: yes, through comfy-api-proxy (beta), which serves the v2 contract in front of a local server. [Comfy API v2 overview](https://docs.comfy.org/api-reference/v2/overview)
- Cost in run response: not published. Runs use your own hardware; partner nodes spend credits. [Comfy MCP](https://docs.comfy.org/agent-tools/mcp)
- MCP server: yes. comfy-mcp is Comfy's first-party local server over stdio. [Comfy MCP](https://docs.comfy.org/agent-tools/mcp)
- Scoped permissions: not published. comfy-api-proxy has authentication off by default with an optional static bearer token. [Comfy API v2 overview](https://docs.comfy.org/api-reference/v2/overview)
- Self-host: yes. [ComfyUI on GitHub](https://github.com/Comfy-Org/ComfyUI)

**Freepik Spaces**

- Run workflow via API: not published. The REST API documents individual model endpoints, not Spaces. [Introduction](https://docs.magnific.com/introduction)
- Async job + polling: not published for Spaces. Model endpoints such as Mystic return a task_id to poll. [Mystic reference](https://docs.magnific.com/api-reference/mystic/post-mystic)
- Webhook trigger URL: not published. [Introduction](https://docs.magnific.com/introduction)
- Completion webhook: not published for Spaces. Model endpoints such as Mystic accept a webhook_url. [Mystic reference](https://docs.magnific.com/api-reference/mystic/post-mystic)
- Idempotency key: not published. [Introduction](https://docs.magnific.com/introduction)
- Cost in run response: not published. [Introduction](https://docs.magnific.com/introduction)
- MCP server: yes. Magnific MCP at mcp.magnific.com, Streamable HTTP with OAuth; spaces_list and spaces_view inspect Spaces. [Magnific MCP](https://docs.magnific.com/modelcontextprotocol)
- Scoped permissions: not published. Private API keys are the only REST authentication method. [Authentication](https://docs.magnific.com/authentication)
- Self-host: not published. [Introduction](https://docs.magnific.com/introduction)

**n8n**

- Run workflow via API: yes, through a Webhook trigger node, which registers a production URL when the workflow is published. The public REST API has no run endpoint. [Webhook node](https://docs.n8n.io/integrations/builtin/core-nodes/n8n-nodes-base.webhook)
- Async job + polling: not published. The Immediately response mode returns "Workflow got started" without an execution ID; GET /executions/{id} reads runs you already know about. [Executions API](https://docs.n8n.io/connect/n8n-api/executions)
- Webhook trigger URL: yes. [Webhook node](https://docs.n8n.io/integrations/builtin/core-nodes/n8n-nodes-base.webhook)
- Completion webhook: not published as a platform setting. [Webhook node](https://docs.n8n.io/integrations/builtin/core-nodes/n8n-nodes-base.webhook)
- Idempotency key: not published. [n8n API](https://docs.n8n.io/connect/n8n-api)
- Cost in run response: not published. [n8n API](https://docs.n8n.io/connect/n8n-api)
- MCP server: yes. Instance-level MCP access runs workflows enabled for MCP with execute_workflow, and the MCP Server Trigger node exposes one workflow as a server. [Connect to n8n MCP server](https://docs.n8n.io/connect/connect-to-n8n-mcp-server)
- Scoped permissions: yes, on the Enterprise plan, where API keys take scopes. [Authentication](https://docs.n8n.io/connect/n8n-api/authentication)
- Self-host: yes. Docker, npm or Docker Compose on your own infrastructure. [Host n8n](https://docs.n8n.io/deploy/host-n8n)

## Selection notes

Flora and Wireflow document the most of the run lifecycle: a saved-workflow run by ID, polling, an idempotency key, cost reported per run, scoped keys and a hosted MCP server. Flora documents a signed completion callback; Wireflow documents an inbound trigger URL instead. ComfyUI and Comfy Cloud share one v2 contract, so an integration can move between your own GPU and Comfy's by changing the base URL, but you send the whole graph with each run. n8n is the self-hosted option when the workflow is mostly automation around model calls. Figma Weave and Freepik Spaces can be reached from an agent through MCP, but neither documents a REST call that runs a saved workflow today.

## Acceptance recipe

- Pick one real workflow and note its inputs, its models and one expected output.
- Start a run from code the documented way: by saved ID, or by posting the exported graph.
- Retry the same request with the same idempotency key, where one exists, and confirm no duplicate run.
- Fetch the result by polling or a completion webhook, then force a failure and check the error you get back.
- Compare the cost the platform reports for the run with your billing page.
- Create a key with the narrowest scope that can still run the workflow and confirm it cannot edit or delete.

## Evaluation record

Record the platform, workflow revision, request ID, idempotency key, final status, output location, reported cost, billed cost and the scope of the key used. Keep failed runs next to successful ones so that a retry does not hide the original result.

## How this list is maintained

- [`data/tools.json`](data/tools.json) is the source of truth. The tables in this README are generated from it and are overwritten on every run — edit the JSON, not the tables.
- [`scripts/update.js`](scripts/update.js) fetches star counts and latest release tags from the GitHub API for the tools that publish an official repo, stamps the check date, and regenerates the tables. `--offline` regenerates without the network; `--check` exits non-zero if the README has drifted from the data.
- [`.github/workflows/refresh.yml`](.github/workflows/refresh.yml) runs it weekly and on manual dispatch, and commits only when the data actually changed.
- Prices are deliberately not stored as numbers. A stale price in a comparison table is worse than no price, so the table links to each vendor's own pricing page.

## Contributing

Corrections and additions are welcome, including corrections to the entry for the tool that maintains this list. Open an issue with the tool name, a working link, one line on what it does that the tools already listed do not, and one line on where it stops. Entries are judged on whether they are usable today, not on popularity. Full rules in [CONTRIBUTING.md](CONTRIBUTING.md).

## License

[CC0 1.0 Universal](LICENSE) — public domain. Take the data, fork the list, no attribution required.

---

Maintained by [a1adams](https://github.com/a1adams).
