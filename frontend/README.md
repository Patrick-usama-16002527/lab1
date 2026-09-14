# React + Vite

This template provides a minimal setup to get React working in Vite with HMR and some ESLint rules.

Currently, two official plugins are available:

- [@vitejs/plugin-react](https://github.com/vitejs/vite-plugin-react/blob/main/packages/plugin-react) uses [Oxc](https://oxc.rs)
- [@vitejs/plugin-react-swc](https://github.com/vitejs/vite-plugin-react/blob/main/packages/plugin-react-swc) uses [SWC](https://swc.rs/)

## React Compiler

The React Compiler is not enabled on this template because of its impact on dev & build performances. To add it, see [this documentation](https://react.dev/learn/react-compiler/installation).

## Expanding the ESLint configuration

If you are developing a production application, we recommend using TypeScript with type-aware lint rules enabled. Check out the [TS template](https://github.com/vitejs/vite/tree/main/packages/create-vite/template-react-ts) for information on how to integrate TypeScript and [`typescript-eslint`](https://typescript-eslint.io) in your project.

---

## Practice Assignment 1 – Filter & Search Todos

### What I completed

**Backend (`backend/controllers/todoController.js`)**
- Modified `getTodos` to read the `done` query parameter from `req.query`.
- Built a filter object conditionally: when `done` is not provided, the filter stays empty and all todos are returned. When provided, it filters by `done: true` or `done: false`.
- Passed the filter into `Todo.find(filter)`.

**Frontend API (`frontend/src/api/todos.js`)**
- Updated `fetchTodos` to accept an optional `done` argument and send it as a query parameter using axios (`api.get('/', { params: { done } })`).

**Frontend UI (`frontend/src/App.jsx`)**
- Added `filter` state (`'all'`, `'active'`, `'done'`).
- Updated the `useEffect` to compute the `done` value based on the filter and re-fetch todos whenever `filter` changes (added `filter` to the dependency array).
- Added All / Active / Done buttons above the todo form to let the user switch filters.

### Server-side vs client-side filtering
I implemented server-side filtering as instructed: each time the filter changes, a new request is sent to the backend with the `done` query parameter, and the database performs the filtering. This is more scalable for large datasets since it avoids downloading unnecessary data and offloads filtering work to the database. Client-side filtering (fetching all todos once and filtering in React) would feel faster for small datasets since there's no extra network round-trip, but it doesn't scale well and wastes bandwidth as the number of todos grows.
