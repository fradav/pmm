CMakeCM
----------

If `CMakeCM` is provided, PMM will download and make available the [CMake
Community Modules](https://github.com/AnotherFoxGuy/CMakeCM) for you project.

Once the `pmm()` function is run, you may `include` or `find_package` any of the
modules provided by `CMakeCM`.

You must also specify either `ROLLING` or `FROM <base-url>` to use CMakeCM with
PMM:

### ROLLING
If you specify `ROLLING`, PMM will download the latest version of the CMakeCM
module index every time you configure (with a few minutes of cooldown).
```cmake
pmm(CMakeCM ROLLING)
```
  
  ### FROM
If you specify `FROM`, the module index will only be obtained from the given
base URL. **Note:** This URL *is not* the URL of a `CMakeCM.cmake` file: It
is a url that *prefixes* the `CMakeCM.cmake` module URL. 
```cmake
pmm(CMakeCM FROM <base-url>)
```
  
## Example 

This is a minimal example that adds [cotire](https://github.com/sakra/cotire) to the dummy exe

```cmake
pmm(CMakeCM ROLLING)

include(cotire)

add_executable(dummy-exe main.cpp)
cotire(dummy-exe)
```