# Windows 11 Installation Guide for Opcode

This guide will help you install all required dependencies and build opcode on Windows 11.

## Prerequisites

### 1. Microsoft C++ Build Tools (REQUIRED)

Tauri and Rust require Visual Studio C++ Build Tools.

**Installation:**
1. Download [Microsoft C++ Build Tools](https://visualstudio.microsoft.com/visual-cpp-build-tools/)
2. Run the installer
3. During installation, check the **"Desktop development with C++"** option
4. Complete the installation (may take 10-15 minutes)

**Why:** Rust and Tauri need MSVC compiler toolchain for Windows development.

**Sources:**
- [Tauri Prerequisites](https://v2.tauri.app/start/prerequisites/)
- [Microsoft Learn - Rust Setup](https://learn.microsoft.com/en-us/windows/dev-environment/rust/setup)

---

### 2. Rust (REQUIRED)

**Installation:**
1. Download the official installer: [rustup-init.exe](https://www.rust-lang.org/tools/install)
2. Run `rustup-init.exe`
3. Follow the onscreen instructions
4. **Important:** Ensure the MSVC toolchain is selected (x86_64-pc-windows-msvc)
5. Installation will add Rust to your PATH automatically

**Verification:**
Open a **new** terminal (Command Prompt or PowerShell) and run:
```powershell
rustc --version
cargo --version
```

You should see version numbers like:
```
rustc 1.xx.x (xxxxx 2026-xx-xx)
cargo 1.xx.x (xxxxx 2026-xx-xx)
```

**Note:** If the commands aren't found, restart your terminal or log out and back in to refresh PATH.

**Sources:**
- [Official Rust Installation](https://rust-lang.org/tools/install/)
- [rustup.rs](https://rustup.rs/)

---

### 3. Bun (REQUIRED)

Opcode uses Bun as its JavaScript package manager.

**Installation:**
1. Download the Windows installer: [bun-setup-x64.exe](https://bun.com/docs/installation)
2. Right-click the installer and select **"Run as administrator"**
3. Ensure the checkbox **"Add Bun to PATH"** is selected
4. Complete the installation wizard

**Verification:**
Open a **new** terminal and run:
```powershell
bun --version
```

You should see a version number like: `1.x.x`

**Prerequisites for Bun:**
If you encounter errors, install [Microsoft Visual C++ Redistributable for Visual Studio 2022 (x64)](https://aka.ms/vs/17/release/vc_redist.x64.exe)

**Sources:**
- [Bun Installation](https://bun.com/docs/installation)
- [Bun Windows Guide](https://medium.com/@tawfeeq/how-to-install-bun-js-on-windows-11-29067f86a98b)

---

### 4. WebView2 (Already Installed)

**Good news:** WebView2 is pre-installed on Windows 11. No action needed!

WebView2 is the rendering engine used by Tauri to display the UI.

---

### 5. Claude Code CLI (Already Installed ✓)

You already have Claude Code CLI version 2.1.7 installed. No action needed!

Verify with:
```powershell
claude --version
```

---

## Building Opcode

Once all prerequisites are installed, follow these steps:

### Step 1: Install Frontend Dependencies

Open a terminal in the opcode directory and run:
```powershell
bun install
```

This will install all Node.js/React dependencies defined in `package.json`.

---

### Step 2: Build and Run in Development Mode

Run the Tauri development server with hot reload:
```powershell
bun run tauri dev
```

This will:
1. Build the React frontend with Vite
2. Compile the Rust backend
3. Launch the application
4. Enable hot reload for development

**First build will take 5-10 minutes** as Rust compiles all dependencies.

---

### Step 3: Create Production Build (Optional)

To create a distributable Windows executable:
```powershell
bun run tauri build
```

The built files will be in:
```
src-tauri/target/release/opcode.exe          # Executable
src-tauri/target/release/bundle/             # Installers (MSI, NSIS)
```

---

## Troubleshooting

### Issue: "rustc not found" after installation
**Solution:**
- Close and reopen your terminal
- Or log out and back in to refresh PATH
- Or manually add to PATH: `%USERPROFILE%\.cargo\bin`

### Issue: "MSVC not found" during Rust/Tauri build
**Solution:**
- Install Microsoft C++ Build Tools (Step 1)
- Ensure "Desktop development with C++" is selected
- Restart terminal after installation

### Issue: Bun installation fails
**Solution:**
- Install Visual C++ Redistributable 2022
- Run installer as administrator
- Download from: https://aka.ms/vs/17/release/vc_redist.x64.exe

### Issue: Build fails with "out of memory"
**Solution:**
- Close other applications
- Build with fewer parallel jobs: `cd src-tauri && cargo build -j 2`

### Issue: "WebView2 not found"
**Solution:**
- On Windows 11, this shouldn't happen
- If it does, download WebView2 Runtime: https://developer.microsoft.com/microsoft-edge/webview2/

---

## Quick Check: Are All Dependencies Installed?

Run these commands to verify everything is ready:

```powershell
# Check Rust
rustc --version

# Check Cargo (Rust package manager)
cargo --version

# Check Bun
bun --version

# Check Claude CLI
claude --version

# Check Git (should already be installed)
git --version
```

If all commands return version numbers, you're ready to build opcode!

---

## Summary of Installation Order

1. ✅ Install Microsoft C++ Build Tools (with "Desktop development with C++")
2. ✅ Install Rust (rustup-init.exe, select MSVC toolchain)
3. ✅ Install Bun (bun-setup-x64.exe, run as admin)
4. ✅ Run `bun install` in opcode directory
5. ✅ Run `bun run tauri dev` to start development

---

## Sources

- [Rust Installation](https://rust-lang.org/tools/install/)
- [Bun Installation](https://bun.com/docs/installation)
- [Tauri 2 Prerequisites](https://v2.tauri.app/start/prerequisites/)
- [Microsoft Learn - Rust Setup](https://learn.microsoft.com/en-us/windows/dev-environment/rust/setup)
- [Bun Windows Guide](https://medium.com/@tawfeeq/how-to-install-bun-js-on-windows-11-29067f86a98b)

---

## Need Help?

- Opcode GitHub: https://github.com/getAsterisk/opcode
- Discord: https://discord.com/invite/KYwhHVzUsY
- Claude Code Documentation: https://claude.ai/code
