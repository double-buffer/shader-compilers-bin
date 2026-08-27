# Shader Compilers Binaries

This repository builds and publishes consistent shader compiler packages for the platforms used by Elemental.

It currently provides:

- DirectXShaderCompiler (Windows x64, Linux x64, macOS arm64)
- SPIRV-Cross (Windows x64, Linux x64, macOS arm64)
- Apple Metal Shader Converter (Windows x64, macOS arm64)

DirectXShaderCompiler is built from source on every platform because upstream DXC still does not publish macOS binaries. Building all platforms from the same source revision also keeps the package layout and compiler revision consistent.

Metal Shader Converter is distributed by Apple behind the Apple Developer downloads login, so the source installers cannot be fetched unattended by GitHub Actions. The repository keeps the remaining work automated:

1. Run the **Import Metal Shader Converter** workflow once. If needed, it creates a draft release named `metal-shader-converter-source` that acts as a temporary inbox.
2. Download the macOS and Windows Metal Shader Converter packages from Apple and upload both files to that draft release.
3. Run **Import Metal Shader Converter** again with the converter version and the exact two uploaded filenames.
4. The workflow extracts the Apple installers, normalizes the `include/` and `lib/` package layout, validates the macOS arm64 library, and uploads the resulting packages to the latest published release (or a release tag supplied manually).
5. The temporary Apple installer assets are removed from the draft inbox after a successful import.

Published releases automatically carry the latest Metal Shader Converter packages forward, so a DXC or SPIRV-Cross update does not require another Apple download unless Metal Shader Converter itself changes.

**Important**

The DXC and SPIRV-Cross binaries built by this repository are not officially supported by Microsoft or Khronos. Metal Shader Converter is Apple software redistributed here for Elemental's build tooling; its use remains subject to Apple's applicable terms.
