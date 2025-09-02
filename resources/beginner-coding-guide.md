# Beginner's Guide to Coding & Web Development

This guide provides a starting point for individuals new to coding, web development, and bioinformatics. It covers fundamental concepts, tools, and best practices to help you build a strong foundation.

## 1. Version Control with Git & GitHub

Version control is like a "save" button for your entire project, but much more powerful. It allows you to track every change, revert to previous versions, and collaborate with others without overwriting their work.

### Core Concepts

-   **Repository (Repo):** A folder containing your project and its entire history of changes. Your `Lab-Placement-B` directory is a Git repository.
-   **Project:** The work you are doing within the repository.
-   **Staging:** The "waiting room" for your changes. Before you save a version of your project, you must first add the files you've modified to the staging area. This lets you choose which changes to include in the next save.
-   **Committing:** The act of saving your staged changes to the repository's history. Each commit is a snapshot of your project at a specific point in time and includes a message describing the changes.
-   **Branch:** A parallel version of your repository. You can create branches to work on new features without affecting the main version of your project (often called the `main` or `master` branch).
-   **Pull Request (PR):** A request to merge the changes from your branch into another branch. This is a core part of collaboration, as it allows others to review your changes before they are integrated.
-   **Issues:** A feature on platforms like GitHub for tracking tasks, bugs, and feature requests. It's a to-do list for your project. You can link commits to issues to automatically track progress.

## 2. Understanding Your Development Environment

Your setup involves several key components that work together:

-   **Visual Studio Code (VS Code):** A powerful and popular code editor. It's highly extensible, meaning you can add tools (extensions) for different languages and workflows.
-   **Windows Subsystem for Linux (WSL) with Ubuntu:** This allows you to run a Linux environment directly on Windows. You'll use its terminal for most of your command-line work, as it's the standard for many development and scientific computing tasks.
-   **Git:** A version control system for tracking changes in your code.
-   **GitHub:** A web-based platform for hosting Git repositories, collaborating with others, and managing projects.

## 3. Coding & Naming Conventions

Following consistent conventions makes your code readable, maintainable, and easier for others (and your future self) to understand.

### a. File Naming

Different projects use different conventions. It's important to look at the existing files and stay consistent. Here are some common ones:

-   **`kebab-case`:** All lowercase, with words separated by hyphens. This is very common for web-related files (HTML, CSS, JS) and is the convention you are using.
    -   *Example:* `beginner-coding-guide.md`, `distance-calculator.js`
-   **`snake_case`:** All lowercase, with words separated by underscores. Common in Python and some other languages.
    -   *Example:* `main_script.py`, `data_processing.py`
-   **`PascalCase`:** Words are capitalized and joined together. Often used for class names in object-oriented programming.
    -   *Example:* `DistanceCalculator`, `RepresentationManager`
-   **`camelCase`:** The first word is lowercase, and subsequent words are capitalized. Commonly used for variable and function names in JavaScript.
    -   *Example:* `calculateDistance`, `userName`

### b. Commit Messages

A good commit message explains *why* a change was made. A common format is:

```
<type>: <subject>

[optional body]

[optional footer]
```

-   **Type:** What kind of change is this?
    -   `feat`: A new feature.
    -   `fix`: A bug fix.
    -   `docs`: Changes to documentation.
    -   `style`: Formatting changes, no code logic change.
    -   `refactor`: Restructuring code without changing its behavior.
    -   `test`: Adding or improving tests.
-   **Subject:** A short, imperative summary of the change (e.g., "Add distance calculation feature," not "Added feature").
-   **Body (Optional):** A more detailed explanation of the changes.
-   **Footer (Optional):** Used for referencing issue numbers (e.g., `Closes #42`).

**Example Commit Message:**

```
feat: Add multiple protein display options

Implement six different molecular representations (Cartoon, Surface, etc.)
to allow for more flexible visualization of the HNF1B protein structure.

This is controlled by a new RepresentationManager class.

Closes #12
```

## 4. Code Quality: Linting

As you noted, **linting** is the process of using an automated tool (a "linter") to check your code for stylistic and programmatic errors.

