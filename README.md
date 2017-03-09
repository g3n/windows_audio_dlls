# Audio libraries for Windows

The G3N engine audio support currently depends on the following external libraries:

- openal        - for spatial audio
- libogg        - for Ogg container format
- libvorbis     - for vorbis decoder support
- libvorbisfile - for reading/decoding ogg vorbis files

These libraries are easily installed in Linux systems using the distribution package manager.

For Windows you can build these libraries from sources using the following procedure
or if you are a trusting person you can simply use the dlls in this directory which were
built using this procedure.

In any case, its recommended that you copy these dlls to the directory from which will
run your application and avoid copying them to the Windows system directory.

# Guide for building the Windows audio dlls

1. Download and install *Microsoft Studio Community* from https://www.visualstudio.com/downloads/.
   I am assuming here that *Microsoft Studio 2017* will be used.

2. Download and install *CMake* from https://cmake.org/download/

3. Download *OpenAL* soft from http://kcat.strangesoft.net/openal-releases/openal-soft-1.17.2.tar.bz2
   and decompress it in a folder. You may need a tool to decompress the file such as http://www.7zip.org.
   Alternatively you can clone the git respository: https://github.com/kcat/openal-soft
   and checkout the latest tagged release:
   ```
   >git checkout tags/openal-soft-1.17.2
   ```

4. Execute the *Developer Command Prompt for VS2017* installed by *Microsoft Visual Studio*.
   It is a command prompt window with environment variables correctly initialized to use
   the MS compiler and tools.

5. In the command prompt change to the build directory inside the *OpenAL* directory.
   Then execute one the of following commands depending on your platform architecture.
   ```
   >cmake -G "Visual Studio 15 2017 Win64" ..   # To build 64 bit dll OR`
   >cmake -G "Visual Studio 15 2017" ..         # To build 32 bit dll`
   ```
   It is important to check in the messages generated by *CMake* if *OpenAL* will be built
   using *DirectSound*.
   If everything is OK, a file *OpenAL.sln* should have been generated in this
   directory between many others.

6. Execute *Visual Studio* and from its menu, select *Open -> Project/Solution...*
   Selects the file *OpenAL.sln* generated previously by *CMake*.
   In the *Visual Studio* tool box, below the menu, select the build mode *Release*. 
   Also in the tool box select the desired architecture: Win32 or x64.
   Then select the menu *Build -> Build Solution* to start the build.
   If everything is OK, the *OpenAL.dll* file should be in the directory `build/Release`.
    
7. Download *libogg* and *libvorbis* from https://xiph.org/downloads/.
   We used the versions:
   - http://downloads.xiph.org/releases/ogg/libogg-1.3.2.zip and
   - http://downloads.xiph.org/releases/vorbis/libvorbis-1.3.5.zip

8. Decompress both files in a directory and rename the decompressed
   directories names removing the version sufix:
   ```
   rename libogg-1.3.2 libogg
   rename libvorbis-1.3.5 libvorbis
   ```

   It is important that the source for both libraries are decompressed in the same
   directory:
   ```
   + parent_directory
      + libogg
         + doc
         + include
         ...
      + libvorbis
         + doc
         + include
         ...
   ```
   *libvorbis* depends on *libogg* and its build system assumes this directory configuration.

9. Execute *Visual Studio* and from its menu select *Open -> Project/Solution...*.
   Select the file `libogg\win32\VS2010\libogg_dynamic.sln`.
   In the Visual Studio tool box, below the menu, select the build mode *Release*. 
   Also in the tool box select the desired architecture: Win32 or x64.
   Then select the menu *Build -> Build Solution* to start the build.
   If during the build *Visual Studio* indicates an error related to
   the installed platform toolset you may need to retarget the solution,
   selecting the menu *Project -> Retarget solution"* and then try the build again.
   If everything is OK, then `libogg.dll` file should be in the directory:
   `libogg\win32\VS2010\x64\Release` for 64 bits or
   `libogg\win32\VS2010\Win32\Release` for 64 bits or

10. Execute *Visual Studio* and from its menu select *Open -> Project/Solution...*.
   Select the file `libvorbis\win32\VS2010\vorbis_dynamic.sln`.
   In the *Visual Studio* tool box, below the menu, select the build mode *Release*. 
   Also in the tool box select the desired architecture: Win32 or x64.
   Then select the menu *Build -> Build Solution* to start the build.
   If during the build *Visual Studio* indicates an error related to
   the installed platform toolset you may need to retarget the solution,
   selecting the menu *Project -> Retarget solution"* and then try the build again.
   If everything is OK, then `libvorbis.dll` and `libvorbisfile.dll` should be in the directory:
   `libvorbis\win32\VS2010\x64\Release` for 64 bits or
   `libvorbis\win32\VS2010\Win32\Release` for 64 bits or

11. Copy the dlls: `OpenAL32.dll, libogg.dll, libvorbis.dll` and `libvorbisfile.dll`
    to the directory from which you will execute a G3N application.



