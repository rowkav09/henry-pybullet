# Windows build instructions for Bullet3 / PyBullet

These steps build the Python wheel for a newer Python, such as Python 3.13, on Windows.

## Prerequisites

Install these first:

- Python 3.13.x from python.org
- Visual Studio 2022 Build Tools
- The "Desktop development with C++" workload
- MSVC v143 build tools
- Windows 10 or Windows 11 SDK

Verify the compiler is available before building:

```powershell
cl
```

If that prints the MSVC compiler banner, the toolchain is ready.

## Build steps

1. Clone the repository:

```powershell
git clone https://github.com/bulletphysics/bullet3.git
cd bullet3
```

2. Upgrade the Python packaging tools for the Python version you want to build with:

```powershell
py -3.13 -m pip install -U pip build hatchling setuptools
```

3. Build the wheel:

```powershell
py -3.13 -m pip wheel . -w dist
```

If you want to skip the native compile step temporarily and only test packaging, set:

```powershell
$env:PYBULLET_SKIP_NATIVE_BUILD='1'
py -3.13 -m pip wheel . -w dist
```

## Notes

- Use the same Python version for both the build and the wheel target.
- The build must be done with a working C++ compiler; without MSVC, the pybullet extension cannot compile.
- If `cl` is not found, open the "x64 Native Tools Command Prompt for VS 2022" or install the C++ workload in Visual Studio Build Tools.
