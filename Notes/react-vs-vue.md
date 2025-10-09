# 🧭 1. Core Concept Difference (React vs Vue)

| Concept                 | React                                          | Vue                                                           |
| ----------------------- | ---------------------------------------------- | ------------------------------------------------------------- |
| **Component Structure** | JSX (JavaScript + XML) Functions returning JSX | HTML-based templates (.vue files) SFC (Single File Component) |
| **State Management**    | External libraries (Redux, Zustand)            | Built-in Vuex/Pinia, reactive data                            |
| **Styling**             | CSS-in-JS or external stylesheets              | Scoped CSS in component files                                 |
| **Performance**         | Virtual DOM with reconciliation                | Virtual DOM + reactive system                                 |
| **Mobile Development**  | React Native                                   | NativeScript Vue, Quasar                                      |
| **Reactivity**          | Manual state updates via useState, useEffect   | Automatic state update with ref(), reactivity()               |
| **Routing**             | react-router or built-in in Next.js            | vue-router or built-in in Nuxt.js                             |
| **SSR / SSG**           | Next.js                                        | Nuxt.js                                                       |

---

# 🧭 2. Life Cycle Difference

| Phase       | React Hook                                 | Vue Equivalent                  |
| ----------- | ------------------------------------------ | ------------------------------- |
| On Mount    | `useEffect(() => {}, [])`                  | `onMounted(() => {})`           |
| On Unmount  | `useEffect(() => { return () => {} }, [])` | `onUnmounted(() => {})`         |
| Watch State | Manual inside `useEffect`                  | `watch(refVar, (newVal) => {})` |
