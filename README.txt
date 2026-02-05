SURVIVALCRAFT BROWSER PORT (WORK IN PROGRESS)
===============================================

You have successfully set up the project structure for porting Survivalcraft to the web (WebAssembly).

CURRENT STATUS:
---------------
The source code and assets have been moved to this folder.
However, the game CANNOT run yet.

THE PROBLEM:
------------
The original game depends on "Engine.dll", which is a closed-source library that uses DirectX (SharpDX).
DirectX works ONLY on Windows. It does not work in a Web Browser.
Web Browsers use WebGL.

HOW TO FIX IT (THE PATH FORWARD):
---------------------------------
To make this run in a browser, you need to replace "Engine.dll" with a web-compatible engine.

1.  **Decompile Engine.dll**: You need the source code for the Engine, just like you have for the Game.
    Tools like ILSpy or dnSpy can decompile "Libs/Engine.dll" to C# code.

2.  **Port to MonoGame (Kni)**: 
    The original Engine wraps SharpDX. You need to modify the Engine source code to wrap "MonoGame" (specifically the Kni fork) instead.
    MonoGame supports running C# games in the browser using WebGL.

3.  **Fix Compilation Errors**:
    Once you have the Engine source in this project, there will be errors because DirectX calls (SharpDX) need to be changed to MonoGame calls.

4.  **Build**:
    Open "SurvivalcraftWasm.csproj" and build it.

FILES:
------
- /Game: The decompiled game logic.
- /Assets: The game assets (Content.pak).
- /Libs: The original DLLs (for reference/decompilation).
- SurvivalcraftWasm.csproj: The project file for building the web version.

Good luck!
