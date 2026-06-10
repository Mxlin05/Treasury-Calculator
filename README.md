```markdown
# 📈 Treasury Calculator

A fast, client-side web application built with Svelte 5 to calculate and aggregate expected profits across multiple treasury investments. 

This project was built from the ground up using raw CSS and modern Svelte 5 architecture, demonstrating an understanding of component-based design, state management, and two-way data binding.

## ✨ Features

* **Dynamic Rows:** Add or remove individual treasury calculation rows on the fly.
* **Real-Time Calculation:** Profits are calculated instantly as the user types, blocking invalid keyboard inputs.
* **Aggregate Totals:** Uses Svelte 5 `$bindable` and `$derived` runes to lift state from child components and calculate a real-time Grand Total.
* **Responsive Styling:** Built entirely with raw CSS (Flexbox, custom button modifiers, and hover states) without relying on heavy external UI libraries.

## 🛠️ Tech Stack

* **Framework:** [Svelte 5](https://svelte.dev/) (SvelteKit)
* **Languages:** HTML, CSS, JavaScript
* **Environment:** Node.js

---

## 🚀 Installation & Setup

To get a local copy up and running, follow these simple steps.

### Prerequisites
Make sure you have Node.js and npm installed on your machine.
* [Download Node.js](https://nodejs.org/)

### Quick Start

1. **Clone the repository**
   ```bash
   git clone [https://github.com/](https://github.com/)[YOUR-USERNAME]/Treasury-Calculator.git

```

2. **Navigate into the project directory**
```bash
cd Treasury-Calculator

```


3. **Install the dependencies**
```bash
npm install

```


4. **Start the development server**
```bash
npm run dev

```


5. **Open the app**
Open your browser and navigate to `http://localhost:5173/` to see the calculator running!

---

## 📦 Building for Production

To create an optimized production build of the app, run:

```bash
npm run build

```

You can preview the built app with `npm run preview`, regardless of whether you installed an adapter. This should *not* be used to serve your app in production.

## 📝 License

Distributed under the MIT License.

```

### What to edit before you push:
* Make sure to swap out `[YOUR-USERNAME]` in the **Quick Start** section with your actual GitHub username so the clone link works perfectly for visitors!

```
