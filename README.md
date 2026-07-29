# oddblog

Simple Astro frontend for a personal blog/portfolio.

## Project structure

```text
/
├── public/
├── src/
│   └── pages/
│       └── index.astro
└── package.json
```

Pages live in `src/pages/` — each `.astro` or `.md` file becomes a route. Components go in `src/components/`, and static assets go in `public/`.

## Commands

Run from the project root:

| Command                   | Action                                      |
| :------------------------ | :------------------------------------------ |
| `npm install`             | Install dependencies                        |
| `npm run dev`             | Start dev server at `localhost:4321`        |
| `npm run build`           | Build for production to `./dist/`           |
| `npm run preview`         | Preview the production build locally        |
| `npm run astro ...`       | Run Astro CLI commands                      |

## Documentation

[Astro docs](https://docs.astro.build)
