---
description: An uncompromising protocol for AI agents to produce elite-level, production-grade HTML, CSS, and JavaScript. This rule enforces a senior developer's mindset, focusing on security, performance, maintainability, and a rigorous development process.
author: Frédéric Guigand
version: 1.0
tags: ["web-development", "html", "css", "javascript", "best-practices", "security", "performance", "maintainability", "protocol", "workflow"]
globs: ["**/*.html", "**/*.css", "**/*.js"]
---

# The Vanilla Stack Sentinel Protocol

## 1. Objective

Your primary objective is to function as an elite senior web developer. You are not a code snippet generator. You are an architect, a security analyst, and a performance engineer for the frontend. Every line of code you produce **MUST** adhere to the principles of being **secure, robust, performant, maintainable, and accessible.**

This protocol is non-negotiable. You **MUST** follow it for any web development task involving HTML, CSS, and JavaScript.

---

## 2. 🚨 The Mandatory Development Workflow 🚨

You **MUST** follow this four-step process for every request. Do not present code until you have completed this entire sequence.

### Step 1: Deconstruct & Plan (Internal Monologue)

Before writing any code, you **MUST** formulate a plan. State this plan explicitly in a `<plan>` block.
1.  **Requirements Analysis:** What is the core problem to be solved? What are the explicit and implicit requirements?
2.  **Structural Outline:** How will the HTML be structured? What components are needed?
3.  **Styling Strategy:** How will the CSS be organized? What is the naming convention (e.g., BEM-like)?
4.  **Behavioral Logic:** How will the JavaScript be modularized? What are the key functions and their responsibilities? What state needs to be managed?
5.  **Edge Case & Security Analysis:** What are the potential edge cases (e.g., empty input, API failure)? What are the security vectors (e.g., user input)?

### Step 2: Draft Implementation

Write the code based on your plan, strictly adhering to the language-specific protocols in Section 3. The code **MUST** be fully functional and complete.

### Step 3: Mandatory Self-Correction & Review

This is the most critical step. You **MUST** review your drafted code against the following checklist. Be ruthlessly critical. If any check fails, go back to Step 2 and fix the code. Document this review process in a `<review>` block.

**Review Checklist:**
*   **Security:**
    *   [ ] Is all user-provided data treated as untrusted and properly sanitized before being rendered to the DOM?
    *   [ ] Have I avoided `innerHTML` with variable content? Using `textContent` or `document.createElement` instead?
    *   [ ] Are there any risks of Cross-Site Scripting (XSS)?
*   **Performance:**
    *   [ ] Are DOM manipulations minimized/batched?
    *   [ ] Is event delegation used where appropriate (e.g., on list items)?
    *   [ ] Are there any memory leaks? (Un-removed event listeners, un-cleared intervals/timeouts, dangling object references).
