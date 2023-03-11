# ODL Wayfinder Interface

An interface for connecting to the Ocean Discovery League Wayfinder system, setting up operations, and transferring data.

## Instructions for Environment Setup:
1. Download [Qt Online Installer](https://www.qt.io/download-qt-installer?utm_referrer=https%3A%2F%2Fwww.qt.io%2Fdownload-open-source%3Futm_referrer%3Dhttps%253A%252F%252Fwww.qt.io%252Fdownload)
2. Run Qt installer, select open source development under LGPL license
3. Install additional libraries: [add here]
5. Open Qt Creator
6. File --> New Project --> Import Project --> Git Clone --> Choose...
7. Add repository URL (https://github.com/ArianeChriss/ODL-Wayfinder-Interface.git)

_*Note: if committing changes from a not-mine system, add build folders to the repository .gitignore file_

## For Development:
Interface frontend is done in main.qml, with functions being called from main.cpp and any other C++ source files. Any images or other resources need to be added in qml.qrc.

QML: [Qt Tutorial](https://doc.qt.io/qt-6/qml-tutorial.html)
### For adding C++ functions to QML:
1. Create C++ .cpp and .h files ([helpful forum post for formatting](https://forum.qt.io/topic/33170/call-c-function-from-qml/2) _*Note: type registration is for using an old version of qmake, for cmake ignore any suggested edits to the main.cpp file and use [this](https://www.qt.io/blog/introduction-to-the-qml-cmake-api), explained in step 2._)

2. Define function file version and use in CMakeLists.txt:
    ```
    qt_add_qml_module(ProjectName
        URI MyFunctions
        VERSION 1.0
        QML_FILES main.qml)
        SOURCES
            MyFunctions.h MyFunctions.cpp
    ```
3. Add import statement with version to top of main.qml:

    `import MyFunctions 1.0`

4. Add .h and .cpp files to qml.qrc file. This applies to **all resource files**, they cannot simply be in the same directory, they need to be manually added to the project.
    
_*Note: Sometimes changes to certain files don't take effect until Cmake is rerun. Clean project (Build --> Clean), Run Cmake, and Rebuild._

## For Building:

__Make sure you're building with MSVC2019 64 bit, if on Windows. WebEngine is not supported by MinGW.__