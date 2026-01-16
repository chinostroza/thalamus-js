# Publishing Guide - @zea/thalamus-js

This guide explains how to publish new versions of the SDK to npm.

## Prerequisites

1. **npm Account**: You need an npm account with publishing rights to the `@zea` scope
   - Create account: https://www.npmjs.com/signup
   - Login: `npm login`

2. **Verify Build**: Ensure the build passes
   ```bash
   npm run build
   ```

3. **Update Version**: Update version in `package.json`
   ```json
   {
     "version": "1.0.1"
   }
   ```

## Publishing Steps

### 1. Clean Build
```bash
# Remove old builds
rm -rf dist

# Fresh install
npm install

# Build
npm run build
```

### 2. Test Package Contents
```bash
# Preview what will be published
npm pack --dry-run

# This will show:
# - Files included in the package
# - Total package size
# - package.json fields
```

### 3. Login to npm
```bash
npm login
# Enter username, password, and email
```

### 4. Publish to npm
```bash
# For first-time public publish
npm publish --access public

# For subsequent publishes
npm publish
```

### 5. Verify Publication
```bash
# Check on npm
npm view @zea/thalamus-js

# Install in a test project
npm install @zea/thalamus-js@latest
```

### 6. Tag Release in Git
```bash
git tag v1.0.0
git push origin v1.0.0
```

## Version Guidelines

Follow Semantic Versioning (semver):

- **MAJOR** (1.0.0 → 2.0.0): Breaking changes
- **MINOR** (1.0.0 → 1.1.0): New features, backward compatible
- **PATCH** (1.0.0 → 1.0.1): Bug fixes, backward compatible

Update version with:
```bash
npm version patch  # 1.0.0 -> 1.0.1
npm version minor  # 1.0.0 -> 1.1.0
npm version major  # 1.0.0 -> 2.0.0
```

## Release Checklist

- [ ] Update version in `package.json`
- [ ] Update CHANGELOG.md (if you have one)
- [ ] Run `npm run build` successfully
- [ ] Run `npm run test` (if tests exist)
- [ ] Run `npm pack --dry-run` to verify contents
- [ ] Commit changes: `git commit -m "chore: bump version to vX.Y.Z"`
- [ ] Create git tag: `git tag vX.Y.Z`
- [ ] Publish: `npm publish`
- [ ] Push to GitHub: `git push && git push --tags`
- [ ] Verify on npm: `npm view @zea/thalamus-js`

## Troubleshooting

### "You must be logged in to publish packages"
```bash
npm login
```

### "You do not have permission to publish '@zea/thalamus-js'"
- Contact the @zea organization owner to add you as a maintainer
- Or create the package with a different scope/name

### "Cannot publish over existing version"
- You tried to publish a version that already exists
- Bump the version number in package.json

## Unpublishing (Use with Caution)

You can unpublish within 72 hours:
```bash
npm unpublish @zea/thalamus-js@1.0.0
```

**Warning**: Unpublishing can break other people's projects. Only do this for serious issues.

## Beta/Alpha Releases

For pre-release versions:
```bash
# Set version to 1.1.0-beta.0
npm version 1.1.0-beta.0

# Publish with beta tag
npm publish --tag beta

# Users can install with:
npm install @zea/thalamus-js@beta
```

## GitHub Repository Setup

1. Create repo on GitHub: `https://github.com/zea/thalamus-js`
2. Add remote:
   ```bash
   git remote add origin git@github.com:zea/thalamus-js.git
   ```
3. Push:
   ```bash
   git push -u origin main
   git push --tags
   ```

## npm Package Page

After publishing, your package will be available at:
- https://www.npmjs.com/package/@zea/thalamus-js
- https://unpkg.com/@zea/thalamus-js@latest/

---

**First time publishing this package?**

Run:
```bash
npm publish --access public
```

This makes the `@zea/thalamus-js` package public on npm.
