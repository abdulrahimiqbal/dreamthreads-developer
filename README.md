# DreamThreads Dream Interpretation API

Build context-aware dream analysis into a journal, sleep product, publication,
research tool, community, or AI agent.

The DreamThreads Dream Interpretation API accepts dream text plus optional
waking-life or physiological context and returns a tentative reflection as
JSON. Unlike a fixed dream dictionary API, DreamGraph weighs emotion, agency,
action, threat, outcome, recurrence, and context—and exposes the factors that
changed the reading.

- Developer guide and access: <https://mydreamthreads.xyz/dream-interpretation-api>
- Interactive API reference: <https://abdulrahimiqbal.github.io/dreamthreads-developer/>
- OpenAPI 3.1: <https://mydreamthreads.xyz/dream-interpretation-api/openapi.json>
- APIs.json 0.21 discovery index: <https://mydreamthreads.xyz/apis.json>
- Dream MCP server guide: <https://mydreamthreads.xyz/dream-mcp-server>
- Public MCP endpoint: `https://mydreamthreads.xyz/mcp`
- MCP registry manifest: <https://mydreamthreads.xyz/.well-known/mcp/server.json>
- Postman collection: <https://mydreamthreads.xyz/dream-interpretation-api/postman.json>
- AI tool manifest: <https://mydreamthreads.xyz/.well-known/ai-plugin.json>
- Production base: `https://mydreamthreads.xyz/api/v1/dreamgraph`
- Free no-key parser: `POST https://mydreamthreads.xyz/api/v1/dreamgraph/public/parse`
- Free dream journal templates: <https://mydreamthreads.xyz/dream-journal/template>

## Free quickstart—no API key

The public parser is useful for prototypes, classrooms, evaluations, and
low-volume tools. It returns structured dream factors, not a generated
interpretation. Dream text is processed in memory and is not stored or added to
the contribution corpus.

```bash
curl https://mydreamthreads.xyz/api/v1/dreamgraph/public/parse \
  -H "Content-Type: application/json" \
  -d '{
    "text": "I watched a snake in my garden. I felt peaceful."
  }'
```

The public endpoint supports CORS and is limited to 12 requests per minute and
100 requests per day per client. Rate-limit state is returned in standard
response headers.

## Public dream MCP server—no API key

Connect a compatible Model Context Protocol client to the Streamable HTTP URL
Read the [dream MCP server guide](https://mydreamthreads.xyz/dream-mcp-server),
then connect a compatible client to `https://mydreamthreads.xyz/mcp`. The server exposes two bounded, read-only
tools:

- `parse_dream` extracts structured dream context without storing dream text;
- `search_dream_concepts` searches the stable DreamGraph vocabulary.

The server does not generate diagnoses, predictions, supernatural claims, or
fixed symbolic meanings. Its official-registry metadata is [`server.json`](server.json).

## Contextual interpretation quickstart

Partner keys belong in a server-side secret manager. Never expose one in
browser JavaScript.

```bash
curl https://mydreamthreads.xyz/api/v1/dreamgraph/interpret \
  -H "Authorization: Bearer $DREAMTHREADS_API_KEY" \
  -H "Content-Type: application/json" \
  -H "X-Request-ID: your-request-123" \
  -d '{
    "text": "I watched a snake in my garden. I felt peaceful.",
    "waking_context": "I recently started caring for a garden."
  }'
```

See [`examples/`](examples/) for JavaScript, Python, and cURL clients. The
machine-readable contract is [`openapi.json`](openapi.json), and
[`postman_collection.json`](postman_collection.json) can be imported directly
into Postman. [`apis.json`](apis.json) publishes the authoritative discovery
index for API catalogs and AI agents. [`ai-plugin.json`](ai-plugin.json) points
compatible discovery tools to the canonical OpenAPI definition and safety
requirements.

## Which kind of dream API is this?

| Search term | Typical contract | DreamThreads |
| --- | --- | --- |
| Dream interpretation API | Dream text in; a user-facing reading out | Yes—tentative reflection plus a factor trace |
| Dream analysis API | Structured factors and reasoning | Yes—parsed context, reason trace, and typed provenance |
| Dream dictionary API | One symbol mapped to one fixed definition | Intentionally no—context can change the reading |

## Endpoints

| Endpoint | Purpose |
| --- | --- |
| `GET /health` | Free no-key API-edge liveness check for integration tests and connectivity diagnostics |
| `POST /public/parse` | Free no-key structured parsing for prototypes and evaluation; 12/minute and 100/day per client |
| `POST /interpret` | Contextual reflection, structured dream, factor trace, provenance, diagnostics, timing, and attribution |
| `POST /parse` | Entities, actions, emotions, locations, agency, threat, outcome, recurrence, and parser version without generating a reading |

Successful responses use `{ data, request_id, version }`. Errors use
`{ error, request_id, version }`. Dream text is required and can contain up to
6,000 characters. Each partner has an origin allowlist and requests-per-minute
quota.

## API or hosted embed?

Use the REST API when your server owns the user interface. Use the hosted embed
when a publication or site wants to ship a responsive interpreter with one
script and no long-lived key in browser code. Request either path through the
[partner intake](https://mydreamthreads.xyz/dream-interpretation-api#request-access).

## Privacy and safety

- Interpretations are reflective—not diagnostic, predictive, or fixed truths.
- The public parser does not store submitted dream text or create a DreamGraph contribution.
- API dream text is not added to the DreamGraph contribution corpus.
- Integrators must provide the disclosure and obtain the consent their use case
  requires.
- Preserve the returned DreamThreads attribution link and uncertainty language.
- Never put real dream text, credentials, or personal information in issues.

Read the [privacy policy](https://mydreamthreads.xyz/privacy),
[terms](https://mydreamthreads.xyz/terms), and
[editorial policy](https://mydreamthreads.xyz/editorial-policy).

## Free dream journal template

The [`dream-journal-template/`](dream-journal-template/) directory mirrors the
free public field kit in four formats:

- fillable and printable PDF;
- editable Word/Google Docs file;
- Notion-ready Markdown;
- CSV dream log.

The canonical guide explains every field and how to use it:
<https://mydreamthreads.xyz/dream-journal/template>.

## Support

Use the [public access form](https://mydreamthreads.xyz/dream-interpretation-api#request-access)
for an integration. For a security issue, follow [SECURITY.md](SECURITY.md).
The DreamThreads application source and private infrastructure are not part of
this repository.
