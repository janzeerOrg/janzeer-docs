# OpenAPI Specification

`openapi.json` is the machine-readable OpenAPI 3 spec for the Janzeer node REST API (`/api/v1/`), as served by a
node's `GET /docs/api-docs`. Import it into Swagger UI, Postman, Insomnia, or an OpenAPI code generator. Every
documented response schema is the node's envelope `RestResponse {timestamp, version, payload}` (the node wraps
success AND error bodies; `payload` holds the documented type, or `{status, message, type?}` on errors). JSON-RPC
(`POST /rpc`, `ws://…/rpc/ws`) is not part of this document — see the developer guide §2.14. The official SDKs
(`@janzeer/sdk`, `janzeer_sdk`, `org.janzeer:janzeer-sdk`) are hand-written against this contract.

To re-export (from `backend_v03/`, JDK 17):

```bash
./gradlew test --tests "*ApiControllerIT.openapi*"   # writes build/openapi.json (pretty-printed) and asserts the metadata
cp build/openapi.json ../docs/api/openapi.json
# or from a running node:
curl -s http://localhost:7019/docs/api-docs | python3 -m json.tool > ../docs/api/openapi.json
```

A node also serves interactive Swagger UI at `http://localhost:7019/docs/swagger-ui.html`.
See `../en/api-reference.md` for the human-readable reference.
