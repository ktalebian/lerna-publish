# lerna-publish

A simple script for publishing Lerna monorepo projects.

## Installation
Install using

```bash
# If using npm
npm install -D @k88/lerna-publish

# If using yarn
yarn add -D @k88/lerna-publish
```

## Usage

Add the following three scripts to your package.json's `scripts`:

```json
{
  "scripts": {
    "publish:alpha": "lerna-publish alpha",
    "publish:beta": "lerna-publish beta",
    "publish:public": "lerna-publish public"
  }
}
```

## Details

The script will perform the following tasks:

1) Check publish version (see below for more detail)
2) Removes all dist/lib/node_modules directory
3) Performs a fresh `npm install`
4) Runs `npm run lint`
5) Runs `npm run test`
6) Runs `npm run build`
7) Publishes the packages

### Publish types

This script safeguards performing `public/beta/alpha` publication based on:

* `public` may only run on `main` branch
* `beta` may only run on `v\d-beta` branch (i.e. `v1-beta`, `v2-beta`, `v3-beta`, etc)
* `alpha` may only run on non-beta/non-publich branches

### Distribution Tags

The following tags are published:

* The `public` publish pushes a `latest` dist tag
* The `beta` publish pushes a `beta` dist tag
* The `alpha` publish pushes a `alpha` dist tag

### Version bump

You can pass an optional `patch/minor/major` argument to change the version bump. By default, a `patch` is published. Some examples are:

```bash
# Publishes a patch beta
npm run publish:beta

# Publishes a minor public
npm run publish:public minor
```

### No package-lock.json

If you do not want to keep your package-file.json, provide `NO_PACKAGE_LOCK=1 lerna-publish ...` to force-remove the lock.





