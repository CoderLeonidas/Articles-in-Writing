# Building a PlugIn for the Mac OS X Client Engine by Using the Virtual Channel SDK

This document describes `how to write a Virtual Channel PlugIn for the OS X client engine`. To successfully build a Virtual Channel PlugIn for the OS X client engine, you will need a Mac running Mac OS X 10.7, 10.8, 10.9 or 10.10 with the Xcode 5.1.1 installed. 

You will also need access to a Windows-based computer where you can compile your applications that are to run on the server, and you should be familiar with the Virtual Channel SDK for Windows. 

# Contents of the Virtual Channel SDK

The Virtual Channel SDK comes in one folder named `Virtual Channel SDK`. This folder contains the following parts: 

•	There are four folders that are part of the Virtual Channel SDK that you should not modify, named `Documentation`, `Includes`, `Libraries`, and `Build Settings`.	
•	There are three folders containing sample PlugIns, named `Ping PlugIn Example`, `Over PlugIn Example`, and `Mix PlugIn Example`. The sample folders each contain a complete project, which is designed to be contained within a folder inside the Virtual Channel SDK folder. Each sample folder contains an Xcode project, such as `Ping.xcodeproj`, a `Build Settings` folder, an `Info.plist` file, an `English.lproj` folder, a `Server items` folder, along with the `C source files and header files` for the project. For example, the Ping PlugIn Example contains four source files: vdping.c, vdping.h, pingwire.c, and pingwire.h. 

•	After successfully building a PlugIn, there will be a build folder inside the folder for that PlugIn, containing in turn three folders `Debug`, `Release`, and a folder named after your project, like `Ping.build`. The Release folder will contain the PlugIn as you want to ship it; for example named `Ping.PlugIn`. The Debug folder contains a debugging version of the client.  

•	The `Server items` folder contains the source code and other files necessary to build the server counterpart of each sample. You will need the Virtual Channel SDK for Windows which contains the documentation for how to build the server executables from these files. Each of these folders also contains a file like `ctxping.exe.sample` or similar; this is the compiled executable to be run on the server. The suffix `.sample` needs to be removed before running it; it is just there to make transporting these files easier.  

The sample PlugIns are set up to work with Xcode 5.1 or later and use a deployment target of OS X 10.7. By default, they produce code that will run on `Intel-based` Macs. You should start development by copying one of the supplied Xcode sample projects. 

When you open each example project using Xcode, you will find the following Groups under Groups & Files: 

•	`Settings`: This contains a single configuration file `_ProductSettings.xcconfig`, which you will need to modify.

•	`Sources`: This contains all the source and header files for your PlugIn. You can start with the files in the examples, but obviously you will have to add your own functionality.

•	`Resources`: Contains Info.plist and InfoPlist.strings (English). These are set up to work correctly once you’ve changed _ProductSettings.xcconfig, but you can change them if you need to.

•	`Virtual Channel SDK`: This folder contains the components supplied by Citrix; that is documentation, header files, a library file, and so on. You should not modify the contents of this group at all. The actual files are not in your PlugIn folder, but inside the Virtual Channel SDK itself.

•	`External Frameworks and Libraries`: This contains a reference to the CoreFoundation framework which is required for any PlugIn; here you would add any frameworks your PlugIn requires.

•	`Products` Contains the completely built PlugIn once it is built successfully.


# Creating Your Own PlugIn

Citrix recommends that you start creating your own PlugIn by copying one of the folders with an existing sample project. Assuming that you want your own PlugIn named `MyPlugIn`, you would make the following changes:

•	Duplicate one of the existing example PlugIn folders. For example, duplicate `Ping PlugIn Example` and name the new folder `My Own PlugIn`. The copy must still be inside the `Virtual Channel SDK` folder. The actual name of the folder doesn't matter, as long as you are happy with it.

•	Inside the `My Own PlugIn` folder, you’ll find the project file, `Ping.xcodeproj`. Rename it appropriately; for example to `MyPlugIn.xcodeproj`. Again, the name of the project doesn't matter. 

•	Decide on a name for your PlugIn; for example, `MyPlugIn` instead of `Ping`. To be compatible with the 10.x and 11.x versions of the client, the name portion should be 7 characters or fewer and must be a total of 12 characters or fewer. This name will be visible in the user interface and needs to be added to the Modules file (see Installing the PlugIn later in this document).

•	Open your PlugIn project by double-clicking `MyPlugIn.xcodeproj`. In the Settings group, you need to edit the file `_ProductSettings.xcconfig`. Change the product name, from `Ping `to `MyPlugIn`, and then change the bundle identifier from `com.citrix.ping.samples.PlugIns` to `com.mycompany.myPlugIn.PlugIns`, customized for your company name. 

