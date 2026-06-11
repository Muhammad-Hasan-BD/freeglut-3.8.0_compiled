# Pre-Compiled FreeGLUT 3.8.0 for MinGW (Windows)

This repository contains stable, pre-compiled **FreeGLUT 3.8.0** 64-bit binaries built natively using the MinGW GCC compiler framework on Windows. 

If you are tired of dealing with broken legacy `glut32` links, dead sites, or struggling to compile raw source code using CMake, you can just download the compiled zip bundle from this repository to jump-start your OpenGL graphics projects instantly.

---

## 📦 What's Inside the Zip Archive
Download and extract `freeglut-3.8.0_compiled.zip`. Inside, you will find:
* **`include/GL/`**: Core C++ graphics header files (`glut.h`, `freeglut.h`, etc.)
* **`build/lib/`**: Pre-compiled linker binaries (`libfreeglut.a`, `libfreeglut_static.a`) for GCC/MinGW compilers.
* **`build/bin/`**: The runtime component (`libfreeglut.dll`) required to launch your window environment.

---

## 🛠️ Setup Guides

### 1. Code::Blocks Global Setup (Recommended)
To configure your IDE so that every project automatically recognizes FreeGLUT without manual configurations:

1. Download and extract `freeglut-3.8.0_compiled.zip` to a permanent path (e.g., `C:\freeglut`).
2. Open **Code::Blocks** and head to **Settings** ➡️ **Compiler...**
3. Select the **Search directories** horizontal tab:
   * Under the **Compiler** sub-tab, click **Add** and choose: `C:\freeglut\include`
   * Under the **Linker** sub-tab, click **Add** and choose: `C:\freeglut\build\lib`
4. Select the **Linker settings** horizontal tab:
   * Under **Link libraries**, click **Add** and select the file: `C:\freeglut\build\lib\libfreeglut.a`
   * Under **Other linker options**, add the following flags to link standard Windows graphics:
     ```text
     -lopengl32
     -lglu32
     ```
5. Copy `libfreeglut.dll` from the `build/bin/` folder and paste it into `C:\Windows\System32` (or keep a copy in your project's executable directory).

---

### 2. VS Code Project Setup
If you prefer writing code inside Visual Studio Code:

1. Extract the zip file and copy the `include/` folder, and the contents of `build/lib/` and `build/bin/` straight into your workspace project root folder.
2. Create a `.vscode/` directory in your workspace and add a **`tasks.json`** file with the following compiler arguments:

```json
{
    "version": "2.0.0",
    "tasks": [
        {
            "type": "shell",
            "label": "Build OpenGL Project",
            "command": "g++",
            "args": [
                "-g",
                "${workspaceFolder}/main.cpp",
                "-o",
                "${workspaceFolder}/main.exe",
                "-I${workspaceFolder}/include",
                "-L${workspaceFolder}/lib",
                "-lfreeglut",
                "-lopengl32",
                "-lglu32"
            ],
            "group": {
                "kind": "build",
                "isDefault": true
            }
        }
    ]
}
