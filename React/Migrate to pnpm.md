
## Understanding pnpm – How It Works (Compared to npm)

### Package Storage – Global Store  
npm downloads and stores a full copy of each dependency directly inside `node_modules` for every project. Each project is independent.  
pnpm stores all packages in a **global store** on the machine (for example, `~/.pnpm-store`). Each project’s `node_modules` doesn’t contain real files — just symlinks pointing to that global store. This allows pnpm to reuse packages across projects without downloading them again.

### Dependency Linking – Symlink Structure  
npm places actual files inside `node_modules`, sometimes hoisting shared dependencies to the top level.  
pnpm places symlinks inside `node_modules` that point to the correct version stored in the global store. Each package gets its own isolated `node_modules` folder under `.pnpm`, which only contains what that package needs.

Example for lodash in a pnpm project:

```
node_modules/
├── lodash -> .pnpm/lodash@4.17.21/node_modules/lodash
├── .pnpm/
│   ├── lodash@4.17.21/
│   │   └── node_modules/
│   │       └── lodash/   (actual lodash files, symlinked from the global store)
```

This way, lodash only exists once in the global store, and all projects just link to it.

### Version Isolation – No Hoisting Conflicts  
npm tries to hoist shared dependencies to the top of `node_modules`, meaning two packages needing different versions might result in only one being available. This can lead to version mismatches where a package accidentally uses the wrong version.  
pnpm avoids this by keeping each package’s dependencies fully isolated under `.pnpm`, with only carefully chosen safe hoisting. This guarantees every package gets the exact versions it declares.

Example folder structure showing isolation:

```
node_modules/
├── packageA -> .pnpm/packageA@1.0.0/node_modules/packageA
├── packageB -> .pnpm/packageB@1.0.0/node_modules/packageB
├── lodash -> .pnpm/lodash@4.17.21/node_modules/lodash
└── .pnpm/
    ├── packageA@1.0.0/
    │   └── node_modules/
    │       └── lodash -> Global store (lodash@4.17.21)
    ├── packageB@1.0.0/
    │   └── node_modules/
    │       └── lodash -> Global store (lodash@3.10.1)
    ├── lodash@4.17.21/
    │   └── node_modules/
    │       └── lodash/ (real files from global store)
    ├── lodash@3.10.1/
        └── node_modules/
            └── lodash/ (real files from global store)
```

Each package gets exactly the version it asked for, no silent replacements.

### Lockfile Differences  
npm uses `package-lock.json`, which tracks top-level and nested dependencies in a somewhat flat format.  
pnpm uses `pnpm-lock.yaml`, which is smaller, easier to review, and tracks nested dependencies more accurately.

### Monorepo Handling  
npm has workspaces, but each workspace still downloads and manages packages separately, leading to slower installs and potential duplication.  
pnpm workspaces automatically link internal packages and reuse the global store, making installs faster and package sharing cleaner.

---

## Migration Guide – Switching from npm to pnpm

1. Delete `node_modules` and optionally `package-lock.json`.
    ```
    rm -rf node_modules package-lock.json
    ```

2. If `package-lock.json` exists, run:
    ```
    pnpm import
    ```
    This converts `package-lock.json` to `pnpm-lock.yaml`.

3. Install using pnpm:
    ```
    pnpm install
    ```

4. Replace `npm run` with `pnpm run` in any scripts or CI jobs.
    ```
    npm run start -> pnpm run start
    ```

5. You can safely remove `package-lock.json` after migrating if desired.
