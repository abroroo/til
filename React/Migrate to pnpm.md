
## Understanding pnpm – How It Works (Compared to npm)

### Package Storage – Global Store  
npm downloads and stores a full copy of each dependency directly inside `node_modules` for every project. Each project is independent.  

### ✅ Key Benefit
- Your `node_modules` stays **very small**.
- All heavy files are in the **global store**, not duplicated across projects.
- Future projects can instantly **reuse the same packages** without downloading again.
  
### Example scenario  
Let’s say you have a React project that uses `lodash` and `react`.

When you run `pnpm install`, pnpm does **two key things**:

---

### 1️⃣ Stores actual packages in a **global store** (outside your project)

Example global store location:

```kotlin
~/.pnpm-store/v3/
├── files/
│   ├── 55/
│   │   └── abc1234567 (actual files for lodash@4)
│   ├── 68/
│   │   └── def9876543 (actual files for react@18)
```

This is **outside your project folder** and is shared between all your projects.

---

### 2️⃣ Creates symlinks in your project’s `node_modules`

Inside your project’s `node_modules`:

```kotlin
node_modules/
├── lodash -> .pnpm/lodash@4.17.21/node_modules/lodash
├── react -> .pnpm/react@18.2.0/node_modules/react
└── .pnpm/
    ├── lodash@4.17.21/
    │   └── node_modules/
    │       └── lodash/  (symlink pointing to global store)
    ├── react@18.2.0/
        └── node_modules/
            └── react/   (symlink pointing to global store)
```

### 🔗 What’s a symlink?
A **symlink is a special file that stores path url to the gloabl store**, pointing to the real files in the global store.

- When your code imports `lodash`, it **follows the symlink**.
- Instead of loading files from your project’s `node_modules/lodash`, it reads directly from the **global store copy**.

---

### Version Isolation – No Hoisting Conflicts  

npm allows version ranges like `^3.0.0` (3.x only). During install, npm hoists shared versions to the root to save space. If most packages accept `lodash@4`, npm may hoist it, even if one package strictly needs `^3`. Due to npm’s hoisting logic or peer dependency gaps, that nested `lodash@3` can be skipped, and Node.js may accidentally load the hoisted version instead. pnpm avoids this by fully isolating every package’s dependencies with strict symlinks, so each package always gets exactly the version it asked for.

---

## 📂 npm folder structure (hoisting)

If **packageA** and **packageB** both depend on **lodash**, but different versions:

- npm tries to **hoist lodash to the top-level `node_modules` if versions are compatible.**
- If versions conflict, **one version is hoisted, and the other might be nested inside a package’s `node_modules`**.
- This **hoisting can cause a package to accidentally import the wrong version if it looks up the wrong path.**

```kotlin
node_modules/
├── lodash/                  <-- Hoisted (might be lodash@4)
├── packageA/
│   └── node_modules/
│       (empty if lodash@4 was hoisted)
├── packageB/
│   └── node_modules/
│       ├── lodash/          <-- Only if packageB needs lodash@3
```

- packageA might work fine with lodash@4 (hoisted).
- packageB might get lodash@3 inside its own `node_modules` if the versions conflict.
- If packageB accidentally imports from the top level (lodash@4), **version mismatch happens**.

---

## 📂 pnpm folder structure (no hoisting)

pnpm **never hoists conflicting versions**. Each package gets exactly what it needs, fully isolated inside `.pnpm`, and `node_modules` just contains **symlinks pointing to the correct version**.

```kotlin
node_modules/
├── packageA -> .pnpm/packageA@1.0.0/node_modules/packageA
├── packageB -> .pnpm/packageB@1.0.0/node_modules/packageB
├── lodash -> .pnpm/lodash@4.17.21/node_modules/lodash  (symlink for root lodash)
└── .pnpm/
    ├── packageA@1.0.0/
    │   └── node_modules/
    │       └── lodash -> Global store lodash@4.17.21
    ├── packageB@1.0.0/
    │   └── node_modules/
    │       └── lodash -> Global store lodash@3.10.1
    ├── lodash@4.17.21/
    │   └── node_modules/
    │       └── lodash/   (actual lodash@4 files)
    ├── lodash@3.10.1/
        └── node_modules/
            └── lodash/   (actual lodash@3 files)
```

- **packageA gets lodash@4**.
- **packageB gets lodash@3**.
- Both are guaranteed to get the correct version, no accidental version leaking.

---

### Lockfile Differences  
npm uses `package-lock.json`, which tracks top-level and nested dependencies in a somewhat flat format.  
pnpm uses `pnpm-lock.yaml`, which is smaller, easier to review, and tracks nested dependencies more accurately.

### Monorepo Handling  
npm has workspaces, but each workspace still downloads and manages packages separately, leading to slower installs and potential duplication.  
pnpm workspaces automatically link internal packages and reuse the global store, making installs faster and package sharing cleaner.

---

## Migration Guide – Switching from npm to pnpm

1. Delete `node_modules` and optionally `package-lock.json`.
    ```kotlin
    rm -rf node_modules package-lock.json
    ```

2. If `package-lock.json` exists, run:
    ```kotlin
    pnpm import
    ```
    This converts `package-lock.json` to `pnpm-lock.yaml`.

3. Install using pnpm:
    ```kotlin
    pnpm install
    ```

4. Replace `npm run` with `pnpm run` in any scripts or CI jobs.
    ```kotlin
    npm run start -> pnpm run start
    ```

5. You can safely remove `package-lock.json` after migrating if desired.
