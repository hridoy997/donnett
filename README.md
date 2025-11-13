# Donnett — ASCII Donut (C)

Small C program that renders the rotating ASCII donut in the terminal.

Contents

- `main.c` — the donut program source.
- `bin/Debug/donnett.exe`, `output/main.exe` — compiled binaries (if present in repo).

Quick notes

- The code uses the math library and a usleep call for timing.
- The program prints ANSI escape sequences; run it in a terminal that supports ANSI (PowerShell 7, WSL, MSYS2, or a Linux terminal).

Build & run (recommended)

1. On Windows using MSYS2 / MinGW-w64 (recommended for native Windows build):

```powershell
# open an MSYS2 MinGW 64-bit shell and run
gcc main.c -o output/main.exe -lm
# then run
./output/main.exe
```

Note: `usleep()` is a POSIX function and may not be available in some native Windows toolchains. If you get a linker error referencing `usleep`, either build inside WSL or MSYS2 which provides `usleep`, or modify `main.c` to use the Windows `Sleep()` function (see troubleshooting below).

2. On WSL / Linux (works out-of-the-box):

```bash
gcc main.c -o donut -lm
./donut
```

Troubleshooting

- If you see compile errors for `usleep`: replace the call with the Windows Sleep function (milliseconds). Example change:

  - Add at top: `#ifdef _WIN32\n#include <windows.h>\n#else\n#include <unistd.h>\n#endif`
  - Replace `usleep(30000);` with `#ifdef _WIN32\nSleep(30);\n#else\nusleep(30000);\n#endif`
  - When using `Sleep()` include `#include <windows.h>` and link normally.

- If the terminal doesn't render animation or shows weird characters: use a terminal with ANSI support. Windows 10/11 PowerShell (v7+) or Windows Terminal usually work.

Credits

- This program implements the classic rotating ASCII donut (popular small demo). Code inspired by widely circulated implementations of the "ASCII donut".

License

- No license file in this repo. Add one if you want to set usage terms.

How to commit this README (example)

```powershell
cd "g:\Programing\C PROJECT\donnett"
# stage the new file
git add README.md
# create a commit with a concise message
git commit -m "Add README with build and run instructions"
```

If you want, I can create the commit for you (or stage additional files). Tell me the commit message to use or say "use default".
