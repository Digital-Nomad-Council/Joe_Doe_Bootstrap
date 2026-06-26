# Guide: Adapting an Existing HTML Project to Bootstrap 5

This guide explains how to migrate a raw HTML/CSS project (such as Version 1 or 2) into a responsive Bootstrap 5 template structure, using **Version 3** of the Joe Doe CV project as a case study.

---

## Step 1: Install and Reference Bootstrap

To integrate Bootstrap into your project, you can either link the files from a CDN or manage them locally using a package manager like NPM.

### A. NPM Installation (Recommended for Production)
Initialize an npm project and install Bootstrap:
```bash
npm init -y
npm install bootstrap
```
Ignore `node_modules/` in your git configuration (`.gitignore`) and copy the required assets to your project's local directories:
* Copy `node_modules/bootstrap/dist/css/bootstrap.css` to `css/bootstrap.css`
* Copy `node_modules/bootstrap/dist/js/bootstrap.bundle.js` to `js/bootstrap.bundle.js`

### B. CDN Integration (Recommended for Prototyping)
Simply add the remote stylesheet link in the `<head>` of your pages.

---

## Step 2: Configure HTML Header and Viewports

Bootstrap is built mobile-first. Ensure the responsive viewport meta tag is added to the `<head>` of every HTML page.

```html
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Joe Doe - CV</title>
    
    <!-- 1. Load Bootstrap CSS first -->
    <link rel="stylesheet" href="css/bootstrap.css">
    
    <!-- 2. Load Custom overrides stylesheet second -->
    <link rel="stylesheet" href="css/style.css">
</head>
```

---

## Step 3: Implement the Grid System and Layouts

Bootstrap structures layout using three main building blocks: **Containers**, **Rows**, and **Columns**.

1. **Containers (`.container`)**: Centers your content and adds horizontal padding.
2. **Rows (`.row`)**: Acts as a flexbox wrapper for columns. Use gutter utilities (like `.g-5`) to control grid spacing.
3. **Columns (`.col-*`)**: Defines the width of elements. Bootstrap uses a 12-column grid. Column parameters can scale dynamically based on screen size (e.g., `col-lg-8` and `col-lg-4` for a two-column desktop grid that collapses into stacked blocks on mobile).

### Example: Story & Skills Layout
```html
<main class="container py-5">
    <div class="row g-5">
        <!-- Story (Takes up 8 columns on large screens, full width on mobile) -->
        <div class="col-lg-8">
            <section class="bg-white p-4 rounded-4 shadow-sm">
                <h2>About Me</h2>
                <p>Content goes here...</p>
            </section>
        </div>
        
        <!-- Skills & Education (Takes up 4 columns on large screens, full width on mobile) -->
        <div class="col-lg-4">
            <section class="bg-white p-4 rounded-4 shadow-sm">
                <h2>Skills</h2>
                <!-- Badges -->
                <span class="badge bg-primary">HTML5</span>
            </section>
        </div>
    </div>
</main>
```

---

## Step 4: Adapt Components to Bootstrap Classes

Replace custom CSS styling with Bootstrap's native UI utility classes:

### 1. Navigation Bar
Convert standard lists into a responsive collapsing navigation bar:
```html
<nav class="navbar navbar-expand-lg navbar-dark bg-dark sticky-top shadow-sm">
    <div class="container">
        <a class="navbar-brand fw-bold text-uppercase" href="index.html">Joe Doe</a>
        <button class="navbar-toggler" type="button" data-bs-toggle="collapse" data-bs-target="#navbarNav">
            <span class="navbar-toggler-icon"></span>
        </button>
        <div class="collapse navbar-collapse" id="navbarNav">
            <ul class="navbar-nav ms-auto">
                <li class="nav-item"><a class="nav-link active" href="index.html">Home</a></li>
                <li class="nav-item"><a class="nav-link" href="about.html">About</a></li>
            </ul>
        </div>
    </div>
</nav>
```

### 2. Cards
Replace custom card boxes with `.card` classes:
```html
<section class="card border-0 rounded-4 shadow-sm overflow-hidden">
    <div class="card-header bg-dark text-white py-3">
        <h2 class="h5 fw-bold mb-0">Education</h2>
    </div>
    <div class="card-body">
        <h3 class="h6 fw-bold">BSc Computer Science</h3>
        <p class="text-secondary small mb-0">Graduated: 2024</p>
    </div>
</section>
```

### 3. Tables
Wrap tables with a `.table-responsive` block to prevent layout breaking on mobile devices, and style them using hover and striped classes:
```html
<div class="table-responsive">
    <table class="table table-hover table-striped mb-0 align-middle">
        <thead class="table-light">
            <tr>
                <th>Role</th>
                <th>Company</th>
                <th class="text-end">Year</th>
            </tr>
        </thead>
        <tbody>
            <tr>
                <td class="fw-semibold">Developer</td>
                <td>Globex</td>
                <td class="text-end text-primary">2024</td>
            </tr>
        </tbody>
    </table>
</div>
```

### 4. Interactive Forms
Use `.form-control` for inputs, `.form-label` for labels, and spacing utilities like `.mb-3` to lay out clean forms:
```html
<form>
    <div class="mb-3">
        <label for="nameInput" class="form-label">Name</label>
        <input type="text" class="form-control" id="nameInput" required>
    </div>
    <button type="submit" class="btn btn-primary w-100 py-2.5">Send</button>
</form>
```

---

## Step 5: Add JavaScript Bootstrap Bundle

To ensure that interactive elements (like the collapsible responsive mobile menu) function correctly, load the Bootstrap bundle JS file at the very bottom of the `<body>` element on every page.

```html
    <!-- Bootstrap 5 Bundle JS (Includes Popper.js) -->
    <script src="js/bootstrap.bundle.js"></script>
</body>
</html>
```
