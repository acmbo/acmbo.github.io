## Setup VSCode and C++ on Linux

- Install VSCode on Ubuntu via Software Shop
- Here is a very good article on setting up VSCode on Linux: https://code.visualstudio.com/docs/cpp/config-linux


```
sudo apt-get update
sudo apt-get install build-essential gdb
sudo apt-get install cmake
```

This will install dependecies like gcc and g++, and GNU debbuger.

Install the following plugin in VSCode:
- C/C++ for Visual Studio Code by Microsoft
- C/C++ Extension Pack for Visual Studio Code by Microsoft
- CMake Tools by Microsoft

### Setting up a C++ Project

- Use the C++ tempaltes uploaded here: https://github.com/acmbo/cpp_templates_byChristoph
- These are CMake presets configured for multiple OS Systems
- VSCode has to be openend on the same level, as the first CMakeLists.txt appears. The template is structured like this, that its on the same level as 'src'.

```
root
  - template_project
      - Development    <- open VSCode here
        - build
        - src
      - ThirdParty
```

- To run Cmake specifiy the cmake path. Got in VScode to File -> Preferences -> Settings -> Cmake Path to `/usr/bin/cmake` (Check beforehand if its there. Otherwise install again with sudo ap install)
