# 🚀✨ Contributing to WalletConnect SDK ✨🚀

Welcome, brilliant developer! 👨‍💻👩‍💻 Thank you for your interest in contributing to **WalletConnect SDK (WcSdk)**! Your support drives innovation and growth in our ecosystem. This repository is the heart of WcSdk Core and WcSdk React/Svelte, beautifully orchestrated with the power of **Rush**.

Let's embark on this exciting journey to build something extraordinary together! 💡🌐

---

## 🛠️ Prerequisites & Setup Guide

### 1️⃣ Install Rush Globally
Unlock the potential of seamless development by installing Rush:

```bash
npm install @microsoft/rush -g
```

### 2️⃣ Project Initialization
Set up your development environment effortlessly:

```bash
rush update
```
> ✨ *This is equivalent to running `npm install` for each package.*

---

## 🏗️ Building the Project

Rebuild the entire project to ensure everything is running smoothly:

```bash
rush rebuild
```
> 🔄 *This functions like `npm run build` for all packages.*

---

## ✅ Pre-Commit Checklist

Before committing any code, follow these essential steps:

1. Build the project to validate your changes.
2. Generate a change file:
   ```bash
   rush change
   ```
> 🔍 *Helps track updates and ensures proper versioning.*

---

## 🚀 Publishing a New Release

Ready to share your work with the world? Follow these steps for a smooth publishing process:

1. Build the project:
   ```bash
   rush rebuild
   ```
2. Increment the version of each package appropriately.
3. Commit your changes with a meaningful message.
4. Navigate into each package directory and publish:
   ```bash
   npm publish
   ```

> 📝 *Ensure you have proper access rights for publishing!* 🔑

---

## 🔄 Resolving Dependency Issues

Stuck with dependency errors? No worries! Follow these quick fixes:

1. **Remove** the existing lock file:
   ```bash
   rm common/config/npm-shrinkwrap.json
   ```
2. **Refresh dependencies:**
   ```bash
   rush update
   ```

> 💡 *This clears inconsistencies and restores harmony among packages.*

---

## 🌟 Let’s Build the Future Together!

Your contributions are the fuel that powers innovation at WalletConnect SDK. Let's collaborate to push the boundaries of decentralized connectivity. Every line of code you write brings us one step closer to a more connected and secure blockchain future. 🚀💼

**Thank you for being part of this journey! 💖**

> Connect. Innovate. Empower.

Stay Epic,

**The WalletConnect SDK Team**

---

*Need help? Have questions?* Feel free to open an issue or reach out. We're here to help you thrive! 🙌

