vcpkg
----------
> [!WARNING]
> You will need `std::filesystem` or `std::experimental::filesystem` support from your
compiler and standard library.

In `VCPKG` mode, PMM will download the vcpkg repository at the given
`REVISION`, build the `vcpkg` tool, and manage the package installation in a
use-local data directory.

When using PMM, you do not need to use the `vcpkg.cmake` CMake toolchain
file: PMM will take care of this aspect for you.

After calling `pmm(VCPKG)`, all you need to do is `find_package()` the
packages that you want to use. 

### REVISION
`REVISION` should be a git tree-ish (A revision number (preferred), branch,
or tag) that you could `git checkout` from the vcpkg repository. PMM will
download the specified commit from GitHub and build the `vcpkg` command line
tool from source. 

> [!TIP]
> I recommend using the latest release as revision tag  
> https://github.com/microsoft/vcpkg/releases

```cmake
# Specify the revision of vcpkg that you want to use (required)
pmm(VCPKG REVISION <rev>)
```

### REQUIRES
`REQUIRES` is a list of packages that you would like to install using the
`vcpkg` command line tool.
```cmake
# Ensure the given packages are installed using vcpkg
pmm(VCPKG REQUIRES  [req [...])
```

### PORTS
 If you want to copy custom ports to the vcpkg ports folder, you can define `PORTS` with a list of folders to copy over.
```cmake
# Copy custom ports to the vcpkg ports directory
pmm(VCPKG PORTS [path to port dir [...]])
```   


## Example

This is a minimal example that adds Catch2 to the dummy target

```cmake
pmm(VCPKG
    REVISION 2019.07
    REQUIRES catch2
)

find_package(Catch2 CONFIG REQUIRED)

add_executable(dummy main.cpp)
target_link_libraries(dummy PRIVATE Catch2::Catch2)
```   

