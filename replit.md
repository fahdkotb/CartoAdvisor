# Workspace

## Overview

pnpm workspace monorepo using TypeScript. Each package manages its own dependencies.
Also includes a Python Streamlit application for professional bilingual cartographic analysis.

## Stack

- **Monorepo tool**: pnpm workspaces
- **Node.js version**: 24
- **Package manager**: pnpm
- **TypeScript version**: 5.9
- **API framework**: Express 5
- **Database**: PostgreSQL + Drizzle ORM
- **Validation**: Zod (`zod/v4`), `drizzle-zod`
- **API codegen**: Orval (from OpenAPI spec)
- **Build**: esbuild (CJS bundle)
- **Python version**: 3.11

## Artifacts

### Cartographic Assistant (Streamlit)
- **Location**: `artifacts/cartographic-assistant/`
- **Run**: `cd artifacts/cartographic-assistant && streamlit run app.py --server.port 5000 --server.address 0.0.0.0`
- **Port**: 5000
- **Workflow**: "Cartographic Assistant"

#### Features
- **Bilingual UI**: English / Arabic toggle with full RTL layout switch, Noto Sans Arabic font, translated all strings
- **Vector Mode (GeoJSON / KML)**:
  - Folium dark-theme interactive map (CartoDB Dark Matter) with teal styling + tooltips
  - Feature Counter: separate counts for Points, Lines, Polygons, Total
  - Topology Health Check: overlapping polygon detection (Shapely) + invalid line detection
  - Projection Recommendation: UTM zone auto-detected from coordinate centroid (Pyproj)
  - Attribute table (Pandas)
- **Raster Mode (JPG/PNG)**:
  - GPT-4o Vision Cartographic Audit: Legend, Scale Bar, North Arrow, Coordinate Grid
  - Critique Score out of 10 with color-coded progress bar
  - Element status cards (Present/Partial/Missing) with detail text
  - Overall assessment summary
- **AI Map Advisor**: Bilingual advice on Symbology, Labeling, and Projection in selected language
- **Export Report**: Download full analysis as UTF-8 text file (`analysis_report.txt` / `تقرير_التحليل.txt`)
- **Dark GIS theme**: near-black backgrounds, teal accent (#00d4aa), monospace + Noto Sans Arabic fonts

#### Python Dependencies
streamlit, folium, streamlit-folium, openai, pandas, geopandas, Pillow, shapely, pyproj, fiona, fpdf2

#### AI Integration
Replit AI Integrations (OpenAI) — env vars `AI_INTEGRATIONS_OPENAI_BASE_URL` and `AI_INTEGRATIONS_OPENAI_API_KEY` (auto-provisioned, no user API key needed)

## Key Commands

- `pnpm run typecheck` — full typecheck across all packages
- `pnpm run build` — typecheck + build all packages
- `pnpm --filter @workspace/api-spec run codegen` — regenerate API hooks and Zod schemas from OpenAPI spec
- `pnpm --filter @workspace/db run push` — push DB schema changes (dev only)
- `pnpm --filter @workspace/api-server run dev` — run API server locally

See the `pnpm-workspace` skill for workspace structure, TypeScript setup, and package details.