•	In the Sources group, rename the four files `vdping.c`, `vdping.h`, `pingwire.c` and `pingwire.h` to something more suitable, like `vdmyPlugIn.c`, `vdmyPlugIn.h`, `myPlugInwire.c` and `myPlugInwire.h`. This will automatically rename the source files on your hard drive as well and update your project appropriately. Change the `#include `directives in the source files appropriately. You can now build your PlugIn.

•	Decide on a Virtual Channel name for your PlugIn. The Virtual Channel name is a unique string of up to **seven** characters. Any strings starting with **CTX** are reserved for use by Citrix. You will find a `#define` directive like` #define CTXPING_VIRTUAL_CHANNEL_NAME  CTXPING` in the file `vdmyPlugIn.h`. You should change the `#define` directive and the source code where it is used appropriately, for example as `#define MYPLUGIN_VIRTUAL_CHANNEL_NAME  MYPLUGN`. Remember that the length of the Virtual Channel name must not exceed **seven** characters. 


# Implementing Your PlugIn

To implement your PlugIn, you should follow the documentation in the Virtual Channel PlugIn for Windows. 
 

Ensuring Data Layout Compatibility Between Server and OS X PlugIn Code

You must make sure that all data structures sent between a server and an OS X PlugIn use exactly the same data layout and the same byte ordering. 

All data structures that are transmitted between the OS X or any other client engine and the server need to be compiled surrounded by the compiler directives `#pragma pack (1)` and `#pragma pack()`. These directives are accepted both by Windows compilers and by the Xcode compiler used by OS X, including x86, PowerPC, and Arm compilers. This ensures that a data structure will be packed as tightly as possible, but more importantly, it ensures that the layout of all data structures is the same on the server and on all versions of OS X PlugIns. There can still be differences due to different endianness. An example data structure from the Ping example: 

```c++
	#pragma pack(1)
	typedef struct _VDPING_C2H
	{
		VD_C2H  Header;
 		USHORT  usMaxDataSize; 
		USHORT  usPingCount; 
	} VDPING_C2H, * PVDPING_C2H;
	#pragma pack()
```

Note that this example uses types like USHORT, ULONG, and so on, which will always have the same size (2 bytes and 4 bytes respectively), no matter what sizes the compiler chooses for short and long, for example. You shouldn't use, for example, **long** because that would cause problems if the server runs a 64 bit application and the OS X PlugIn is 32 bit, or vice versa. You must use the types CHAR, SHORT, LONG, UINT8, USHORT and ULONG for 8-, 16- and 32-bit signed and unsigned quantities. Do not use the Standard C types char, short, int or long to avoid compatibility problems between the server and the PlugIn.

Note that in some sample code you might find `#define` directives like `#define packed_sizeof_VDC2H 48`. These macros need to be used on computers where the compiler will produce different data layouts than on the server; this macro would be used for the size of a data structure when compiled on the server, which might be different from the size of the same structure compiled in a PlugIn. The numbers in these macros are counted manually. These macros are not needed in OS X, but they will still work. 

# Installing the PlugIn 

To test your PlugIn, the bundle must be copied into the `~/Library/Application Support/Citrix/PlugIns` folder. (You must create that folder if it doesn’t already exist; also note that PlugIns is case-sensitive.) 

In a new Finder window, open the folder containing your PlugIn, and then open the build folder. The build folder will contain a folder `MyPlugIn.build` (or whatever name you picked) which can be ignored, and folders named Debug and Release, depending on whether you built a Debug or Release version of the PlugIn. Inside, you will find the PlugIn, named for example `MyPlugIn.PlugIn`; the Debug folder would also contain a file `MyPlugIn.PlugIn.dSym`. Drag the PlugIn and optionally the symbol file into the PlugIns folder mentioned above. 

Versions of the Citrix Viewer up to version 11.0.0 don't support PlugIns with names of more than *12* characters, and they don't automatically append .PlugIn to the name of the PlugIn. If you want to support these versions, you need to rename your PlugIn to MyPlugIn (without the suffix `.PlugIn`). To do so, right-click your PlugIn, choose Get Info, and then deselect Hide Extension. You can then remove the suffix .PlugIn after a warning. If the name of your PlugIn is five characters or fewer, you can leave it unchanged; for example Ping.PlugIn, but you need to use Ping.PlugIn as the PlugIn name, not Ping. If you only have clients later than the 11.0.0 client, you can leave the PlugIn as it is and use MyPlugIn or Ping as the PlugIn name. 

Next, modify the Modules file inside the `~/Library/Application Support/Citrix Receiver` folder. In the section `[ICA 3.0]`, add the name of your PlugIn at the end of the VirtualDriver line, for example `Ping.PlugIn`. Also, add a line `Ping.PlugIn = On` in that section. Then, add a section `[Ping.PlugIn]` and add any settings that your PlugIn reads to this section; for example, add `PingCount = 3` to the Ping.PlugIn section, because that is a setting that the Ping sample PlugIn expects. 
