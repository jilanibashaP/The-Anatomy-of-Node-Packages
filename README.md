# The Anatomy of Node Packages

## Understanding Package Files

### package.json vs package-lock.json

The **package.json** file only contains the dependencies with semantic versioning. It does not keep track of the exact versions of dependencies or their sub-dependencies.

On the other hand, the **package-lock.json** file contains the exact versions of each installed package, including sub-dependencies. It also includes the resolved URLs and the actual versions that were installed.

## Installation Behavior

When both `package.json` and `package-lock.json` are present, `node_modules` will be installed using the exact versions specified in `package-lock.json`.

If two people have the same `package-lock.json`, their `node_modules` directories will be identical, which is why we do not need to push the `node_modules` folder to GitHub.

If the `package-lock.json` file is not present, npm will generate a new one based on the dependencies defined in `package.json` using semantic versioning, and then install the `node_modules`.

## Best Practices for Version Control

If we want consistency across environments, we need to push both `package.json` and `package-lock.json` to the repository.

- **package.json** is the source of truth for our project's dependencies, scripts, and metadata
- **package-lock.json** is a snapshot of the entire dependency tree with exact versions, ensuring the same packages are installed every time

### When to Skip package-lock.json

If consistency between dependency versions is not required based on semantic versioning, then don't push `package-lock.json`. In that case, dependencies will be installed based on semantic versioning defined in `package.json`.

## What is Semantic Versioning?

Semantic versioning (also known as **semver**) is a versioning scheme in the format:

```
MAJOR.MINOR.PATCH
```

**Example:** `^1.4.2`

- **MAJOR**: Breaking changes (e.g., `1.x.x` → `2.0.0`)
- **MINOR**: Backward-compatible new features (e.g., `1.4.x` → `1.5.0`)
- **PATCH**: Backward-compatible bug fixes (e.g., `1.4.2` → `1.4.3`)

### Symbols in package.json

- `^1.4.2` allows updates to any version `<2.0.0` (same major version)
- `~1.4.2` allows updates to any version `<1.5.0` (same minor version)
- No symbol (e.g., `1.4.2`) means only that exact version will be installed

## Conclusion

If you don't care about exact versions and are okay with minor or patch updates happening automatically, you can omit `package-lock.json`. However, for predictable and consistent builds across different environments, it's best to include it in your repository.
