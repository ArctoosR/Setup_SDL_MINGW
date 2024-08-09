# Setup_SDL_MINGW
Install_SDL2


How to Setup SDL2 on Windows for C/C++
This tutorial will go through the process of setting up the SDL2 library on Windows for C/C++ development with mingw-w64, which is a port of the GCC compiler for Windows.


Our example will be written in C using a 64-bit compiler but this works exactly the same for C++ and one could easily use a 32-bit compiler instead.

Step 1: Installing mingw-w64
The first step is to download mingw-w64, and during the install, make sure to install the 64-bit compiler x86_64, as shown below.

![Preview](https://github.com/ArctoosR/Setup_SDL_MINGW/blob/main/01.png)

After the installer is done we need to add the mingw directory to PATH.

Open the start menu and search for "Edit the system environment variables" -> click "Environment Variables" -> select "Path" under System variables and click "Edit" -> add mingw64\bin

![Preview](https://github.com/ArctoosR/Setup_SDL_MINGW/blob/main/02.png)

Now we can make sure everything works correctly by opening cmd and typing in the gcc command.

![Preview](https://github.com/ArctoosR/Setup_SDL_MINGW/blob/main/03.png)

Step 2: Installing SDL2
Go to the SDL2 download page and download the latest development library for Windows using MinGW.

![Preview](https://github.com/ArctoosR/Setup_SDL_MINGW/blob/main/04.png)


After extracting the contents using for example 7-Zip, copy the folder "x86_64-w64-mingw32", to where you want to store the library.
Note that this is still the 64-bit version of the library.

![Preview](https://github.com/ArctoosR/Setup_SDL_MINGW/blob/main/05.png)


This folder contains the include- and library files needed for compiling, as well as the SDL2.dll file that we need to distribute along with the final compiled .exe file.
For the sake of this tutorial, we will rename this folder SDL2 and copy it into our project folder C:\Tutorial (which only has an empty main.c file).


Now go into the SDL2/bin folder and copy the SDL2.dll file to where your main.c file is located (or main.cpp if you are writing in C++).

![Preview](https://github.com/ArctoosR/Setup_SDL_MINGW/blob/main/06.png)

![Preview](https://github.com/ArctoosR/Setup_SDL_MINGW/blob/main/07.png)

Step 3: Creating a Basic C/C++ Program
We will now make a very simple C program that initializes SDL, and then terminates. There are two ways to do this, as illustrated below.

![Preview](https://github.com/ArctoosR/Setup_SDL_MINGW/blob/main/08.png)

The method on the left is the recommended way, and is what we will use. Because of the way SDL works, the main method should be written as:

int main(int argc, char* argv[])
{
...
}

If it's not on this form, we have to define the macro SDL_MAIN_HANDLED before including the SDL.h header.


We are now ready to compile our main.c program, so open up cmd and go to the project directory. We then compile it with the following command:

gcc -std=c17 main.c -I{Path to SDL2\include} -L{Path to SDL2\lib} -Wall -lmingw32 -lSDL2main -lSDL2 -o main

or if we are writing a C++ program:

g++ -std=c17++ main.cpp -I{Path to SDL2\include} -L{Path to SDL2\lib} -Wall -lmingw32 -lSDL2main -lSDL2 -o main

This will create a main.exe file in the project directory.


![Preview](https://github.com/ArctoosR/Setup_SDL_MINGW/blob/main/09.png)



As we can see everything works. Now some explanation about the flags.
-std=c17 means that the compiler uses the most recent C standard, ISO/IEC 9899:2018, known as both C17 and C18. Because of this, the flag -std=c18 is equivalent. Worth noting is that C17 was pretty much a bugfix version of C11, and the fixes are also applied to C11 in GCC - so the only difference from using -std=c11 is the value of __STDC_VERSION__.
See also: GCC Language Standards for C


-I is for include and -L is for linking the library.


-Wall enables many compiler warning messages, it is not required but it is recommended. Also recommended is adding the -Wextra tag for more warnings, which we skip in this tutorial since we are not using the parameters argc and argv[] from int main and would get a warning about that.


-lmingw32 is required, but don't get fooled by the name - we are still compiling a 64-bit program (which you can check by making sure that the value of (8 * sizeof(void *)) is 64).


-lSDL2main and -lSDL2 are also required.

Step 4: A Platformer in C
Now we are done with the setup and can therefore start using SDL2 for development in C/C++, so I will include some example code to get a basic object moving on the screen. Here is platformer.c!

![Preview](https://github.com/ArctoosR/Setup_SDL_MINGW/blob/main/platformer.png)






Run:
gcc -std=c17 main.c -I{Path to SDL2\include} -L{Path to SDL2\lib} -Wall -lmingw32 -lSDL2main -lSDL2 -o main


g++ -std=c17++ main.cpp -I{Path to SDL2\include} -L{Path to SDL2\lib} -Wall -lmingw32 -lSDL2main -lSDL2 -o main


Note:
Building in MSYS2
To build in MSYS2, install the following set of packages with pacman -S --needed:

pacman -S git wget mingw-w64-x86_64-gcc mingw-w64-x86_64-ninja mingw-w64-x86_64-cmake make mingw-w64-x86_64-python3 autoconf libtool
