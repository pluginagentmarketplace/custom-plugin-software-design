---
name: frontend-frameworks
description: Modern frontend frameworks including React, Vue, Angular, and Next.js. Master component-based architecture, state management, and full-stack development. Use when building interactive web applications or learning modern frontend technologies.
---

# Frontend Frameworks

## Quick Start

Modern frontend frameworks enable building complex, interactive web applications with reusable components. The three major frameworks are:

- **React** - Component library by Meta, largest ecosystem
- **Vue** - Progressive framework, gentle learning curve
- **Angular** - Full-featured framework by Google, enterprise-focused

## React Fundamentals

React is a JavaScript library for building user interfaces with components:

```javascript
// Functional Component with Hooks
import { useState } from 'react';

function Counter() {
  const [count, setCount] = useState(0);

  return (
    <div>
      <p>Count: {count}</p>
      <button onClick={() => setCount(count + 1)}>Increment</button>
    </div>
  );
}

export default Counter;
```

### React Core Concepts

- **Components** - Reusable UI building blocks (functional or class)
- **JSX** - HTML-like syntax in JavaScript
- **Props** - Pass data to components (one-way flow)
- **State** - Component internal data that triggers re-renders
- **Hooks** - Functions to use state and other features (useState, useEffect, useContext)
- **Effects** - Side effects like API calls (useEffect hook)
- **Events** - Handle user interactions (onClick, onChange, etc.)

### State Management

```javascript
// Using Redux
import { createSlice, configureStore } from '@reduxjs/toolkit';
import { useDispatch, useSelector } from 'react-redux';

const counterSlice = createSlice({
  name: 'counter',
  initialState: { value: 0 },
  reducers: {
    increment: state => { state.value += 1; }
  }
});

const store = configureStore({
  reducer: { counter: counterSlice.reducer }
});

function App() {
  const dispatch = useDispatch();
  const count = useSelector(state => state.counter.value);

  return (
    <button onClick={() => dispatch(counterSlice.actions.increment())}>
      Count: {count}
    </button>
  );
}
```

### Advanced React Patterns

- **Render Props** - Share state between components via function props
- **Higher-Order Components (HOCs)** - Functions that enhance components
- **Custom Hooks** - Reusable stateful logic
- **Context API** - Share data across component tree (Redux alternative)
- **Error Boundaries** - Catch errors in component tree
- **Portals** - Render outside DOM hierarchy
- **Code Splitting** - Lazy load components for performance

## Vue Framework

Vue offers an approachable, progressive framework:

```vue
<template>
  <div>
    <p>Count: {{ count }}</p>
    <button @click="increment">Increment</button>
  </div>
</template>

<script setup>
import { ref } from 'vue';

const count = ref(0);
const increment = () => { count.value++; };
</script>

<style scoped>
button { padding: 10px; cursor: pointer; }
</style>
```

### Vue Ecosystem

- **Composition API** - Modern reactive programming (similar to hooks)
- **Vue Router** - Official routing library
- **Pinia** - State management (Vuex replacement)
- **Nuxt** - Meta-framework for full-stack Vue development
- **Single File Components (SFC)** - Template, script, styles in one file

## Angular Framework

Angular is a complete framework with built-in tools:

```typescript
// Component with Services and RxJS
import { Component, OnInit } from '@angular/core';
import { UserService } from './user.service';

@Component({
  selector: 'app-user',
  template: `
    <div>
      <p>{{ user.name }}</p>
      <button (click)="logout()">Logout</button>
    </div>
  `
})
export class UserComponent implements OnInit {
  user: any;

  constructor(private userService: UserService) {}

  ngOnInit() {
    this.userService.getUser().subscribe(data => {
      this.user = data;
    });
  }

  logout() {
    this.userService.logout();
  }
}
```

### Angular Features

- **TypeScript-first** - Strong typing built-in
- **Dependency Injection** - Powerful IoC container
- **RxJS** - Reactive programming with Observables
- **Angular CLI** - Professional development tools
- **Angular Material** - UI component library
- **NgRx** - State management for complex apps

## Next.js Meta-Framework

Next.js extends React with server-side capabilities:

