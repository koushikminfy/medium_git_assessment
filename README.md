Great! Here's a breakdown of **Assignment 4: Git Hooks & Automation**, including what each task involves and why it matters:

---

## 🎯 **Objective:**

Learn to improve **code quality and consistency** through **Git hooks** and basic **CI (Continuous Integration)** using **automation tools**.

---

## ✅ **Tasks Explained:**

### 1. **Set up a repository with Husky and lint-staged**

* **What is Husky?**
  Husky lets you run scripts at different stages of the Git lifecycle (e.g., before a commit or push). It's great for enforcing rules automatically.
* **What is lint-staged?**
  Runs linters (like ESLint) only on files that are staged for commit. This saves time and keeps your commits clean.

> You'll install these with npm/yarn in a JavaScript project:

```bash
npm install husky lint-staged --save-dev
```

Then set up Husky hooks:

```bash
npx husky install
```

Add it to your `package.json` scripts:

```json
"scripts": {
  "prepare": "husky install"
}
```

---

### 2. **Configure pre-commit hooks for:**

* **Code linting** using ESLint (or a language-specific linter like Flake8 for Python)
* **Code formatting** using Prettier
* **Commit message validation** using commitlint + Husky

#### Example Husky setup for pre-commit:

```bash
npx husky add .husky/pre-commit "npx lint-staged"
```

#### `lint-staged` config (in `package.json`):

```json
"lint-staged": {
  "*.js": ["eslint --fix", "prettier --write"]
}
```

#### Commit message validation:

* Install:

  ```bash
  npm install --save-dev @commitlint/{config-conventional,cli}
  ```
* Create `commitlint.config.js`:

  ```js
  module.exports = { extends: ['@commitlint/config-conventional'] };
  ```
* Add Husky commit-msg hook:

  ```bash
  npx husky add .husky/commit-msg 'npx commitlint --edit "$1"'
  ```

---

### 3. **Attempt commits that fail:**

* Commit code that violates linter rules
* Commit badly formatted code
* Use a bad commit message like “update”

All of these should be **rejected** by the respective hook.

---

### 4. **Fix the issues and successfully commit**

* Clean up the code (fix ESLint errors, format with Prettier)
* Use a proper commit message like:
  `feat: add login validation`

---

### 5. **GitHub Actions: Simple CI Workflow**

Create `.github/workflows/ci.yml`:

```yaml
name: Lint Check

on: [push, pull_request]

jobs:
  lint:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - name: Set up Node
        uses: actions/setup-node@v3
        with:
          node-version: '18'
      - run: npm install
      - run: npm run lint
```

---

## 📦 **Deliverables:**

* A **GitHub repo** with all the above set up
* **Screenshots** showing:

  * Commit failures
  * Commit success
* **GitHub Actions run history** (you can show the "Actions" tab)
* A **`README.md`** section explaining:

  * What automation you set up
  * Benefits like: saved time, reduced bugs, standardized code, etc.

---

Here are the **related topics and key concepts** you should understand or explore to fully grasp Assignment 4: **Git Hooks & Automation**:

---

## 🔧 **Core Tools and Concepts**

### 1. **Git Hooks**

* Client-side vs server-side hooks
* Pre-commit, commit-msg, pre-push, etc.
* Custom scripts in `.git/hooks/` (native Git hooks)
* Husky as a modern hook manager

### 2. **Husky**

* How Husky makes managing hooks easier
* How to install and configure hooks with Husky
* Integrating Husky with linting, formatting, and commitlint

### 3. **lint-staged**

* Running linters and formatters on **staged files only**
* Benefits: faster performance, avoids linting the whole project
* Works with any file type (JS, TS, CSS, etc.)

---

## 💅 **Code Quality Tools**

### 4. **ESLint**

* JavaScript/TypeScript linter
* Rules and plugins
* Auto-fixing with `--fix`
* Using `.eslintrc.json` or `.eslintrc.js`

### 5. **Prettier**

* Code formatter (style rules only, not logic)
* Automatically formats code consistently
* Works with many languages (JS, HTML, CSS, etc.)

---

## 🔏 **Commit Standards**

### 6. **commitlint + Conventional Commits**

* Enforces commit message format like:
  `type(scope): subject` (e.g., `feat(auth): add login button`)
* Common types: `feat`, `fix`, `chore`, `docs`, `test`, `refactor`
* Useful for changelogs, semantic versioning, and clarity

---

## 🤖 **Automation and CI/CD**

### 7. **GitHub Actions**

* Automating tasks like:

  * Linting
  * Running tests
  * Building apps
* `on: push` and `on: pull_request` triggers
* YAML syntax for workflows
* Understanding `jobs`, `steps`, and using actions like `actions/checkout` and `setup-node`

---

## 🧪 **Optional Advanced Topics (if curious)**

### 8. **Semantic Release**

* Automates versioning and changelog generation based on commit messages

### 9. **Pre-commit Framework** (non-JS projects)

* Especially for Python: [https://pre-commit.com/](https://pre-commit.com/)

### 10. **Monorepos & Nx / TurboRepo**

* If you're working with multiple projects in one repo, managing linting/hooks gets more complex

---

## 💡 **Practical Skills Gained**

* Automating quality checks before code is pushed
* Reducing bugs from bad commits
* Creating self-validating workflows
* Ensuring team-wide code consistency

---



