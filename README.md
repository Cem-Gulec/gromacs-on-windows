Gromacs on windows (ver 2018.8)
=====================
While I was searching for how to compile gromacs on windows, I came across with some solutions but they were not that complete. So, I figured maybe this would be helpful.
FYI: It may fail on the versions of 2019. For me it works successfully at version 2018.8.
Requirements: Microsoft Visual Studio, Cmake, an unpacking tool, Cygwin

Unpacking Tar File
=====================
There are plenty of softwares such as tar, 7-zip, TarTools. But for me 7-zip was the easiest one to use.
You can find the [detailed information](https://wiki.haskell.org/How_to_unpack_a_tar_file_in_Windows)

How to Build
=====================
[CMake](http://www.cmake.org) for building the system. To build it, follow these steps:

1. For the section "Where is the source code": specify your unpacked gromacs file (example: /Gromacs/gromacs-2018.8). And for the section "Where to build the binaries": you can create a new directory such as Gromacs/gromacs-2018.8/build

2. Press "Configure" and just select the version of visual studio you own in your pc.

3. Configuring might take a while but after it finishes you'll come up with some specified errors. At this step, from the "GMX" section, you need to find "GMX_FFT_LIBRARY". Change its value from "fftw3" to "fftpack". Then configure again.

4. After configuration is done, one last thing to do: From the "CMAKE" section, change "CMAKE_INSTALL_PREFIX"'s value to a new directory name such that: ( Gromacs/gromacs_2018.8_verbuilded ). Then configure again.

5. After configuration is done, you should be able to "Generate" files without any errors. Press "Generate" button.

6. If you have come to this step without any error, you at "/Gromacs/gromacs-2018.8/build" there is a file named "Gromacs.sln". In order to open it you require Microsoft Visual Studio.

7. This step probably the longest one takes to compile, so be patient. After opening the "Gromacs.sln" via MVS, as in the image compile "gmx".

8. After you compiling "gmx", you may come up with an error "'\_BitScanReverse64': identifier not found". You may be able to solve it just by changing "\_BitScanReverse64" into "\_BitScanReverse" from the specified error location code line. Or "intrin.h" library- which contains the "\_BitScanReverse" function may not be existing.

9. Compile "INSTALL"

10. Last thing I want to mention is that: some command words are based for Unix systems and will not work at Windows. At this case, you need to install cygwin packages to handle this. Packages you may need: gcc-core, make, openssl, ssh, ftp, python, libfftw3. 

11. After installing all packages you need to add cygwin path into: Environment Variables > System Variables > Path

Other Options Without CMake or Cygwin
=====================
* You may also handle it without any of these and just by installing Ubuntu subsystem. At that case, I have attached the packages you may need at "requirements.txt".