-   **Why it's important:**
    -   **Enforces Consistency:** Ensures everyone on a project follows the same style guide.
    -   **Catches Errors:** Finds potential bugs like using an undefined variable before they cause problems.
    -   **Improves Readability:** Clean, consistent code is easier to read and understand.

-   **Popular Linters:**
    -   **JavaScript/TypeScript:** ESLint
    -   **Python:** Ruff, Flake8, Pylint
    -   **General:** Prettier (for formatting)

You can install these as extensions in VS Code, and they will highlight problems directly in your editor.

## 5. Interacting with Large Language Models (LLMs)

LLMs are powerful AI tools that can assist in writing code, debugging, and learning. Here are the primary ways you'll interact with them:

### a. Web Browser (Copy-Paste Method)

-   **How it works:** You open an LLM chat interface (like Gemini, Claude, or ChatGPT) in your web browser, write a prompt, and copy-paste the generated code into your editor.
-   **Pros:** Simple, accessible from anywhere, and allows you to refine your prompt easily.
-   **Cons:** Can be slow, requires switching between windows, and the model lacks direct context of your project. You must provide all relevant code snippets and file information manually.

### b. Editor Extensions (e.g., GitHub Copilot)

-   **How it works:** An extension integrated directly into VS Code. It provides real-time code suggestions, autocompletes entire functions, and can answer questions within the editor.
-   **Pros:** Highly efficient, has context of your open files, and speeds up development significantly.
-   **Cons:** Usually a paid service (though often free for students).

### c. Terminal-Based Access (e.g., Gemini CLI)

-   **How it works:** You interact with an LLM directly from your terminal. This is a very powerful method as the LLM can read your files, understand your project structure, and even execute commands.
-   **Pros:** The most powerful and context-aware method. It can perform complex tasks like refactoring code across multiple files, running tests, and managing your repository.
-   **Cons:** Requires learning specific commands and a different way of interacting with the AI.

## 6. Key Concepts for a Bioinformatics Web Project

Your project combines web technology with bioinformatics. Here are some core concepts that tie everything together.

### a. Basic Web Project Structure

A clean folder structure is essential for a maintainable project. As you've noted, it's better to use subfiles rather than one large file. A typical structure looks like this:

-   `/index.html`: The main entry point of your website.
-   `/css/`: A folder to hold your styling files (e.g., `style.css`).
-   `/js/`: A folder for your JavaScript files (e.g., `protein-viewer.js`, `data-handler.js`).
-   `/data/`: A folder for your data files (e.g., `variants.json`, `1ABC.pdb`).

### b. The Trio of Web Technologies

A website is built using three core languages that work together:

-   **HTML (HyperText Markup Language):** Provides the fundamental **structure** and content of the page (e.g., headings, paragraphs, buttons).
-   **CSS (Cascading Style Sheets):** Controls the **presentation** and styling (e.g., colors, fonts, layout).
-   **JavaScript (JS):** Enables **interactivity** and dynamic behavior (e.g., loading a protein viewer, handling user clicks, filtering data).

### c. JavaScript Libraries

You don't have to write everything from scratch. A **library** is a collection of pre-written code that provides common functionality.

-   **Example:** For this project, you are using `NGL.js` (or a library based on it). This library provides all the complex logic for parsing PDB files and rendering interactive 3D protein structures in the browser. You simply need to learn how to use the library's functions.

### d. Common Data Formats

-   **PDB (`.pdb`):** The standard format for a Protein Data Bank file, which contains the 3D coordinates of atoms in a protein or nucleic acid. This is what `NGL.js` loads to display a structure.
-   **JSON (`.json`):** A lightweight, human-readable format for data exchange. It's perfect for storing structured data like your list of HNF1B variants and their associated phenotypes.
-   **CSV (`.csv`):** Comma-Separated Values. A simple text file where data is organized in a table, with columns separated by commas. It's another common way to store variant data.

### e. Debugging in the Browser

When your JavaScript code doesn't work as expected, the first place to look is your browser's **Developer Tools**.

-   **How to open:** Right-click anywhere on your webpage and select "Inspect," or press `F12`.
-   **The Console Tab:** Click on the "Console" tab. This is where JavaScript errors, warnings, and messages you log yourself (using `console.log()`) will appear. It is an essential tool for finding and fixing problems in your code.

