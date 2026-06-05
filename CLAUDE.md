# Purioxa — Shopify MCP Server

## Project Context

This repo is the **Shopify MCP Server** for the Purioxa store. It connects AI assistants (Claude Desktop, Claude Code) to the Shopify Admin API via GraphQL.

### The Store
- **Name**: Purioxa
- **Domain**: purioxa.com
- **Owner**: hicham.ecom438@gmail.com
- **Plan**: Shopify Basic
- **Country**: Canada
- **Currency**: USD

### The Product
- **Name**: Ultrasonic Jewelry Cleaner Machine (Purioxa Pro)
- **Price**: $64.99 USD
- **GID**: `gid://shopify/Product/9331630670043`
- **Variant GID**: `gid://shopify/ProductVariant/48734060347611`
- **Stock**: 7 units
- **Vendor**: Purioxa™
- One product, one variant, no SKU
- 6 product images (hero, 3 lifestyle, cinematic, dimensions)
- Emotional copywriting angle: jewelry loses shine over time, Purioxa Pro restores it in 5 min

### Business Context
- One-product ecommerce store
- Target market: jewelry owners (engagement rings, gold chains, watches)
- Positioning: professional jeweler-grade cleaning at home
- Key differentiator: 40,000 Hz ultrasonic, viewing window, no chemicals

---

## Tech Stack

- **TypeScript** + Node.js
- **`@modelcontextprotocol/sdk`** — MCP server with StdioServerTransport
- **`graphql-request`** — Shopify Admin GraphQL client
- **Zod** — input validation
- **Shopify API**: `2025-01`

## Auth
- `SHOPIFY_ACCESS_TOKEN` via `--accessToken` CLI arg or `.env`
- `MYSHOPIFY_DOMAIN` via `--domain` CLI arg or `.env`

---

## MCP Tools Available

| Tool | File |
|---|---|
| `get-products` | `src/tools/getProducts.ts` |
| `get-product-by-id` | `src/tools/getProductById.ts` |
| `update-product` | `src/tools/updateProduct.ts` |
| `get-collections` | `src/tools/getCollections.ts` |
| `update-collection` | `src/tools/updateCollection.ts` |
| `get-pages` | `src/tools/getPages.ts` |
| `update-page` | `src/tools/updatePage.ts` |
| `get-blogs` | `src/tools/getBlogs.ts` |
| `get-blog-by-id` | `src/tools/getBlogById.ts` |
| `update-blog` | `src/tools/updateBlog.ts` |
| `get-articles` | `src/tools/getArticles.ts` |
| `get-article-by-id` | `src/tools/getArticleById.ts` |
| `update-article` | `src/tools/updateArticle.ts` |
| `create-article` | `src/tools/createArticle.ts` |
| `search-shopify` | `src/tools/searchShopify.ts` |

---

## Skills Installed (`.claude/skills/`)

| Skill file | Command | Purpose |
|---|---|---|
| `stop-slop.md` | `/stop-slop` | Remove AI writing patterns from copy |
| `ui-ux-pro-max.md` | `/ui-ux-pro-max` | UI/UX design intelligence (67 styles, 161 palettes) |
| `impeccable.md` | `/impeccable` | Frontend design quality & anti-patterns |
| `seo.md` | `/seo` | Full SEO audit (technical, E-E-A-T, schema, GEO) |
| `seo-audit.md` | `/seo-audit` | SEO audit workflow |
| `copywriting.md` | `/copywriting` | Conversion copywriting for pages |
| `cro.md` | `/cro` | Conversion rate optimization |
| `ads.md` | `/ads` | Paid ads copy & strategy |
| `social-media.md` | `/social-media` | Social media content |
| `emails.md` | `/emails` | Email marketing copy |
| `product-marketing.md` | `/product-marketing` | Product marketing strategy (foundational) |
| `competitor-profiling.md` | `/competitor-profiling` | Competitor analysis |
| `content-strategy.md` | `/content-strategy` | Content strategy planning |

---

## Git

- **Working branch**: `claude/intelligent-bell-YtlAD`
- **Remote**: `4yffhbbgsv-art/shopify-mcp`
- Always develop on `claude/intelligent-bell-YtlAD`, never push to `main` directly

---

## Development Notes

- Entry point: `src/index.ts`
- Add new tools: create `src/tools/newTool.ts`, import in `src/index.ts`, call `initialize()` and register with `server.tool()`
- Product GID format: `gid://shopify/Product/NUMERIC_ID`
- All mutations return `userErrors` — always check them
