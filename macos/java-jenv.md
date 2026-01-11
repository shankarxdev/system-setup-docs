# Java + Jenv Management Guide for macOS

This document serves as a complete reference for installing, updating, removing, and managing Java versions on macOS using Homebrew and **jenv**.

---

## 1. Update Homebrew

```bash
brew update
brew upgrade
```

- **brew update** updates Homebrew package definitions.
- **brew upgrade** updates all installed packages, including JDKs.

---

## 2. Install a New JDK

### Option A — Install via Homebrew (Recommended)

Install Java 25 (LTS):

```bash
brew install temurin@25
```

Homebrew installs JDKs under: `/Library/Java/JavaVirtualMachines/`

---

### Option B — Install via SDKMAN

Install SDKMAN:

```bash
curl -s "https://get.sdkman.io" | bash
source "$HOME/.sdkman/bin/sdkman-init.sh"
```

Install Java 25:

```bash
sdk install java 25.0.1-tem
```

---

### Option C — Manual Install

Download from [https://jdk.java.net](https://jdk.java.net), then place under: `/Library/Java/JavaVirtualMachines/`

---

## 3. List Installed JDKs on macOS

```bash
/usr/libexec/java_home -V
```

This shows all detected JDK installations.

---

## 4. Add a JDK to jenv

```bash
jenv add /Library/Java/JavaVirtualMachines/temurin-25.jdk/Contents/Home
jenv rehash
```

- Registers the JDK with jenv.
- **rehash** updates internal shims.

---

## 5. Remove Unwanted JDKs from jenv

```bash
jenv remove temurin64-21.0.7
jenv remove 21.0.7
jenv rehash
```

- Removes version entries from jenv.
- Does *not* delete actual JDK files.

---

## 6. Uninstall JDKs from macOS

### Homebrew JDK Removal

```bash
brew uninstall temurin@21
```

### Manual JDK Removal

```bash
sudo rm -rf /Library/Java/JavaVirtualMachines/temurin-21.jdk
```

After removal, clean jenv:

```bash
jenv remove temurin64-21.0.7
jenv rehash
```

---

## 7. List jenv Versions

```bash
jenv versions
```

Displays all JDKs known to jenv.

---

## 8. Switch Java Versions

### Set Global Java Version

```bash
jenv global temurin64-25.0.1
```

### Set Project-local Java Version

```bash
cd your-project
jenv local temurin64-21.0.9
```

### Set Version for Current Shell

```bash
jenv shell temurin64-17.0.17
```

---

## 9. Verify Active Java Version

```bash
java -version
javac -version
```

Validates your active JDK.

---

## 10. Update Existing JDK Versions

Use Homebrew:

```bash
brew update
brew upgrade temurin@17
brew upgrade temurin@21
brew upgrade temurin@1.8
```

After upgrade, clean duplicates:

```bash
jenv remove temurin64-17.0.15
jenv add /Library/Java/JavaVirtualMachines/temurin-17.jdk/Contents/Home
jenv rehash
```

---

## 11. Clean Duplicate or Old JDK Versions

```bash
jenv remove temurin64-21.0.7
jenv remove 21.0.7
jenv rehash
```

---

## 12. Best Practices

- Prefer `temurin64-*` identifiers to avoid confusion.
- Always `jenv rehash` after installing/removing JDKs.
- Keep only LTS versions: **8, 17, 21, 25**.
- Use `jenv local` for project-specific Java needs.
- Remove old JDKs from both **Homebrew** and **jenv**.

---

## Summary

This document gives you complete instructions on:

- Installing new JDK versions
- Updating existing ones
- Removing old or unused JDKs safely
- Managing and switching Java versions with jenv

If you want, I can also generate an automation script that sets up everything with one command.

