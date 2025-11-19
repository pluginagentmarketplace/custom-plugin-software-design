---
name: web-fundamentals
description: HTML, CSS, JavaScript, and TypeScript fundamentals. Master semantic HTML, modern CSS layouts, ES6+ JavaScript, and type-safe development. Essential foundation for all web development roles.
---

# Web Fundamentals

## Quick Start

Web fundamentals are the foundation for all web development. Master HTML structure, CSS styling, JavaScript interactivity, and TypeScript type safety.

### HTML5 Essentials

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <meta name="description" content="Page description">
  <title>My Website</title>
  <link rel="stylesheet" href="styles.css">
</head>
<body>
  <!-- Semantic HTML -->
  <header>
    <nav>
      <ul>
        <li><a href="/">Home</a></li>
        <li><a href="/about">About</a></li>
      </ul>
    </nav>
  </header>

  <main>
    <article>
      <h1>Article Title</h1>
      <time datetime="2024-01-15">January 15, 2024</time>
      <p>Article content...</p>
    </article>

    <aside>
      <h2>Related Links</h2>
      <ul>
        <li><a href="#">Link 1</a></li>
      </ul>
    </aside>
  </main>

  <footer>
    <p>&copy; 2024 My Website</p>
  </footer>

  <script src="script.js"></script>
</body>
</html>
```

### CSS3 Modern Layouts

```css
/* Flexbox - 1D Layout */
.flex-container {
  display: flex;
  justify-content: space-between;
  align-items: center;
  gap: 20px;
}

/* CSS Grid - 2D Layout */
.grid-container {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 20px;
}

/* Responsive Design */
@media (max-width: 768px) {
  .grid-container {
    grid-template-columns: 1fr;
  }
}

/* Modern Selectors & Features */
:root {
  --primary-color: #3498db;
  --spacing-unit: 8px;
}

.card {
  color: var(--primary-color);
  padding: calc(var(--spacing-unit) * 2);
  border-radius: 8px;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.1);
}
```

### JavaScript ES6+ Fundamentals

```javascript
// Variables and Types
const name = 'John';  // String
let age = 30;         // Number
var isActive = true;  // Boolean (avoid var - use let/const)

// Template Literals
const greeting = `Hello, ${name}! You are ${age} years old.`;

// Arrow Functions
const add = (a, b) => a + b;
const greet = () => `Hello!`;

// Destructuring
const { firstName, lastName } = person;
const [first, second] = array;

// Spread Operator
const combined = { ...obj1, ...obj2 };
const merged = [...arr1, ...arr2];

// Async/Await
async function fetchData(url) {
  try {
    const response = await fetch(url);
    const data = await response.json();
    return data;
  } catch (error) {
    console.error('Fetch failed:', error);
  }
}

// Promise Basics
fetch('/api/data')
  .then(res => res.json())
  .then(data => console.log(data))
  .catch(error => console.error(error));

// Array Methods
const numbers = [1, 2, 3, 4, 5];
const doubled = numbers.map(n => n * 2);
const evens = numbers.filter(n => n % 2 === 0);
const sum = numbers.reduce((acc, n) => acc + n, 0);

// Classes
class Person {
  constructor(name, age) {
    this.name = name;
    this.age = age;
  }

  greet() {
    return `Hi, I'm ${this.name}`;
  }
}

// Modules
export const myFunction = () => {};
export default MyClass;

import MyClass, { myFunction } from './module.js';
```

### TypeScript Type Safety

```typescript
// Basic Types
const name: string = 'John';
const age: number = 30;
const isActive: boolean = true;
const items: string[] = ['a', 'b'];
const data: any = {}; // Avoid any

// Union Types
type Status = 'active' | 'inactive' | 'pending';
const status: Status = 'active';

// Interfaces
interface User {
  id: number;
  name: string;
  email?: string;  // Optional property
  readonly createdAt: Date;  // Read-only
}

// Functions
function greet(name: string): string {
  return `Hello, ${name}`;
}

