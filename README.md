# paraview-chm
A custom built Paraview for support with datetime visualization

This requires `cmake` and `conan` to be installed. The following assumes they are available on the path.

![](output.gif)


# Clone repository
To build, check out this repository and recursively initialize the submodles

```
git clone --recursive  https://github.com/Chrismarsh/paraview-chm.git

```

# Build dependencies
Run
```
python init_conan.py
```
to move the paraview and boost dependencies to the local conan cache. If you have already built CHM, then the boost depdency is already present.

Create a seperate build directory seperate from the git repository and then install the conan dependencies

```
mkdir build
conan install <path to git repository> -if=. --build missing

```
# Build filter
Still in the `build` folder used above, 

```
cmake <path to git repository> -DCMAKE_TOOLCHAIN_FILE=./conan_paths.cmake
make install
```

# Final steps
This will produce a `lib/` directory in the build folder with the filter library. As a final step run

```
conan install <path to git repository> -if=./paraview

```
which will create a local copy of the built paraview in `paraview/paraview/bin`