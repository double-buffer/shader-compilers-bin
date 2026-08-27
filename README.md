# Shader Compilers Binaries

This repository builds and publishes consistent shader compiler packages for the platforms used by Elemental.

It currently provides:

- DirectXShaderCompiler (Windows x64, Linux x64, macOS arm64)
- SPIRV-Cross (Windows x64, Linux x64, macOS arm64)

DirectXShaderCompiler is built from source on every platform because upstream DXC still does not publish macOS binaries. Building all platforms from the same source revision also keeps the package layout and compiler revision consistent.

**Important**

These compiled binaries are not officially supported by Microsoft or Khronos.
