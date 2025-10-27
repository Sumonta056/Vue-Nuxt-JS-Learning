## Vue JS Resource

This repository contains a collection of resources and examples for learning and working with Vue.js, a progressive JavaScript framework for building user interfaces.

### Contents

- [Vue.js Official Documentation](https://vuejs.org/guide/quick-start.html)
- [Vue.js Explained in 100 Seconds](https://youtu.be/nhBVL41-_Cw?si=4eIkd45jzlxgeN4Z)
- [Vue.JS Setup with Tailwind CSS](https://youtu.be/P5d_UUxqOzs?si=KeMc70jda6jCQzhj), [Tailwind CSS Vue Doc](https://tailwindcss.com/docs/installation/using-vite)
- [HuXn WebDev : Master Vue.js Composition API: Build 10 Stunning Projects for Real-world Expertise!](https://www.youtube.com/watch?v=pgWZLS75Nmo), [GitHub Repo](https://github.com/HuXn-WebDev/Vue.js-Complete-Course-With-10-Projects)
- [Simple Expense Tracker App using Vue 3 and Composition API](https://www.youtube.com/watch?v=hNPwdOZ3qFU)

### Resources

- [Dummy Product Json API for basic implementation](https://dummyjson.com/docs/products)

# Vue.js Learning Progress

This document tracks the Vue.js concepts and features I have learned and implemented in this workspace.

## 📚 Topics Covered

## Intro to Vue 3

1. ref : ref is like a reactive variable that hold value and helps to achieve reactivity in vue 3.
2. reactivity : It is a way to make data reactive between script and template.
3. v-bind: It is used to bind data dynamically to HTML attributes. like :class, :style etc.
4. V-if : Conditional rendering of elements based on a boolean expression. V-else-if and V-else can also be used for multiple conditions.
5. V-for : It is used to render a list of items by iterating over an array or object.
6. Watch : It is used to watch for changes in a reactive data property and execute a function when that property changes.
7. V-On: It is used to listen to DOM events and execute methods when those events are triggered. like @click, @submit etc.
8. Class and Style Binding: Vue 3 allows dynamic binding of classes and styles using the v-bind directive or its shorthand syntax (:). Example: :class="{ active: isActive }" or :style="{ color: activeColor }".
9. computed(): Computed properties are used to create derived state based on reactive data. They are cached and only re-evaluated when their dependencies change.
10. toRefs(): toRefs is a function that converts a reactive object into a plain object where each property is a ref. This is useful when destructuring reactive objects while maintaining reactivity.
11. emit(): emit is used to send custom events from a child component to its parent component, allowing communication between components.
12. defineProps(): defineProps is a function used in the script setup syntax to define the props that a component can accept from its parent component.
13. reactive(): reactive is a function that creates a reactive object, allowing for deep reactivity in Vue 3 applications.
14. v-model: reactive two-way data binding between form input elements and component data properties.
15. onMounted(): A lifecycle hook that is called after the component has been mounted to the DOM. It is often used for performing actions that require the component to be present in the DOM, such as fetching data or manipulating the DOM elements.
16. useRoute(): A function provided by Vue Router to access the current route object, which contains information about the current route, such as path, params, query, etc. route.params, route.query etc.
17. useRouter(): A function provided by Vue Router to access the router instance, allowing programmatic navigation and route manipulation within components. router.push(), router.replace(), router.go() etc.

### 1. **Vue.js Fundamentals**

- ✅ Vue 3 project setup with Vite
- ✅ Single File Components (SFC) structure
- ✅ Template syntax and directives
- ✅ Component composition and organization

### 2. **Template Interpolation & Data Binding**

- ✅ **Text Interpolation** - [`TextInterpolation.vue`](Vue-Course/src/components/TextInterpolation.vue)
  - Mustache syntax `{{ }}`
  - Displaying dynamic data in templates
  - Basic event handling with `@click`

### 3. **Attribute Binding**

- ✅ **V-Bind Directive** - [`VBind.vue`](Vue-Course/src/components/VBind.vue)
  - Binding data to HTML attributes (`:src`, `:alt`, `:class`)
  - Conditional classes based on data
  - Dynamic attribute binding
- ✅ **Advanced Attribute Binding** - [`AttributeBinding.vue`](Vue-Course/src/components/AttributeBinding.vue)
  - Multiple binding syntaxes (`v-bind:` vs `:`)
  - Dynamic object binding
  - Boolean attribute binding

### 4. **Event Handling**

- ✅ **Basic Event Handling** - [`EventHandler.vue`](Vue-Course/src/components/EventHandler.vue)
  - Click events with `@click`
  - Method definitions and execution
  - State manipulation through events
- ✅ **Form Event Handling** - [`FormEventHandler.vue`](Vue-Course/src/components/FormEventHandler.vue)
  - Form submission with `@submit.prevent`
  - Two-way data binding with `v-model`
  - Form validation and user input handling

### 5. **Reactivity System**

- ✅ **Ref API** - [`RefComponent.vue`](Vue-Course/src/components/RefComponent.vue)
  - Creating reactive references with `ref()`
  - Working with primitive and complex data types
  - Updating reactive data (.value syntax)
  - Arrays and objects in refs
- ✅ **Reactive API** - [`ReactiveComponent.vue`](Vue-Course/src/components/ReactiveComponent.vue)
  - Creating reactive objects with `reactive()`
  - Nested object reactivity
  - Direct property manipulation

### 6. **List Rendering**

- ✅ **V-For Directive** - [`VFor.vue`](Vue-Course/src/components/VFor.vue)
  - Iterating over arrays
  - Using `:key` for list optimization
  - Accessing array items and properties
  - Template rendering for each item

### 7. **Conditional Rendering**

- ✅ **V-If/V-Else/V-Else-If** - [`VIf.vue`](Vue-Course/src/components/VIf.vue)
  - Conditional DOM rendering
  - Complex conditional logic
  - Loading states and user authentication flows
- ✅ **V-Show Directive** - [`VIf.vue`](Vue-Course/src/components/VIf.vue)
  - CSS-based visibility toggling
  - Performance considerations (v-if vs v-show)
  - Dynamic UI controls

### 8. **Computed Properties**

- ✅ **Computed Values** - [`VComputed.vue`](Vue-Course/src/components/VComputed.vue)
  - Reactive computed properties with `computed()`
  - Automatic dependency tracking
  - Performance optimization through caching
  - Derived state management

### 9. **Component Lifecycle**

- ✅ **OnMounted Hook** - [`OnMounted.vue`](Vue-Course/src/components/OnMounted.vue)
  - Component lifecycle management
  - API calls on component mount
  - Async data fetching
  - Loading states and error handling

### 10. **Component Architecture & Communication**

- ✅ **Props** - [`Balance.vue`](Expense-Tracker/src/components/Balance.vue), [`IncomeExpense.vue`](Expense-Tracker/src/components/IncomeExpense.vue)
  - Parent-to-child data passing
  - Prop validation and type checking
  - Required props and default values
- ✅ **Events (Emit)** - [`AddTransaction.vue`](Expense-Tracker/src/components/AddTransaction.vue), [`TransactionList.vue`](Expense-Tracker/src/components/TransactionList.vue)
  - Child-to-parent communication
  - Custom event emission with `defineEmits`
  - Event payload handling

### 11. V Directives Overview

![alt text](./assets/image.png)

### 12. Lifecycle Methods Overview

![alt text](./assets/image-1.png)

## 🎯 Practical Projects

### 1. **Vue Course Examples** - [`Vue-Course/`](Vue-Course/)

A comprehensive collection of Vue.js feature demonstrations covering all fundamental concepts.

### 2. **Expense Tracker Application** - [`Expense-Tracker/`](Expense-Tracker/)

A complete CRUD application featuring:

- Add/delete transactions
- Income and expense calculation
- Local storage persistence
- Toast notifications
- Component communication patterns

## 📝 Key Vue.js Concepts Mastered

1. **Composition API** - Modern Vue 3 approach
2. **Reactivity System** - Understanding Vue's reactive data
3. **Component Communication** - Props down, events up
4. **Template Directives** - v-if, v-for, v-model, v-bind
5. **Lifecycle Management** - Component mounting and cleanup
6. **State Management** - Local component state handling

---

_This learning journey demonstrates proficiency in Vue.js fundamentals and practical application development._
