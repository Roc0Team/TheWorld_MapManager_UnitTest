# TheWorld_MapManager_UnitTest

The existing native Visual Studio test project is included in `..\build\TerrainTechDemo.sln` and in the top-level CMake build. The x64 configurations use MSVC v145 and C++20. MapManager and Utils must be built before linking the tests; both workflows handle these dependencies automatically.

From `TerrainTechDemo`, build with:

```powershell
msbuild .\build\TerrainTechDemo.sln /t:TheWorld_MapManager_UnitTest /m /p:Configuration=Debug /p:Platform=x64
```

Alternatively, after configuring the top-level CMake project:

```powershell
cmake --build .\build\out\cmake --config Debug --target TheWorld_MapManager_UnitTest
ctest --test-dir .\build\out\cmake -C Debug -R '^TheWorld_MapManager_UnitTest$' --output-on-failure
```

Outputs are `build\x64\TheWorld_MapManager_UnitTest_d.dll` (Debug) and `build\x64\TheWorld_MapManager_UnitTest.dll` (Release). Use Visual Studio Test Explorer to select individual tests. `TestMethodCreateWD` checks WorldDefiner calculations; the three `TestMethodAddAndEraseWD*` tests modify MapManager data and require a configured, disposable database environment.
