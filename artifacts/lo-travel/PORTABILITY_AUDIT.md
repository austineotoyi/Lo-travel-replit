# Portability Audit

## Result

The LO Travel mobile app is packaged as a standalone Expo/React Native project
that can be cloned from GitHub and installed with npm. It does not require
Replit to install dependencies, run TypeScript, generate Android files, or run
the GitHub Actions build.

## Removed from the mobile package

- Replit artifact metadata and workspace configuration
- `catalog:` and `workspace:*` dependency specifications
- Replit-only development environment variables and scripts
- The unused Expo Router scaffold
- The unused legacy static build script
- Replit package-firewall URLs from `package-lock.json`
- Duplicate Android GitHub Actions workflow

## Standard build entry points

- `npm install --legacy-peer-deps --ignore-scripts`
- `npm run typecheck`
- `cd android && ./gradlew assembleDebug`
- `cd android && ./gradlew assembleRelease`
- `.github/workflows/android-build.yml`

## Verification completed

- Public-registry npm install: passed
- TypeScript check: passed with zero errors
- Android project files and Gradle wrapper: present
- GitHub Actions workflow: uses standard checkout, Node, Java, Android SDK,
  npm, Gradle cache, Gradle wrapper, and artifact upload actions

## Environment limitation

The Replit runtime does not provide Java or the Android SDK, so Gradle APK
assembly must be run on a developer machine or GitHub Actions runner. The
workflow installs the required Android SDK components and builds both debug
and release variants.