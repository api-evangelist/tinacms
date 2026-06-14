# TinaCMS GraphQL API

TinaCMS generates a GraphQL Content API from your schema definitions in `tina/config.ts`. The API exposes every content collection you define as both single-document queries (`<collection>(relativePath: String!)`) and paginated list queries (`<collection>Connection(...)`) following the Relay cursor-based pagination specification. Built-in root fields include `node`, `document`, `collection`, and `collections` for cross-collection access. All documents implement the `Node` and `Document` interfaces, carrying a system metadata field `_sys` (filename, path, breadcrumbs, extension, template, collection) alongside their user-defined fields.

Authentication to the hosted TinaCloud endpoint uses a bearer token issued per project. The token is supplied in the `X-API-KEY` header or the `Authorization: Bearer <token>` header. When running locally with `tinacms dev`, the API is available without authentication at `http://localhost:4001/graphql`. For production projects the per-project endpoint encodes the clientId and the Git branch, so each branch of your content has its own addressable URL.

Mutations mirror the query surface: `createDocument`, `updateDocument`, `deleteDocument`, and `addPendingDocument` operate across all collections using a `collection` discriminator plus `relativePath`. Per-collection typed mutations (`update<Collection>`, `create<Collection>`) are also generated, accepting a strongly-typed `params` input object derived directly from the collection's field definitions. Rich-text fields are stored and returned as a custom JSON-encoded AST rather than raw markdown strings.

**Endpoint:** https://content.tinajs.io/1.0/content/{clientId}/github/{branch}

**Local Development Endpoint:** http://localhost:4001/graphql

**Documentation:** https://tina.io/docs/graphql/overview

**References:**
- Documentation: https://tina.io/docs/graphql/overview
- GettingStarted: https://tina.io/docs/setup-overview
- Queries: https://tina.io/docs/graphql/queries/query-documents
- Mutations: https://tina.io/docs/graphql/queries/update-document
- Schema Reference: https://tina.io/docs/reference/schema
