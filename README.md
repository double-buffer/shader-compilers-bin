# Shader Compilers Binaries

This repository contains Releases for the latest stables binaries of different shader compilers for multiple platforms.

It currently provides:

- DirectXShaderCompiler
- SPIRV-Cross

**Important**

Please note that the MacOS versions of DirectXShaderCompiler doesn't contain dxil library. It means it is not possible to compile DXIL shaders that are signed (They will not run on a prod Windows install). You can use it however to compile HLSL to SPIRV and to transcompile it to something else.
