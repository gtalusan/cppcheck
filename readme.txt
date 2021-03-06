=========
Cppcheck
=========


About

    The original name of this program is "C++check" but it was later changed to "cppcheck".

Manual

    A manual is available online:
    http://cppcheck.sourceforge.net/manual.pdf

Compiling

    Any C++ compiler should work.

    To build the GUI, you need Qt.

    When building the command line tool, PCRE is normally used.
    PCRE is optional.

    There are multiple compilation choices:
      * qmake - cross platform build tool
      * Windows: Visual Studio
      * Windows: Qt Creator + mingw
      * gnu make
      * g++

    qmake
    =====
        You can use the gui/gui.pro file to build the GUI.
            cd gui
            qmake
            make

    Visual Studio
    =============
        Use the cppcheck.sln file. The rules are normally enabled.

        To compile with rules (pcre dependency):
            * the pcre dll is needed. it can be downloaded from:
                http://cppcheck.sourceforge.net/pcre-8.10-vs.zip

        To compile without rules (no dependencies):
            * remove the preprocessor define HAVE_RULES from the project
            * remove the pcre.lib from the project

    Qt Creator + mingw
    ==================
        The PCRE dll is needed to build the CLI. It can be downloaded here:
            http://software-download.name/pcre-library-windows/

    gnu make
    ========
        Simple build (no dependencies):
            make

        The recommended release build is:
            make SRCDIR=build CFGDIR=cfg HAVE_RULES=yes

        Flags:
        SRCDIR=build   : Python is used to optimise cppcheck
        CFGDIR=cfg     : Specify folder where .cfg files are found
        HAVE_RULES=yes : Enable rules (pcre is required if this is used)

    g++ (for experts)
    =================
        If you just want to build Cppcheck without dependencies then you can use this command:
            g++ -o cppcheck -Ilib -Iexternals/tinyxml cli/*.cpp lib/*.cpp externals/tinyxml/tinyxml2.cpp

        If you want to use --rule and --rule-file then dependencies are needed:
            g++ -o cppcheck -lpcre -DHAVE_RULES -Ilib -Iexternals cli/*.cpp lib/*.cpp externals/tinyxml/tinyxml2.cpp

    mingw
    =====
        The "LDFLAGS=-lshlwapi" is needed when building with mingw
            mingw32-make LDFLAGS=-lshlwapi

    other compilers/ide
    ===================

        1. Create a empty project file / makefile.
        2. Add all cpp files in the cppcheck cli and lib folders to the project file / makefile.
        3. Compile.

Cross compiling Win32 (CLI) version of Cppcheck in Linux

    sudo apt-get install mingw32
    make CXX=i586-mingw32msvc-g++ LDFLAGS="-lshlwapi"
    mv cppcheck cppcheck.exe

Webpage

    http://cppcheck.sourceforge.net/
