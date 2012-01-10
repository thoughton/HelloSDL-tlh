This is an Xcode 4 project that draws a colourful triangle to the screen with SDL.

Originally by Ricket (https://github.com/Ricket), forked and modified by thoughton (https://github.com/thoughton).


Ricket's original linked to the SDL framework, this fork links to dylibs instead.

The reasons for the change to dylibs, and for this fork's existence in general, are as follows:


 1. To be able to link to SDL libraries that are build using the makefiles on OSX, which in my (limited) experience seems to be the easiest way to build SDL on OSX

 2. To be able to link to SDL libraries that are installed to non-standard locations, eg. within the home directory structure of the user, so admin rights are not needed for building or installing SDL, or for linking to it

 3. To be able to bundle the libraries inside the app's bundle, and to make the necessary modifications to the app's built Mach-O binary, so that the app can be redistributed and relocated without the need to worry about the location of the user's SDL libraries

 4. To experiment with ways of doing #3 in a manner that is easily able to handle any number of additional non-SDL dylibs, in as simple and as painless a way as possible


To be able to build this code after initial git cloning, you should only need to alter the following two settings in the Target's Build Settings within Xcode:

 
 A. Add to the "Header Search Paths" setting: the directory that contains the "SDL" sub-directory that contains your SDL headers (SDL.h, etc.)

 B. Add to the "Library Search Paths" setting: the directory that contains the "SDL" sub-directory that contains your SDL libraries (libSDL.dylib, etc.)


And that's it. At this point the project should compile without a hitch, and the resulting app should be redistributable and relocatable without a problem.


If you want to add additional dylibs to the project, other than adding another "-lXXX" entry to the "Other Linker Flags" setting so that the linker knows to actually link the library in, all you have to do to also get the dylib bundled in with the built app is just add its name (without version numbers or file extension) to the "DYLIBS_TO_BE_BUNDLED" setting in the User-Defined section of the Target's Build Settings.
