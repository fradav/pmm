Conan
----------

In `CONAN` mode, PMM will find, obtain, and use Conan to manage project
packages.

PMM will always use the `cmake` Conan generator, and will define imported
targets for consumption (Equivalent of `conan_basic_setup(TARGETS)`). It will
also set `CMAKE_PREFIX_PATH` and `CMAKE_MODULE_PATH` for you to use
`find_package()` and `include()` against the installed dependencies.

> [!NOTE]
> No other CMake variables from regular Conan usage are defined.

`CONAN` mode requires a `conanfile.txt` or `conanfile.py` in your project
source directory. It will run `conan install` against this file to obtain
dependencies for your project.

The nitty-gritty of how PMM finds/obtains Conan:

1. Check for the `CONAN_EXECUTABLE` variable. If found, it is used.
2. Try to find a `conan` executable. Searches:
    1. Any `pyenv` versions in the user home directory
    2. `~/.local/bin` for user-mode install binaries
    3. `C:/Python{36,27,}/Scripts` for Conan installations
    4. Anything else on `PATH`
3. If still no Conan, attempts to obtain one automatically, trying first
   Python 3, then Python 2:
    1. Check for a `venv` or `virtualenv` executable Python module.
    2. Create a user-local virtualenv.
    3. Installs Conan *within the created virtualenv* and uses Conan from there.
    
> [!WARNING]
> While PMM will ensure that Conan has been executed for you as part of your
  configure stage, it is up to you to provide a Conanfile that Conan can consume
  to get your dependency information.
> 
> You will still need to read the Conan documentation to understand the basics of
  how to declare and consume your dependencies. 


### SETTINGS
Set additional --setting flags
```cmake
pmm(CONAN SETTINGS ...)
```
### OPTIONS 
Set additional --option flags
```cmake
pmm(CONAN OPTIONS ...)
```
### BUILD 
Set the conan --build option. (Default is `missing`)
```cmake
pmm(CONAN BUILD <policy>)
```
### PROFILE 
Use a custom profile instead of the auto-generated profile created by PMM
```cmake
pmm(CONAN PROFILE <profile-name>)
```
### REMOTES
Ensure remotes are present before installing
```cmake
pmm(CONAN REMOTES [<name>[::no_verify] <url> [...]])
```
#### BINCRAFTERS
Enable the Bincrafters repository
```cmake
pmm(CONAN REMOTES BINCRAFTERS)
```
#### COMMUNITY
Enable the conan-community repository
```cmake
pmm(CONAN REMOTES COMMUNITY)
```
## Example 

This is a minimal example that adds Catch2 to the dummy target

```cmake
pmm(CONAN)

add_executable(dummy main.cpp)
target_link_libraries(dummy PRIVATE CONAN_PKG::Catch2)

add_test(dummy dummy)
```