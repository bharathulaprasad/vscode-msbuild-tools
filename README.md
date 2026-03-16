# msbuild-tools

Work with **Visual Studio (MSBuild) projects** directly from **Visual Studio Code**.

Feedback is highly appreciated! Let me know:  
- Does this work for you?  
- Are there any showstopping bugs?  
- Any missing features?  

> Note: I may eventually merge this into `vscode-xbuild-tools` when I have time.

---

## Caveats

- First release; my first non-trivial TypeScript/JavaScript program — expect some bugs, issues, and non-idiomatic code.
- Managing the project (adding files, changing settings, etc.) should be done using **Visual Studio** itself.

---

## Features

- Build, Clean, Debug, and Run Visual Studio solutions directly in VSCode.
- Switch between build configurations (Debug/Release).
- Debug directly from VSCode — easily define debug configurations.
- Status bar items for quick access to build, debug, and configuration switching.

---

## Demo

1. **Create a project in Visual Studio**

![Create a project in Visual Studio](gifs/vs-create-project.gif)

2. **Open the project in VSCode**

![msbuild-tools demo](gifs/msbuild-tools-demo.gif)

---

## Example

The `example` subdirectory contains a working example.

1. Open VSCode in `example/helloworld` and examine `.vscode/msbuild-tools.json`.
2. Use `msbuild-tools` commands to:
   - Build, Debug, Run, Clean
   - Switch build configurations
   - Switch debug configurations
3. Use the **status bar** to build, debug, switch configurations, or kill the build.

### `.vscode/msbuild-tools.json` example

```json
{
    "solution": "${workspaceRoot}/helloworld.sln",
    "variables": {
        "MSBUILD": "C:/program files/Microsoft Visual Studio/2022/BuildTools/MSBuild/Current/Bin/MSBuild.exe"
    },
    "buildConfigurations": [
        "Debug",
        "Release"
    ],
    "platformConfigurations": [
        "x64",
        "x86"
    ],
    "preBuildTasks": [
        {
            "name": "Print a message",
            "program": "cmd",
            "args": ["/c", "echo [pre-build task]: Build Started"],
            "cwd": "${workspaceRoot}"
        }
    ],
    "postBuildTasks": [
        {
            "name": "Print another message",
            "program": "cmd",
            "args": ["/c", "echo [post-build task]: BUILD Finished"],
            "cwd": "${workspaceRoot}"
        }
    ],
    "debugConfigurations": [
        {
            "name": "test",
            "cwd": "${workspaceRoot}",
            "program": "${workspaceRoot}/x64/${buildConfig}/helloworld.exe",
            "args": []
        }
    ]
}