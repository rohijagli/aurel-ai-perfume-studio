# AUREL — AI Perfume Studio

*Your scent, imagined.*

A presentation prototype of an AI perfume generation, cloning and customization platform.
Frontend only, roughly 20% of the full system. All "AI" responses are mock data.

**Stack:** Next.js 15 (App Router) · React 19 · TypeScript · Tailwind CSS v4 · Framer Motion · Lucide icons

## Run it

```bash
npm install
npm run dev        # http://localhost:3000
```

Production build: `npm run build && npm start` · Type check: `npm run typecheck`

Requires Node 18.18+ (Node 20+ recommended). Fonts (Cormorant Garamond + Manrope) load from Google Fonts, so the first load needs internet.

## Demo script

**Primary flow:**
1. Home, then **Create with AI**
2. Type `Warm, luxurious and mysterious for winter evenings` (or click the "Try the example" link)
3. **Generate My Perfume**. A ~3s loading sequence plays, then **NOIR ÉCLAT** appears (Woody Amber, 91% AI confidence)
4. **Customize This Scent**. Swap notes (max 6), drag the sliders and watch the bottle colour change, rename it
5. **Save**. A toast links to **My Fragrances**, where the creation appears and the counters go up

**Secondary flow:** Clone, type `Bleu de Chanel` (or click a chip), **Analyze Perfume**, 91% similarity result, **Customize the Clone**

Other things to show:
- Clone, "Use a sample image", Analyze Image, "Luxury Oud Perfume" analysis
- Explore search (try `oud`, `rose`, `eclat`) and the family filters
- The heart icon on any card, then the Favorites tab
- The mobile hamburger menu

Each suggestion chip on the generator produces a different mock result (5 archetypes).

## Project structure

```
src/
  app/                  routes: /, /ai-perfume, /clone, /customize, /explore, /my-fragrances
    layout.tsx          fonts, navbar, footer, toast, StudioProvider
    template.tsx        page transition
  components/           PerfumeBottle, PerfumeCard, AIResult, NoteSelector, ScentSlider,
                        UploadBox, LoadingSequence, Hero, FeatureCard, Navbar, Footer, ...
  context/StudioContext.tsx   draft being customized, saved creations, favorites, cart, toasts
  data/                 perfumes.ts, notes.ts, collection.ts (mock data)
  lib/
    mockAI.ts           generatePerfume(), analyzePerfume(), clonePerfume() (MOCKED)
    scent.ts            scent dimensions, profile → bottle colour
    types.ts            shared types = the expected API JSON shape
```

`<PerfumeBottle name="NOIR ÉCLAT" color="#5B3A2A" size="lg" />` is fully reusable (sizes `sm | md | lg | xl`).

## Connecting a real backend later

- **AI:** replace the bodies of the three functions in `src/lib/mockAI.ts` with `fetch` calls to your API routes. The UI only depends on their signatures and the `ScentResult` type.
- **Persistence:** `StudioContext` stores data in `localStorage`/`sessionStorage`. Search for `TODO(api)` to find every place a real endpoint belongs (save, favorites, cart, catalogue).

## Intentionally not implemented

Real AI or computer vision, fragrance chemistry, authentication, database, payments or checkout, orders, inventory, admin, email. "Add to Cart" and "Save" are demo-only and persist in your browser.
