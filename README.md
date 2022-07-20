# build-unity

GitHub Action to build Unity project.

Works on Ubuntu, macOS and Windows.

This fork of [kuler90/build-unity](https://github.com/kuler90/build-unity).
Default build method was removed. Unity on build activation added ( to give unity ability to upload symbols/dSym files on build ).

## Inputs

### `unity-path`

Path to Unity executable. `UNITY_PATH` env will be used if not provided.

### `project-path`

Path to Unity project. Used to find Unity version. Default `${{ github.workspace }}`.

### `build-target`

**Required** Build target platform.

### `build-path`

Path to build output. Only for default build method.

### `build-version`

Set application version. Only for default build method.

### `build-number`

Set application build number. Only for default build method.

### `build-defines`

Set scripting define symbols. For example, `RELEASE_VERSION;ENG_VERSION`. Only for default build method.

### `build-options`

List of additional [BuildOptions](https://docs.unity3d.com/ScriptReference/BuildOptions.html). For example, `SymlinkLibraries, CompressWithLz4HC`. Only for default build method.

### `unity-username`

Unity account user name.

### `unity-password`

Unity account user password.

### `unity-serial`

Unity account serial key.

### `build-method`

Path to build method. For example, `MyEditorScript.PerformBuild`. Default build method will be used if not provided.

### `build-method-args`

Custom arguments for build method.

## Outputs

### `build-path`

Path to build output.

## Example usage

```yaml
- name: Checkout project
  uses: actions/checkout@v2

- name: Setup Unity
  uses: kuler90/setup-unity@v1
  with:
    unity-modules: android ios

- name: Build Unity
  uses: TiltingPoint/build-unity-github-action@v1.0.6
  with:
    build-target: Android
    build-path: ./build.apk
    build-method: MyBuilder.Build
    build-method-args: -someParameter "someValue"
```