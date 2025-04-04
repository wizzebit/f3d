## Plugins

F3D officially supports plugins for certain file formats. If you installed F3D using the binary
release, there's no need to manually load these plugins when opening your file.
F3D will load them automatically.

However, if you installed F3D using a package manager,
it's possible that the packager chose to bundle the plugins into different packages or
to list plugin dependencies as optional in order to reduce the number of dependencies of the main package.

In order to open a file that requires a plugin, make sure you've installed all necessary
dependencies. You can then specify the `--load-plugins=<path or name>` [option](OPTIONS.md)
in the command line to load your plugin.

Alternatively, you can add your plugin directly in the
[configuration file](CONFIGURATION_FILE.md) if it isn't there already. You can specify one or
multiple plugins in a single comma-separated list, like in the example below:

```
[
{
  "match": ".*(file_extension)",
  "options":
  {
    "load-plugins": "plugin1", "plugin2"
  }
}
]
```

### Supported plugins

F3D supports the following plugins and their file formats:

- **alembic**: `.abc`
- **assimp**: `.fbx`, `.dae`, `.off`, `.dxf`, `.x`, `.3mf`
- **draco**: `.drc`
- **exodus**: `.ex2`
- **occt**: `.step/.stp`, `.iges/.igs`
- **usd**: `.usd`, `.usda`, `.usdc`, `.usdz`
- **vdb**: `.vdb` (experimental)

> Note: If you downloaded the binaries from the release page, it's not necessary to specify manually the plugins above. F3D loads them automatically.

Here is how the plugins are searched (in preceding order):

1. Search the static plugins.
2. Consider the `load-plugins` option given it is a full path.
3. Search in the paths specified in `F3D_PLUGINS_PATH` environment variable.
4. Search in a directory relative to the F3D application: `../lib`.
5. Rely on OS specific paths (e.g. `LD_LIBRARY_PATH` on Linux or `DYLD_LIBRARY_PATH` on macOS).

You can also try plugins maintained by the community. If you have created a plugin and would like it to be listed here, please submit a pull request.

- **Abaqus**: ODB support by @YangShen398 ([repository](https://github.com/YangShen398/F3D-ODB-Reader-Plugin))

### Reader options

Plugins can provide option that can be set using the `-D/--define` [command line option](OPTIONS.md).
eg: `-DVDB.downsampling_factor=0.5`.

Values are parsed as doubles. For booleans, 0 means false, not 0 means true.

- `vdb` - `VDB.downsampling_factor` : Control the level of downsampling when reading a volume, default is 0.1.
- `occt` - `STEP.linear_deflection` : Control the distance between a curve and the resulting tessellation, default is 0.1.
- `occt` - `STEP.angular_deflection` : Control the angle between two subsequent segments, default is 0.5.
- `occt` - `STEP.relative_deflection` : Control if the deflection values are relative to object size, default is false.
- `occt` - `STEP.read_wire` : Control if lines should be read, default is true.
- `occt` - `IGES.linear_deflection` : Control the distance between a curve and the resulting tessellation, default is 0.1.
- `occt` - `IGES.angular_deflection` : Control the angle between two subsequent segments, default is 0.5.
- `occt` - `IGES.relative_deflection` : Control if the deflection values are relative to object size, default is false.
- `occt` - `IGES.read_wire` : Control if lines should be read, default is true.
- `occt` - `BREP.linear_deflection` : Control the distance between a curve and the resulting tessellation, default is 0.1.
- `occt` - `BREP.angular_deflection` : Control the angle between two subsequent segments, default is 0.5.
- `occt` - `BREP.relative_deflection` : Control if the deflection values are relative to object size, default is false.
- `occt` - `BREP.read_wire` : Control if lines should be read, default is true.
- `occt` - `XBF.linear_deflection` : Control the distance between a curve and the resulting tessellation, default is 0.1.
- `occt` - `XBF.angular_deflection` : Control the angle between two subsequent segments, default is 0.5.
- `occt` - `XBF.relative_deflection` : Control if the deflection values are relative to object size, default is false.
- `occt` - `XBF.read_wire` : Control if lines should be read, default is true.
