# Setup_SDL_MINGW
Install_SDL2


How to Setup SDL2 on Windows for C/C++
This tutorial will go through the process of setting up the SDL2 library on Windows for C/C++ development with mingw-w64, which is a port of the GCC compiler for Windows.


Our example will be written in C using a 64-bit compiler but this works exactly the same for C++ and one could easily use a 32-bit compiler instead.

Step 1: Installing mingw-w64
The first step is to download mingw-w64, and during the install, make sure to install the 64-bit compiler x86_64, as shown below.

After the installer is done we need to add the mingw directory to PATH.

Open the start menu and search for "Edit the system environment variables" -> click "Environment Variables" -> select "Path" under System variables and click "Edit" -> add mingw64\bin

Now we can make sure everything works correctly by opening cmd and typing in the gcc command.



Step 2: Installing SDL2
Go to the SDL2 download page and download the latest development library for Windows using MinGW.




After extracting the contents using for example 7-Zip, copy the folder "x86_64-w64-mingw32", to where you want to store the library.
Note that this is still the 64-bit version of the library.



Run:
gcc -std=c17 main.c -I{Path to SDL2\include} -L{Path to SDL2\lib} -Wall -lmingw32 -lSDL2main -lSDL2 -o main


g++ -std=c17++ main.cpp -I{Path to SDL2\include} -L{Path to SDL2\lib} -Wall -lmingw32 -lSDL2main -lSDL2 -o main
