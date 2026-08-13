# DreamThreads Dream Interpretation API

Build context-aware dream analysis into a journal, sleep product, publication,
research tool, community, or AI agent.

The DreamThreads Dream Interpretation API accepts dream text plus optional
waking-life or physiological context and returns a tentative reflection as
JSON. Unlike a fixed dream dictionary API, DreamGraph weighs emotion, agency,
action, threat, outcome, recurrence, and context—and exposes the factors that
changed the reading.

- Developer guide and access: <https://mydreamthreads.xyz/dream-interpretation-api>
- OpenAPI 3.1: <https://mydreamthreads.xyz/dream-interpretation-api/openapi.json>
- Production base: `https://mydreamthreads.xyz/api/v1/dreamgraph`
- Free dream journal templates: <https://mydreamthreads.xyz/dream-journal/template>

## Quickstart

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
machine-readable contract is [`openapi.json`](openapi.json).

## Endpoints

| Endpoint | Purpose |
| --- | --- |
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