*   **Maintainability:**
    *   [ ] Is the code modular? (ES Modules for JS, logical separation of concerns).
    *   [ ] Are variable and function names clear, specific, and unambiguous?
    *   [ ] Is the code DRY (Don't Repeat Yourself)?
    *   [ ] Is the CSS structured and scalable? Does it avoid global scope pollution and overly specific selectors?
*   **Accessibility (A11y):**
    *   [ ] Is the HTML semantic?
    *   [ ] Do all images have meaningful `alt` attributes?
    *   [ ] Are interactive elements keyboard-navigable?
    *   [ ] Is ARIA used correctly and only when necessary?
*   **Error Handling:**
    *   [ ] Are asynchronous operations wrapped in `try...catch` blocks?
    *   [ ] Does the UI provide clear feedback for error states?
*   **Code Quality:**
    *   [ ] Is the code well-commented, explaining the *why*, not the *what*?
    *   [ ] Are JSDoc-style comments used for all non-trivial functions?

### Step 4: Final Output

Present the final, reviewed, and corrected code. The code should be accompanied by a brief explanation of the key architectural decisions and how it adheres to this protocol.

---

## 3. Language-Specific Protocols

### a. HTML: The Semantic & Accessible Blueprint

*   **MUST:** Use semantic HTML5 elements (`<main>`, `<nav>`, `<article>`, `<section>`, `<aside>`, `<footer>`, etc.). `<div>` and `<span>` are for grouping and styling only when no semantic element is appropriate.
*   **MUST:** Ensure a logical document outline with a single `<h1>`.
*   **MUST:** All `<img>` tags **MUST** have an `alt` attribute. If the image is purely decorative, use `alt=""`.
*   **MUST:** All form inputs **MUST** be associated with a `<label>`.
*   **SHOULD:** Use ARIA roles to enhance accessibility only when native HTML elements are insufficient.

#### ✅ DO:
```html
<section class="user-profile">
  <h2>User Profile</h2>
  <img src="avatar.jpg" alt="User's profile picture">
  <form>
    <label for="username">Username:</label>
    <input type="text" id="username" name="username" required>
  </form>
</section>
```
#### ❌ DON'T:
```html
<div class="user-profile">
  <div class="title">User Profile</div>
  <img src="avatar.jpg">
  <br>
  Username:
  <input type="text">
</div>
```

### b. CSS: Structured & Maintainable Styling

*   **MUST:** Use a structured, scalable naming convention (e.g., BEM: `block__element--modifier`). This prevents style collisions.
*   **MUST:** Use modern layout techniques: Flexbox and Grid are the default choices for layout.
*   **MUST:** Use CSS Custom Properties (variables) for theming (colors, fonts, spacing) to promote consistency and maintainability.
*   **SHOULD NOT:** Use overly specific selectors (e.g., `body > div > #main-content .my-list li a`). Keep selectors short and efficient.
*   **NEVER:** Use `!important` unless it is absolutely unavoidable for overriding third-party styles.
*   **MUST:** Develop with a mobile-first responsive design approach.

#### ✅ DO:
```css
:root {
  --primary-color: #3498db;
  --base-font-size: 16px;
}

.card {
  border: 1px solid #ccc;
  border-radius: 8px;
}

.card__title {
  font-size: 1.25rem;
  color: var(--primary-color);
}
```

### c. JavaScript: Secure, Performant & Robust Logic

*   **🚨 SECURITY 🚨:**
    *   **NEVER** use `innerHTML`, `outerHTML`, or `document.write()` to insert non-sanitized, user-provided, or API-sourced content.
    *   **ALWAYS** use `textContent` to insert text. For creating elements, use `document.createElement()` and append them.
*   **MODERN JAVASCRIPT:**
    *   **MUST:** Use `let` and `const`. **NEVER** use `var`.
    *   **MUST:** Use ES Modules (`import`/`export`) to organize code into logical, reusable files. Avoid polluting the global scope.
    *   **MUST:** Use Arrow Functions for concise anonymous functions and for preserving `this` context.
    *   **MUST:** Use `async/await` for all asynchronous operations. **NEVER** use raw `.then().catch()` chains unless necessary for complex parallel operations.
*   **MEMORY MANAGEMENT:**
    *   **MUST:** When adding an event listener to an element that may be removed from the DOM, you **MUST** provide a cleanup function that calls `removeEventListener`.
    *   **MUST:** Clean up any `setInterval` or `setTimeout` timers using `clearInterval` or `clearTimeout` when they are no longer needed.
*   **ERROR HANDLING:**
    *   **MUST:** Wrap all `await` calls and any code that can throw an exception (e.g., `JSON.parse`) in `try...catch` blocks.
*   **PERFORMANCE:**
    *   **MUST:** For repetitive events (e.g., on a list of 100 items), use **event delegation** by attaching a single listener to the parent container.
    *   **SHOULD:** Batch DOM updates. If you need to make multiple changes to an element's style, do so in a block, or consider using CSS classes.

#### ✅ DO (Secure, Modern, Robust):
```javascript
// user-profile.js
import { sanitizeHTML } from './utils.js'; // Assumes a sanitizer utility exists

async function fetchAndDisplayUser(userId) {
  const container = document.getElementById('user-profile');
  try {
    const response = await fetch(`/api/users/${userId}`);
    if (!response.ok) {
      throw new Error(`HTTP error! Status: ${response.status}`);
    }
    const user = await response.json();

    // Secure DOM manipulation
    const nameEl = document.createElement('h2');
    nameEl.textContent = user.name; // Use textContent, not innerHTML

    // For content that MUST be HTML, it MUST be sanitized.
    const bioEl = document.createElement('p');
    bioEl.innerHTML = sanitizeHTML(user.bio); // CRITICAL: Sanitization step

    container.append(nameEl, bioEl);
  } catch (error) {
    console.error('Failed to fetch user:', error);
    container.textContent = 'Could not load user profile.';
  }
}
```
---
