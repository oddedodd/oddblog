# oddblog

Simple Astro frontend for a personal blog/portfolio, with content in Sanity.

## Sanity

- Studio lives in `studio/` — run with `npm run studio` (port 3333)
- Astro queries content via `@sanity/astro` and `import { sanityClient } from 'sanity:client'`
- Project ID and dataset are in `.env` (`PUBLIC_SANITY_PROJECT_ID`, `PUBLIC_SANITY_DATASET`)
- Post schema is in `studio/schemaTypes/post.ts`

## Development

When starting the dev server, use background mode:

```
astro dev --background
```

Manage the background server with `astro dev stop`, `astro dev status`, and `astro dev logs`.

### Build restriction

Agents must never run `npm run build`, either in the project root or in `studio/`.

## Documentation

Full documentation: https://docs.astro.build

Consult these guides before working on related tasks:

- [Adding pages, dynamic routes, or middleware](https://docs.astro.build/en/guides/routing/)
- [Working with Astro components](https://docs.astro.build/en/basics/astro-components/)
- [Using React, Vue, Svelte, or other framework components](https://docs.astro.build/en/guides/framework-components/)
- [Adding or managing content](https://docs.astro.build/en/guides/content-collections/)
- [Adding styles or using Tailwind](https://docs.astro.build/en/guides/styling/)
- [Supporting multiple languages](https://docs.astro.build/en/guides/internationalization/)
