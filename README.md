# Installing & using vcpkg
<ins> About</ins> <br>

>vcpkg is a free C/C++ package manager for acquiring and managing libraries. 
Choose from over 1500 open source libraries to download and build in a single step or add
your own private libraries to simplify your build process. Maintained by the Microsoft 
C++ team and open source contributors.  
          
## Prerequisites -

    • Windows 7 or newer
    • Visual Studio 2015 Update 3 or newer
    • Visual Studio Code 1.20 2017 or newer
    • Git-Bash

## Install vcpkg

I recommand installing globally, and placing the repo in short install path like: `C:\src\vcpkg` or `C:\dev\vcpkg`, since otherwise you may run into path issues for some port build systems.

### Step 1: Clone the vcpkg repo

```git
git clone https://github.com/Microsoft/vcpkg.git
```

### Step 2: installing vscpkg

in the vscpkg open git-bash and type `.\bootstrap-vcpkg.bat`
this will install vscpkg in the folder

### Step 3: Adding vscpkg command into bash

open git-bash, then type `code .bash_profile`

paste in the code:

```git
#vcpkg
export PATH=$PATH:/c/ProgramData/vcpkg
```

save the file and close the editor

### [Optional] Step 4: add git-bash into Visual Studio

open Visual Studio 2015 Update 3 or newer, click `CTRL` + `` ` `` it will open the integrated terminal, click the cogwheel or gear icon.
make sure it open in Environment > Terminal, click `Add` and input this

```git
Name: Git-Bash
Shell Location: c:\program files\git\bin\bash.exe
Arguments: --login -i
```

the arguments `--login -i` will open our `code .bash_profile`

### Step 5: Add a new package

find a package that you want to use, in this case we going to install GLM

<details>
  <summary>Click To Read About GLM</summary>
  OpenGL Mathematics (GLM) is a C++ mathematics library for graphics software based on the OpenGL Shading Language
</details>

to install this package we will input this command

```git
vcpkg install glm
```
you can find each package installion command by searching it and clicking on the `View Details`

<img src="assets/GLMDetails.gif" align="center" width="50%">


by default vcpkg will install the x86 version if you want the x64 version attach `:x64-windows` in the end of the command like this

```git
vcpkg install glm:x64-windows
```

you can choose other versions
<img style="box-shadow: 0 10px 16px 0 rgba(0,0,0,0.2),0 6px 20px 0 rgba(0,0,0,0.19) !important; border-radius: 8px;" align="center" src="Assets\vscpkg.png" >

### Step 6: Include in your project:
after the installation of the package run the command:
```git
vcpkg integrate install
```
this will enable the global packages to be included in your project

this is the console response 
```git
Applied user-wide integration for this vcpkg root.
CMake projects should use: "-DCMAKE_TOOLCHAIN_FILE=C:/dev/vcpkg/scripts/buildsystems/vcpkg.cmake"

All MSBuild C++ projects can now #include any installed libraries. Linking will be handled automatically. Installing new libraries will make them instantly available.
```

we successfully installed and enabled vcpkg to be use in our project.

now create or go to your project, and include GLM 
```cpp
#include <glm/glm.hpp>
```
 plug in this code to make sure it's working
 ```cpp
int main()
{
    std::cout << "Hello World!\n";
	glm::vec3 a(1.0f, 0.0f, 0.0f);
}

glm::vec3 computeNormal(
    glm::vec3 const& a,
    glm::vec3 const& b,
    glm::vec3 const& c)
{
    return glm::normalize(glm::cross(c - a, b - a));
}
```

Done!


<hr>

Written by <a href="https://www.linkedin.com/in/dorz/">Dor Zairi<a>
