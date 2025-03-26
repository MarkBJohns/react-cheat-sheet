# 🧰 Setup Instructions for Using `temp-library` on Windows (No Linux Required)

## ✅ Goal

Set up a React component library that:
- Works from Windows Command Prompt or PowerShell
- Can generate new React apps from templates using:

```bash
npx template <template-path> <app-name>
```

---

## ⚒️ Prerequisites (One-Time Setup)

### 1. Install Node.js (LTS)

Install the latest LTS version of Node.js (includes `npm`):

- From website: [https://nodejs.org](https://nodejs.org)

**Or from terminal (PowerShell or CMD):**

```bash
winget install OpenJS.NodeJS.LTS -s winget
```

---

### 2. Verify Install

Open **Command Prompt** or **PowerShell**, then run:

```bash
node -v
npm -v
```

---

## 📦 Usage: Using the Library

### 1. Clone the Library

```bash
git clone https://github.com/MarkBJohns/temp-library
cd temp-library
npm install
cd ..
```

### 2. Link It Locally (from Outside the Folder)

From the folder *above* `temp-library`:

```bash
npm install ./temp-library
```

---

### 3. Create a New App

Run this from the same folder (outside `temp-library`):

```bash
npx template page-starters/test-page test-app
```

This creates a new folder `test-app` using the `test-page` template.

---

### 4. Start the App

```bash
cd test-app
npm install
npm run dev
```
