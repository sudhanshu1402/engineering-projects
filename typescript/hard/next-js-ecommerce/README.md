# Next.js Ecommerce

A single-page Next.js snippet showing static-site generation with `getStaticProps`.

## What this is

One file, one page. It renders a hardcoded product list at build time using Next.js's `getStaticProps`. Despite the name, there's no cart, no checkout, no data source, and no styling — it's a practice exercise for the SSG data-fetching pattern, not an actual store.

## What the code does

`pages/index.tsx`:

- Declares a `Product` type (`id`, `name`).
- `getStaticProps` returns a fixed array `[{ id: 1, name: "Item 1" }]` as props. In a real app this is where you'd fetch from an API or CMS; here it's stubbed.
- The `Home` component maps those props to an `<ul>` of `<li>` items, keyed by `id`.

That's the whole thing.

## Stack

- Next.js (Pages Router — uses the `pages/` directory and `getStaticProps`)
- TypeScript
- React (JSX)

There's no `package.json` in this folder, so exact versions aren't pinned here.

## Run it

The `.replit` file runs:

```bash
npm install && npm start
```

To run it standalone you'd need a Next.js project scaffold around it (a `package.json` with `next`, `react`, `react-dom`, and the standard `next dev` / `next build` scripts), then drop `pages/index.tsx` into the `pages/` directory. On its own the folder is just the one page component.

## Output

The rendered page:

```html
<ul>
  <li>Item 1</li>
</ul>
```

## Scope

Learning exercise. The point is the `getStaticProps` + typed-props pattern, not a working ecommerce app. The "hard" difficulty label overstates it — the code is a minimal SSG example.
