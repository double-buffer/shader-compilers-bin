# Shader Compilers Binaries

This repository contains Releases for the latest stables binaries of different shader compilers for multiple platforms.

It currently provides:

- DirectXShaderCompiler
- SPIRV-Cross

**Important**

Please note that the MacOS version of DirectXShaderCompiler doesn't contain dxil library. So it means it is not possible to compiler DIXL shaders that are signed. You can use it however to compile to SPIRV and to transcompile it to something else.