```javascript
// pages/blog/[slug].js - Dynamic routes
export default function BlogPost({ post }) {
  return (
    <article>
      <h1>{post.title}</h1>
      <p>{post.content}</p>
    </article>
  );
}

export async function getStaticProps({ params }) {
  const post = await fetch(`/api/posts/${params.slug}`);
  return {
    props: { post: await post.json() },
    revalidate: 60 // ISR: revalidate every 60 seconds
  };
}

export async function getStaticPaths() {
  const posts = await fetch('/api/posts');
  const paths = (await posts.json()).map(p => ({
    params: { slug: p.slug }
  }));
  return { paths, fallback: 'blocking' };
}
```

### Next.js Capabilities

- **Server-Side Rendering (SSR)** - Render pages on server
- **Static Site Generation (SSG)** - Pre-build pages at build time
- **Incremental Static Regeneration (ISR)** - Update static pages without rebuild
- **API Routes** - Build serverless API endpoints
- **Image Optimization** - Automatic image optimization
- **CSS Support** - Built-in CSS modules and styled-jsx
- **Deployment** - Vercel platform integration

## Styling Approaches

### CSS Modules
```css
/* Button.module.css */
.button {
  padding: 10px 20px;
  background: blue;
  color: white;
  border: none;
}
```

```javascript
import styles from './Button.module.css';

export function Button() {
  return <button className={styles.button}>Click me</button>;
}
```

### Tailwind CSS
```javascript
export function Button() {
  return (
    <button className="px-5 py-2 bg-blue-500 text-white rounded hover:bg-blue-600">
      Click me
    </button>
  );
}
```

### Styled Components
```javascript
import styled from 'styled-components';

const StyledButton = styled.button`
  padding: 10px 20px;
  background: blue;
  color: white;
  border: none;

  &:hover {
    background: darkblue;
  }
`;

export function Button() {
  return <StyledButton>Click me</StyledButton>;
}
```

## Testing Frameworks

```javascript
// Jest + React Testing Library
import { render, screen, fireEvent } from '@testing-library/react';
import Counter from './Counter';

test('increments counter on button click', () => {
  render(<Counter />);
  const button = screen.getByRole('button', { name: /increment/i });

  fireEvent.click(button);

  expect(screen.getByText(/Count: 1/)).toBeInTheDocument();
});
```

## Framework Comparison

| Aspect | React | Vue | Angular | Next.js |
|--------|-------|-----|---------|---------|
| Learning Curve | Medium | Easy | Hard | Medium |
| Ecosystem | Huge | Good | Built-in | Excellent |
| Performance | Excellent | Excellent | Good | Excellent |
| Typing | Optional (TS) | Optional | Required (TS) | Supported |
| SSR Support | Next.js | Nuxt | Limited | Built-in |
| Company | Meta | Community | Google | Vercel |
| Bundle Size | Medium | Small | Large | Small |
| Job Market | Very High | Medium | High | Growing |

## Best Practices

- **Component Composition** - Build with small, focused components
- **Props Over Inheritance** - Favor composition patterns
- **State Immutability** - Never mutate state directly
- **Lazy Loading** - Code split and lazy load components
- **Memoization** - Prevent unnecessary re-renders (React.memo, useMemo)
- **Error Handling** - Use error boundaries and try-catch
- **Testing** - Write unit and integration tests
- **Accessibility** - Use semantic HTML, ARIA attributes
- **Performance Monitoring** - Use React Profiler, Lighthouse
- **TypeScript** - Add type safety to catch errors early

## Resources

- [React Official Docs](https://react.dev)
- [Vue Official Docs](https://vuejs.org)
- [Angular Documentation](https://angular.io)
- [Next.js Documentation](https://nextjs.org/docs)
- [Egghead.io React Courses](https://egghead.io)
- [Frontend Masters](https://frontendmasters.com)

## Related Skills

- **JavaScript/TypeScript** - Language fundamentals
- **CSS & Styling** - Layout and styling
- **Web Performance** - Optimization techniques
- **Testing** - Jest, React Testing Library
- **State Management** - Redux, Zustand, Pinia
