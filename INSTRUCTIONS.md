# Survivalcraft Web Port Instructions

## Current Status
I have successfully:
1.  Decompiled the closed-source `Engine.dll` into C# source code (in `Engine/`).
2.  Set up the `Game` logic (in `Game/`).
3.  Created a .NET 9 WebAssembly project (`SurvivalcraftWasm.csproj`) that includes both.
4.  Created the HTML entry point (`wwwroot/index.html`).

## How to Compile
1.  Open `Survivalcraft.sln` in Visual Studio 2022 (or VS Code).
2.  Right-click the Solution and select "Restore NuGet Packages".
3.  Build the solution.

## Critical Next Steps (The "Hard Part")
The original game engine was built for Windows (DirectX/OpenGL Desktop).
Web Browsers use **WebGL**.

1.  **Fix Compilation Errors**: 
    The decompiled `Engine` code uses `OpenTK`. The NuGet package referenced is OpenTK 4.x. You may need to fix namespace differences (e.g., `OpenTK.Graphics.ES20` might be different in modern OpenTK).

2.  **Replace the Graphics Backend**:
    This is the most important step. You need to rewrite `Engine/Graphics/Display.cs` and `Engine/Graphics/GLWrapper.cs`.
    *   **Goal**: Replace `GL.DrawArrays` calls with **WebGL** calls.
    *   **Recommended**: Use **Silk.NET** (which supports WebGL) or **Blazor.Extensions.Canvas**.
    *   **Alternative**: Port the entire `Engine` project to use **MonoGame (Kni)**, which handles this for you.

3.  **Fix the Game Loop**:
    The original `Game/Program.cs` calls `Window.Run()`, which is an infinite loop.
    In a browser, you cannot have an infinite loop (it freezes the page).
    You must change `Window.Run()` to use `requestAnimationFrame` loop pattern.

## Assets
The `Assets/` folder contains your `Content.pak`. The build is set to copy this to the web root so the game can load it.

Good luck! You have the full source code now, so everything is possible.
