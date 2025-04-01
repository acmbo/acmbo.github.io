## Setup VSCode and C++ on Linux


- Install VSCode on Ubuntu via Software Shop
- Here is a very good article on setting up VSCode on Linux: https://code.visualstudio.com/docs/cpp/config-linux


```
sudo apt-get update
sudo apt-get install build-essential gdb
sudo snap install cmake #--classic
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

- To run Cmake specifiy the cmake path. Got in VScode to File -> Preferences -> Settings -> Cmake Path to `/snap/cmake/current/bin/cmake` (Check beforehand if its there. Otherwise install again with sudo ap install)
- Setup the CMakeLists.txt file correctly:
  - Remove all not installed or unused ThirdParty Libaries.
  - Make sure that 'add_executable' is set.
- In the CMake plugin on the site of VSStudio, you should be able to see the Cmake plugin (If your VScode opens the folder on the same level)
- Now you should be able to configure the CMake plugin, that you can start build, Debug and Launch 
