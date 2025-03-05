
## pnpm – How It Works (vs npm)

### How pnpm Stores Packages

npm downloads a full copy of each dependency into `node_modules` for every project — every project has its own copy, even if two projects use the same packages.

pnpm does it differently:  
- Packages are stored **once** in a global store (outside your project).  
- Each project’s `node_modules` only contains **symlinks** that point to the global store.

### Example Global Store

All files are saved here (outside your project):

```kotlin
~/.pnpm-store/v3/
├── files/
│   ├── 55/
│   │   └── abc1234567  # lodash@4 files
│   ├── 68/
│   │   └── def9876543  # react@18 files
```

Every project reuses the same files if they already exist — so installs are much faster and `node_modules` is much smaller.

---

### Example Project Node Modules with pnpm

Your project’s `node_modules` looks like this:

```kotlin
node_modules/
├── lodash -> .pnpm/lodash@4.17.21/node_modules/lodash
├── react -> .pnpm/react@18.2.0/node_modules/react
└── .pnpm/
    ├── lodash@4.17.21/
    │   └── node_modules/
    │       └── lodash/  # symlink to global store
    ├── react@18.2.0/
        └── node_modules/
            └── react/   # symlink to global store
```

Each symlink just points to the real files in the global store.

---

### What’s a Symlink?

It’s a file that contiants full path to global store location on disk. When you `import lodash`, Node follows the symlink to the global store and uses files from there.

---

### Hoisting Problem (npm)

npm tries to **hoist** packages to the top-level `node_modules` to save space. This works until two packages need **different versions** of the same dependency.

For example, if packageA and packageB both need lodash:

```kotlin
node_modules/
├── lodash/                  # hoisted (lodash@4)
├── packageA/
│   └── node_modules/
│       (empty if lodash@4 is hoisted)
├── packageB/
│   └── node_modules/
│       ├── lodash/          # only exists if packageB needs lodash@3
```

- If lodash@4 is hoisted, packageA is happy.
- If packageB needs lodash@3, npm might nest it under packageB’s `node_modules`.
- If packageB accidentally imports from the top level, it gets lodash@4 instead — version conflict.

This is why npm projects sometimes break when versions don’t match exactly.

---

### How pnpm Avoids Hoisting Problems

pnpm **never hoists conflicting versions**. Each package gets exactly the version it requested, even if that means two versions exist side by side.

Example folder structure in pnpm:

```kotlin
node_modules/
├── packageA -> .pnpm/packageA@1.0.0/node_modules/packageA
├── packageB -> .pnpm/packageB@1.0.0/node_modules/packageB
├── lodash -> .pnpm/lodash@4.17.21/node_modules/lodash
└── .pnpm/
    ├── packageA@1.0.0/
    │   └── node_modules/
    │       └── lodash -> global store lodash@4.17.21
    ├── packageB@1.0.0/
    │   └── node_modules/
    │       └── lodash -> global store lodash@3.10.1
    ├── lodash@4.17.21/
    │   └── node_modules/
    │       └── lodash/
    ├── lodash@3.10.1/
        └── node_modules/
            └── lodash/
```

- packageA gets lodash@4  
- packageB gets lodash@3  
- Each package is guaranteed to get exactly the version it needs, no accidental leaks.

---

### Lockfile Difference

npm uses `package-lock.json` — it tracks dependencies but can get messy because of hoisting.  
pnpm uses `pnpm-lock.yaml` — smaller, easier to read, and more accurate since it tracks dependencies **per package**, not per project.

---

### Monorepo Handling

npm has workspaces, but each workspace installs its own copies, even if they overlap.  
pnpm workspaces automatically link internal packages and reuse the global store — faster and cleaner.

---

### Switching from npm to pnpm (Quick Steps)

1. Remove `node_modules` and `package-lock.json`:

    ```kotlin
    rm -rf node_modules package-lock.json
    ```

2. If you have `package-lock.json`, convert it:

    ```kotlin
    pnpm import
    ```

3. Install with pnpm:

    ```kotlin
    pnpm install
    ```

4. Replace `npm run` with `pnpm run` in scripts:

    ```kotlin
    npm run start -> pnpm run start
    ```

5. Once it works, you can delete `package-lock.json`.

