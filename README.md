# oddblog

Simple Astro frontend for a personal blog/portfolio, with content managed in [Sanity](https://www.sanity.io).

## Project structure

```text
/
├── public/
├── src/
│   └── pages/
│       ├── index.astro
│       └── blog/[slug].astro
├── studio/              # Sanity Content Studio
└── package.json
```

Pages live in `src/pages/`. Content schemas and the editing UI live in `studio/`.

## Getting started

1. Install dependencies:

   ```sh
   npm install
   cd studio && npm install && cd ..
   ```

2. Copy environment variables:

   ```sh
   cp .env.example .env
   ```

3. Start Sanity Studio (content editing):

   ```sh
   npm run studio
   ```

   Studio runs at [http://localhost:3333](http://localhost:3333). Create a **Post** document there.

4. Start the Astro site:

   ```sh
   npm run dev
   ```

   Site runs at [http://localhost:4321](http://localhost:4321).

## Commands

| Command                   | Action                                      |
| :------------------------ | :------------------------------------------ |
| `npm install`             | Install Astro dependencies                  |
| `npm run dev`             | Start dev server at `localhost:4321`        |
| `npm run build`           | Build for production to `./dist/`           |
| `npm run preview`         | Preview the production build locally        |
| `npm run studio`          | Start Sanity Studio at `localhost:3333`     |
| `npm run studio:deploy`   | Deploy Studio to sanity.io                  |

## Documentation

- [Astro docs](https://docs.astro.build)
- [Sanity + Astro](https://www.sanity.io/docs/astro/introduction)
