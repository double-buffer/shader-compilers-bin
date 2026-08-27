# Shader Compilers Binaries

This repository builds and publishes consistent shader compiler packages for the platforms used by Elemental.

It currently provides:

- DirectXShaderCompiler (Windows x64, Linux x64, macOS arm64)
- SPIRV-Cross (Windows x64, Linux x64, macOS arm64)
- Apple Metal Shader Converter (Windows x64, macOS arm64)

DirectXShaderCompiler is built from source on every platform because upstream DXC still does not publish macOS binaries. Building all platforms from the same source revision also keeps the package layout and compiler revision consistent.

Metal Shader Converter is distributed by Apple behind the Apple Developer downloads login, so the source installers cannot be fetched unattended by GitHub Actions. Everything around that authenticated download is automated:

1. **Check Metal Shader Converter** runs weekly and reads the current download version from Apple's public Metal Shader Converter page.
2. If that version is not already packaged in the latest release, the workflow opens an issue and creates a temporary draft release named `metal-shader-converter-source`.
3. Download the macOS and Windows Metal Shader Converter packages from Apple and upload both original files to that draft release.
4. Run **Import Metal Shader Converter** with only the converter version. The workflow identifies the macOS and Windows assets automatically from their filenames/extensions.
5. The workflow extracts the Apple installers, normalizes the `include/` and `lib/` package layout, validates the macOS arm64 library, and uploads the resulting packages to the latest published release (or a release tag supplied manually).
6. After a successful import, the temporary draft release is deleted completely and the update issue is closed automatically.

The import workflow can still be run manually before the checker notices an update. If the source inbox does not exist yet, its first run creates it; upload the two Apple packages and rerun the import with the same version.

Published releases automatically carry the latest Metal Shader Converter packages forward, so a DXC or SPIRV-Cross update does not require another Apple download unless Metal Shader Converter itself changes.

**Important**

The DXC and SPIRV-Cross binaries built by this repository are not officially supported by Microsoft or Khronos. Metal Shader Converter is Apple software redistributed here for Elemental's build tooling; its use remains subject to Apple's applicable terms.
