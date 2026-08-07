# docs-site — Mintlify (público)

Documentación pública PSP para **https://docs.gallo-pay.com**.

No confundir con [`../docs/`](../docs/) (ops / arquitectura interna).

## Restricción Mintlify

Mintlify (plan actual) **solo conecta repositorios públicos**. El monorepo `gallo-pay` es **privado**, por eso el deploy no usa este path en el monorepo.

| Repo | Visibilidad | Rol |
|------|-------------|-----|
| `gpellegrinigallo/gallo-pay` | private | fuente de verdad (`docs-site/` aquí) |
| [`gpellegrinigallo/gallo-pay-docs`](https://github.com/gpellegrinigallo/gallo-pay-docs) | **public** | mirror para Mintlify (`docs.json` en la **raíz**) |

## Contenido (fuente en monorepo)

| Path | Rol |
|------|-----|
| `docs.json` | Config Mintlify |
| `index.mdx` / `quickstart.mdx` | Intro |
| `guias/*.mdx` | Guías |
| `openapi.json` | Spec cliente (sync CI) |

## Publicar / espejar

Desde la raíz del monorepo:

```bash
./scripts/sync-openapi.sh          # opcional: refrescar OpenAPI
./scripts/mirror-docs-site.sh      # push → gallo-pay-docs (público)
```

CI: `.github/workflows/mirror-docs-site.yml` (tras push a `main` que toque `docs-site/`, o manual).

## Conectar Mintlify (una vez)

1. Proyecto en [app.mintlify.com](https://app.mintlify.com).
2. GitHub App en el repo **público** `gallo-pay-docs` (no en el monorepo).
3. **No** activar subdirectory: `docs.json` está en la **raíz** del mirror.
4. Custom domain `docs.gallo-pay.com` — ver abajo y [`../produccion/dns-godaddy.md`](../produccion/dns-godaddy.md).

## Custom domain

| Tipo | Nombre | Valor |
|------|--------|--------|
| CNAME | `docs` | `<subdomain>.mintlify.app` (exacto del dashboard) |

## Preview local

```bash
cd docs-site && npx mintlify dev
```
