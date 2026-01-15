# Repository Guidelines

## Project Structure & Modules
- `CMakeLists.txt` configures JUCE (8.0.12), GoogleTest (1.17.0), shared warnings, and adds the `plugin` and `test` targets.
- `plugin/` holds the audio plug-in: `include/YourPluginName/` for headers, `source/` for implementation, and target wiring in `plugin/CMakeLists.txt`.
- `test/` contains GoogleTest-based unit tests (`source/AudioProcessorTest.cpp`) wired via `test/CMakeLists.txt`.
- `cmake/` carries helper scripts (CPM, warnings, utilities). `libs/` is the CPM download cache. `build/` is the generated build tree (safe to delete/recreate).
- `plugin_codes_used.txt` tracks reserved JUCE `PLUGIN_CODE` values—update when changing codes to avoid collisions.

## Documentation
- When you need JUCE references, use the Context7 MCP docs first: library `/juce-framework/juce` (or `/websites/juce` for site content) via `resolve-library-id` → `query-docs`. Avoid generic web search.

## Build, Test, and Development Commands
- Configure: `cmake -S . -B build` (adds JUCE/GoogleTest via CPM into `libs/`).
- Build: `cmake --build build` (produces plug-in targets under `build/` and artefacts per generator).
- Run tests: `ctest --output-on-failure --test-dir build` after a build.
- Regenerate with custom cache: `cmake -S . -B build -DCPM_SOURCE_CACHE=<path>` to share dependencies across projects.

## Coding Style & Naming Conventions
- C++20 across targets; warnings-as-errors are enforced via `PROJECT_WARNINGS_CXX`.
- Prefer two-space indentation and brace placement consistent with existing JUCE files.
- Keep public headers in `include/YourPluginName/`; mirror names in `source/`.
- Update `juce_add_plugin` fields (`COMPANY_NAME`, `PLUGIN_CODE`, `PRODUCT_NAME`) and rename `YourPluginName` folders/namespaces to match the final plug-in name.

## Testing Guidelines
- Tests use GoogleTest (`GTest::gtest_main`). Add new cases under `test/source/` and register sources in `test/CMakeLists.txt`.
- Name tests with clear fixtures (e.g., `AudioProcessorTest.GeneratesSilenceOnReset`). Keep fast, deterministic, and host-agnostic.
- Run `ctest` from the build tree after adding tests; ensure new behavior is covered when altering DSP or MIDI paths.

## Commit & Pull Request Guidelines
- No history yet—use short, imperative commit subjects (e.g., `Add MIDI input handling`).
- Include: what changed, why, and how to test (commands or steps). Link issues if applicable and add screenshots/recordings for UI-facing audio editors when relevant.
- For changes to plug-in identity, note updated `PLUGIN_CODE` and entries added to `plugin_codes_used.txt`.
