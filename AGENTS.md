# AGENTS.md

ESP32 firmware (ESP-IDF v6.1, target `esp32`), project name `ESP32Compass`. Entry point: `main/main.c` (`app_main`).

## Build
- Requires an ESP-IDF v6.1 environment (`IDF_PATH` set). Devcontainer provides one at `/opt/esp/idf`.
- `idf.py build`
- Flash + monitor: `idf.py -p <PORT> flash monitor`
- `sdkconfig` is a generated, gitignored file and there is no `sdkconfig.defaults`; do not delete it without saving config (`idf.py menuconfig`).
- `build/` artifacts here came from a macOS host (paths under `/Users`/`/Volumes`); regenerate locally.

## Components
- Managed components are vendored under `components/ESP32ManagedComponents/` (`espressif__cjson`, `espressif__mqtt`).
- They are not auto-discovered by IDF (no `CMakeLists.txt` at that directory). To use them, set `EXTRA_COMPONENT_DIRS` to that path before `project()` in root `CMakeLists.txt`, or move the subdirs into `components/`.

## Tooling
- `build/compile_commands.json` drives clangd; `.clangd` strips `-f*`/`-m*` flags.
- No project tests exist.
