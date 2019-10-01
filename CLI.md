pmm-cli (Helper Commands)
------------

Executing PMM in script mode provides some additional helper commands to work
with your project.

> [!NOTE]
> On windows, replace `./pmm-cli.sh` with `pmm-cli.bat`

## Help
Get help with the `/Help` option:

```shell
./pmm-cli.sh /Help
```

## GenerateShellScript
(Re)generate a pmm-cli.sh and pmm-cli.bat script for calling PMM helper commands

```shell
./pmm-cli.sh /GenerateShellScript 
```

## Conan
Perform a Conan action

### Install
Ensure that a Conan executable is installed.
```shell
./pmm-cli.sh /Conan /Install 
```
#### Upgrade
If `/Upgrade` is provided, will attempt to upgrade an existing installation
```shell
./pmm-cli.sh /Conan /Install /Upgrade
```

### Uninstall
Remove the Conan installation that PMM may have created
(necessary for Conan upgrades)
```shell
./pmm-cli.sh /Conan /Uninstall 
```

### Rebuild
Force rebuilds a package by name
```shell
./pmm-cli.sh /Conan /Rebuild <package name> 
```

### UpdatePackages
Check for updates for Conan packages
```shell
./pmm-cli.sh /Conan /UpdatePackages 
```

### Clean
Removes temporary source and build folders in the local conan cache.
```shell
./pmm-cli.sh /Conan /Clean 
```

### Version
Print the Conan version
```shell
./pmm-cli.sh /Conan /Version 
```

### Export 
Run `conan export . <ref>`.

With `/Upload`, will also upload the package after export.
```shell
/Conan /Export /Ref my-user/unstable /Remote some-remote
```

### Create
Run `conan create . <ref>`.

With `/Upload`, will also upload the package after creation.
```shell
/Conan /Create /Upload /Ref my-user/unstable /Remote some-remote
```

### Upload 
Upload the current package (should have already been exported).

`<ref>` may be a partial `user/channel` reference. In this case the full
ref will be obtained using the project in the current directory.
```shell
/Conan /Create /Upload /Ref my-user/unstable /Remote some-remote
```