const add = (a: number, b: number): number => a + b;

// Generics
function identity<T>(value: T): T {
  return value;
}

interface Container<T> {
  value: T;
  getValue: () => T;
}

// Type Aliases vs Interfaces
type Point = { x: number; y: number };
interface Position { x: number; y: number; }

// Classes with TypeScript
class User {
  readonly id: string;
  private password: string;
  public name: string;

  constructor(name: string, password: string) {
    this.id = Math.random().toString();
    this.name = name;
    this.password = password;
  }

  private hashPassword(): string {
    // Implementation
    return '';
  }
}

// Enums
enum Color {
  Red = '#FF0000',
  Green = '#00FF00',
  Blue = '#0000FF'
}

// Advanced Types
type Admin = User & { permissions: string[] };
type Result<T> = { success: true; data: T } | { success: false; error: string };
```

## DOM Manipulation

```javascript
// Selecting Elements
const element = document.getElementById('myId');
const elements = document.querySelectorAll('.my-class');
const first = document.querySelector('div > p');

// Creating Elements
const div = document.createElement('div');
div.textContent = 'Hello';
div.className = 'my-class';
div.setAttribute('data-id', '123');

// Adding to DOM
document.body.appendChild(div);
parent.insertBefore(div, existing);

// Event Handling
element.addEventListener('click', (e) => {
  console.log('Clicked!');
  e.preventDefault();
});

// Event Delegation
document.addEventListener('click', (e) => {
  if (e.target.matches('.button')) {
    // Button clicked
  }
});

// Styling
element.style.color = 'red';
element.classList.add('active');
element.classList.remove('disabled');
element.classList.toggle('selected');
```

## Web APIs

```javascript
// Fetch API
const response = await fetch('https://api.example.com/data', {
  method: 'GET',
  headers: { 'Content-Type': 'application/json' },
  body: JSON.stringify({ key: 'value' })
});
const data = await response.json();

// LocalStorage
localStorage.setItem('user', JSON.stringify({ name: 'John' }));
const user = JSON.parse(localStorage.getItem('user'));

// Geolocation
navigator.geolocation.getCurrentPosition((position) => {
  console.log(position.coords.latitude);
});

// Notifications
Notification.requestPermission().then((permission) => {
  if (permission === 'granted') {
    new Notification('Hello!');
  }
});

// Web Workers
const worker = new Worker('worker.js');
worker.postMessage({ task: 'compute' });
worker.onmessage = (e) => console.log(e.data);
```

## Accessibility (a11y)

```html
<!-- Semantic HTML -->
<button>Click me</button> <!-- Not <div onclick> -->
<label for="input">Name:</label>
<input id="input" type="text">

<!-- ARIA -->
<div role="navigation" aria-label="Main navigation">
  <ul>
    <li><a href="/">Home</a></li>
  </ul>
</div>

<!-- Alt Text -->
<img src="photo.jpg" alt="Description of image">

<!-- Keyboard Navigation -->
<nav>
  <ul>
    <li><a href="/">Home</a></li>
    <li><a href="/about">About</a></li>
  </ul>
</nav>
```

## Performance Best Practices

- Use semantic HTML for SEO and accessibility
- Minimize HTTP requests and bundle sizes
- Use CSS Grid and Flexbox for modern layouts
- Optimize images with modern formats (WebP)
- Implement code splitting for JavaScript
- Use CSS variables for maintainability
- Prefer CSS over JavaScript for animations
- Lazy load images and components
- Use async/defer for script loading

## Resources

- [MDN Web Docs](https://developer.mozilla.org)
- [HTML Living Standard](https://html.spec.whatwg.org)
- [CSS-Tricks](https://css-tricks.com)
- [JavaScript.info](https://javascript.info)
- [TypeScript Official Docs](https://www.typescriptlang.org)

## Related Skills

- **React/Vue/Angular** - Framework implementation
- **Testing** - Jest, React Testing Library
- **Performance** - Optimization techniques
- **Accessibility** - WCAG compliance
