# React TS Widget

A single-file React counter component written in TypeScript. It's a stub — a starting point, not a finished app.

## What's here

One file: `app.tsx`. It defines a `Widget` component that takes a `title` prop and holds a numeric `count` in state. The UI is a heading, a line showing the current count, and an "Inc" button that adds one on each click.

```tsx
interface Props {
    title: string;
}

const Widget: React.FC<Props> = ({ title }) => {
    const [count, setCount] = useState<number>(0);
    return (
        <div>
            <h1>{title}</h1>
            <p>Count: {count}</p>
            <button onClick={() => setCount(count + 1)}>Inc</button>
        </div>
    );
}
export default Widget;
```

That's the whole thing. It shows the basic shape of a typed React component: a `Props` interface, `useState<number>`, and a default export.

## Scope

This is a learning stub (the source comments even say `// App.tsx (Stub)`). There's no `package.json`, no bundler config, no entry point that mounts the component, and no tests. `app.tsx` exports `Widget` but nothing imports or renders it yet.

## Running it

The `.replit` file says:

```
run = "npm install && npm start"
```

That command won't work as-is — there's no `package.json` for npm to install from, and nothing renders `Widget`. To actually run it you'd need to scaffold a project around this file. For example, with Vite:

```bash
npm create vite@latest my-app -- --template react-ts
```

Then drop `app.tsx` in, import `Widget` in your entry file, and mount it:

```tsx
import Widget from './app';
// <Widget title="Hello" />
```

## Tech

- TypeScript
- React (`useState`, function component, `React.FC`)
