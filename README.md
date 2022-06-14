# EAT-ExportAccessTable
EAT - Export Access Table diagram writeup

![image](https://user-images.githubusercontent.com/90676852/173491921-4de70cd9-2525-40c7-a168-328b33d1d0f5.png | width=100 )
![image](https://user-images.githubusercontent.com/90676852/173491921-4de70cd9-2525-40c7-a168-328b33d1d0f5.png width="48")

<img src="https://user-images.githubusercontent.com/90676852/173491921-4de70cd9-2525-40c7-a168-328b33d1d0f5.png" width="100">

<a href="url"><img src="https://user-images.githubusercontent.com/90676852/173491921-4de70cd9-2525-40c7-a168-328b33d1d0f5.png" align="left" width="200" ></a>

## install python2.7
    sudo apt-get update 
    sudo apt-get -y install python2.7
    sudo apt-get -y install python3.9.2
    sudo apt-get -y install pcregrep libpcre++-dev python-dev python2-dev -y

## set python2.7 as the default version
    sudo su
    python --version 
    update-alternatives --list python 
    update-alternatives --install /usr/bin/python python /usr/bin/python2.7 1 
    update-alternatives --install /usr/bin/python python /usr/bin/python3.9 2 
    update-alternatives --config python  
> type number 1 and enter

    python --version
#now you will see default python is version 2.x



    su <localuser> #replace the localuser


## install pydeep
    sudo apt-get -y install libfuzzy-dev
    cd ~/
    git clone https://github.com/kbandla/pydeep
    python ./pydeep/setup.py build
    python ./pydeep/setup.py test
    sudo python ./pydeep/setup.py install

    pip2 uninstall distorm3
    pip2 install distorm3==3.4.4
    pip2 install pdbparse pefile pyimpfuzzy libpff-python pexpect django geoip2 pycrypto pymongo python-registry virustotal-api yara-python git+https://github.com/smarnach/pyexiftool.git#egg=pyexiftool
    
#pip2 install certifi==2018.10.15 chardet==3.0.4 construct==2.9.45 distorm3==3.4.4 Django==1.11.16, django-developer-panel==0.1.2, enum34==1.1.6, geoip2==2.9.0, idna==2.7, ipaddress==1.0.22, maxminddb==1.4.1, pexpect==4.6.0, Pillow==5.4.1, ptyprocess==0.6.0, pycrypto==2.6.1, pydeep==0.2, pymongo==3.7.2, python-registry==1.0.4, pytz==2018.7, requests==2.20.1, urllib3==1.24.1, virustotal-api==1.1.10, yara-python==3.5.0, git+https://github.com/smarnach/pyexiftool.git#egg=pyexiftool

    pip2 install certifi chardet construct distorm3==3.4.4 Django django-developer-panel enum34 geoip2 idna ipaddress maxminddb pexpect Pillow ptyprocess pycrypto pydeep pymongo python-registry pytz requests urllib3 virustotal-api yara-python git+https://github.com/smarnach/pyexiftool.git#egg=pyexiftool
    echo "/usr/local/lib" >> /etc/ld.so.conf && ldconfig
    

    
○ When you want to use a function exported from the DLL you can import it by name or ordinal
	• when importing by ordinal the number used is base + The corresponding value for the function in the AddressOfNameOrdinal

From <https://www.linkedin.com/in/nima-foroughi/details/experience/> 



lmDV 
!dh [baseaddress of modoule] #showing sections and headers

	:000> lmD
	start    end        module name
	00400000 00412000   helloworld_smallest   (no symbols)           
	75170000 75210000   apphelp    (deferred)             
	76220000 762e2000   msvcrt     (pdb symbols)          C:\ProgramData\Dbg\sym\msvcrt.pdb\3115F74B5F917A20087F0FC0C26356291\msvcrt.pdb
	764e0000 765d0000   KERNEL32   (pdb symbols)          C:\ProgramData\Dbg\sym\wkernel32.pdb\5157D8708DD8FDACE5661EB05F938FE01\wkernel32.pdb
	76860000 76ab7000   KERNELBASE   (deferred)             
	774e0000 7768a000   ntdll      (pdb symbols)          C:\Pro
	

Structure:

    typedefstruct_IMAGE_EXPORT_DIRECTORY{
        1-DWORDCharacteristics;
        2-DWORDTimeDateStamp;
        3-WORDMajorVersion;WORDMinorVersion;
        4-DWORDName;// The name of the Dll
        5-DWORDBase;// Number to add to the values found in AddressOfNameOrdinals to retrieve the "real" Ordinal number of the function (by real I mean used to call it by ordinals).
        6-DWORDNumberOfFunctions;// Number of all exported functions      
        7-DWORDNumberOfNames;// Number of functions exported by name-  If this value is 0, then all of the functions in this module are exported by ordinal and none of them is exported by name.     
        8-DWORDAddressOfFunctions;// Export Address Table. Address of the functions addresses array.   
        9-DWORDAddressOfNames;// Export Name table. Address of the functions names array.  a RVA to the list of exported names – it points to an array of NumberOfNames 32-bit values, each being a RVA to the exported symbol name.      
        10-DWORDAddressOfNameOrdinals;// Export sequence number table.  Address of the Ordinals (minus the value of Base) array.    

    }IMAGE_EXPORT_DIRECTORY,*PIMAGE_EXPORT_DIRECTORY;

From <https://alice.climent-pommeret.red/posts/direct-syscalls-hells-halos-syswhispers2/#what-is-a-hook-> 



    0:000> dc 774e0000+110340
    775f0340	00000000		9f1bbe3a		00000000		001163da	Dll name	 ....:........c..
    775f0350	00000008	Base ordinal	000009a5	NumberOfFunctions	000009a5	NumberOfNames	00110368	AddressOfFunctions	 ............h...
    775f0360	001129fc	AddressOfNames	00115090	AddressOfNameOrdinals	0002a180		0003f280	 	  .)...P..........
    775f0370  0003efc0 000c2b80 000c2c30 000c2c40  .....+..0,..@,..
    775f0380  000c2c60 0006aff0 00099250 0006b0d0  `,......P.......
    775f0390  000c2c70 000c2ca0 000c2d90 000c2dc0  p,...,...-...-..
    775f03a0  00069f50 00069f10 000c2e00 000c2f50  P...........P/..
    775f03b0  00069ed0 000c2f70 000c2f80 000c2fd0  ....p/.../.../..

    0:000> dc 774e0000+110340
    775f0340  	00000000 9f1bbe3a 00000000 001163da  ....:........c..
    775f0350  	00000008 000009a5 000009a5 00110368  ............h...
    775f0360  	001129fc 00115090 0002a180 0003f280  .)...P..........
    775f0370  	0003efc0 000c2b80 000c2c30 000c2c40  .....+..0,..@,..
    775f0380  	000c2c60 0006aff0 00099250 0006b0d0  `,......P.......
    775f0390  	000c2c70 000c2ca0 000c2d90 000c2dc0  p,...,...-...-..
    775f03a0  	00069f50 00069f10 000c2e00 000c2f50  P...........P/..
    775f03b0  	00069ed0 000c2f70 000c2f80 000c2fd0  ....p/.../.../..



    001163da : Name >>> ntdll.dll
    001129fc : AddressOfFunctions >>> 0002a180 (1st Function Address RVA)
    00115090 : AddressOfNames >>> 00116488 [table] >>> 1st Function Name (A_SHAFinal) #it is the 8th= (base[0]) function actually
    0002a180 : AddressOfNameOrdinals >>> 00080007 >>> 8304eb00

From <http://jumpdollar.blogspot.com/2014/09/windbg-trying-to-find-export-address.html> 

    Each Function_name[n] finds its corresponding Function_address[?] based on the AddressOfNameOrdinals[n]
    Function_name[n]	.Function_address.index	= AddressOfNameOrdinals[n]
    Function_name[0]	.Function_address.index	= AddressOfNameOrdinals[0]
    A_SHAFinal	.Function_address_index	= 07
    A_SHAFinal	corresponding to	Function_address[07]
    or 
    Function_name[n]	.Function_address.index	= Function_address[n+BaseOrdinal-1]
    Function_name[0]	.Function_address.index	= Function_address[0+BaseOrdinal-1]
    A_SHAFinal	.Function_address_index	= 0+08-1
    A_SHAFinal	corresponding to	Function_address[07]=0006aff0




    Base 0x00400000 
    .idata 0x00408000
    .Text 0x00401000

    import 0x00008000 (size=610)
    import-address 0x00008134 (size= E4)

    ILT (RVA) 50800000 > 00008050 >>> 00008218 >>> (d000)+ DeleteCriticalSection
    Name (RVA) 5C850000 > 0000855C >>> KERNEL32.dll
    IAT (RVA) 34810000 > 00008134 >>> 00008218 >>> (d000)+ DeleteCriticalSection


    ILT (RVA) A0800000 > 80A0 >>> 8382 >>> (0051)+ _strdup
    Name (RVA) 74850000 > 8574 >>> msvcrt.dll
    IAT (RVA) 84810000 > 8184 >>> 8382 >>> (0051)+ _strdup

    ILT (RVA) AC800000 > 80AC >>> 8398 >>> (0059)+ __getmainargs
    Name (RVA) 04860000 > 8604 >>> msvcrt.dll
    IAT (RVA) 90810000 > 8190 >>>  8398 >>> (0059)+ __getmainargs




    + 774e0000 774e1000     1000 MEM_IMAGE   MEM_COMMIT  PAGE_READONLY                      Image      [ntdll; "ntdll.dll"]
      774e1000 77606000   125000 MEM_IMAGE   MEM_COMMIT  PAGE_EXECUTE_READ                  Image      [ntdll; "ntdll.dll"]

      77606000 7760c000     6000 MEM_IMAGE   MEM_COMMIT  PAGE_READWRITE                     Image      [ntdll; "ntdll.dll"]

      7760c000 7768a000    7e000 MEM_IMAGE   MEM_COMMIT  PAGE_READONLY                      Image      [ntdll; "ntdll.dll"]


    +        0`774e0000        0`774e1000        0`00001000 MEM_IMAGE   MEM_COMMIT  PAGE_READONLY                      Image      [ntdll32; "ntdll32.dll"]
             0`774e1000        0`77606000        0`00125000 MEM_IMAGE   MEM_COMMIT  PAGE_EXECUTE_READ                  Image      [ntdll32; "ntdll32.dll"]

             0`77606000        0`77607000        0`00001000 MEM_IMAGE   MEM_COMMIT  PAGE_WRITECOPY                     Image      [ntdll32; "ntdll32.dll"]
             0`77607000        0`7760d000        0`00006000 MEM_IMAGE   MEM_COMMIT  PAGE_READWRITE                     Image      [ntdll32; "ntdll32.dll"]

             0`7760d000        0`7760f000        0`00002000 MEM_IMAGE   MEM_COMMIT  PAGE_WRITECOPY                     Image      [ntdll32; "ntdll32.dll"]
             0`7760f000        0`7768a000        0`0007b000 MEM_IMAGE   MEM_COMMIT  PAGE_READONLY                      Image      [ntdll32; "ntdll32.dll"]



    774e1000 - 77603620 .text RX  
    77604000 - 77604401 PAGE RX
     77605000 - 77605199 RT RX

    77606000 - 7760B780 .data RW
    7760C000 - 7760E368 .mrdata RW

    7760F000 -  7760F004 .00cfg R
    77610000 - 77683480 .rsrc  R
    77684000- 77689288 .reloc R


    0:000> !dh 774e0000

    File Type: DLL
    FILE HEADER VALUES
         14C machine (i386)
           8 number of sections
    9F1BBE3A time date stamp
           0 file pointer to symbol table
           0 number of symbols
          E0 size of optional header
        2102 characteristics
                Executable
                32 bit word machine
                DLL

    OPTIONAL HEADER VALUES
         10B magic #
       14.28 linker version
      123000 size of code
       80800 size of initialized data
           0 size of uninitialized data
           0 address of entry point
        1000 base of code
             ----- new -----
    774e0000 image base
        1000 section alignment
         200 file alignment
           3 subsystem (Windows CUI)
       10.00 operating system version
       10.00 image version
       10.00 subsystem version
      1AA000 size of image
         400 size of headers
      1ABEB1 checksum
    00040000 size of stack reserve
    00001000 size of stack commit
    00100000 size of heap reserve
    00001000 size of heap commit
        4140  DLL characteristics
                Dynamic base
                NX compatible
                Guard
      110340 [   132E0] address [size] of Export Directory
           0 [       0] address [size] of Import Directory
      130000 [   73480] address [size] of Resource Directory
           0 [       0] address [size] of Exception Directory
      19F200 [    6110] address [size] of Security Directory
      1A4000 [    5288] address [size] of Base Relocation Directory
        A368 [      70] address [size] of Debug Directory
           0 [       0] address [size] of Description Directory
           0 [       0] address [size] of Special Directory
           0 [       0] address [size] of Thread Storage Directory
        18B0 [      BC] address [size] of Load Configuration Directory
           0 [       0] address [size] of Bound Import Directory
           0 [       0] address [size] of Import Address Table Directory
           0 [       0] address [size] of Delay Import Directory
           0 [       0] address [size] of COR20 Header Directory
           0 [       0] address [size] of Reserved Directory


    SECTION HEADER #1
       .text name
      122620 virtual size
        1000 virtual address 774e1000 - 77603620
      122800 size of raw data
         400 file pointer to raw data
           0 file pointer to relocation table
           0 file pointer to line numbers
           0 number of relocations
           0 number of line numbers
    60000020 flags
             Code
             (no align specified)
             Execute Read


    Debug Directories(4)
        Type       Size     Address  Pointer
        cv           23       23798    22b98	Format: RSDS, guid, 1, wntdll.pdb
        (   13)     548       237bc    22bbc
        (   16)      24       23d04    23104
        dllchar       4       23d28    23128

    00000001 extended DLL characteristics
              CET compatible


    SECTION HEADER #2
        PAGE name
         401 virtual size 
      124000 virtual address 77604000 - 77604401
         600 size of raw data
      122C00 file pointer to raw data
           0 file pointer to relocation table
           0 file pointer to line numbers
           0 number of relocations
           0 number of line numbers
    60000020 flags
             Code
             (no align specified)
             Execute Read

    SECTION HEADER #3
          RT name
         199 virtual size
      125000 virtual address 77605000 - 77605199
         200 size of raw data
      123200 file pointer to raw data
           0 file pointer to relocation table
           0 file pointer to line numbers
           0 number of relocations
           0 number of line numbers
    60000020 flags
             Code
             (no align specified)
             Execute Read

    SECTION HEADER #4
       .data name
        5780 virtual size
      126000 virtual address 77606000 - 7760B780
         E00 size of raw data
      123400 file pointer to raw data
           0 file pointer to relocation table
           0 file pointer to line numbers
           0 number of relocations
           0 number of line numbers
    C0000040 flags
             Initialized Data
             (no align specified)
             Read Write

    SECTION HEADER #5
     .mrdata name
        2368 virtual size
      12C000 virtual address 7760C000 - 7760E368
        2400 size of raw data
      124200 file pointer to raw data
           0 file pointer to relocation table
           0 file pointer to line numbers
           0 number of relocations
           0 number of line numbers
    C0000040 flags
             Initialized Data
             (no align specified)
             Read Write

    SECTION HEADER #6
      .00cfg name
           4 virtual size
      12F000 virtual address 7760F000 -  7760F004
         200 size of raw data
      126600 file pointer to raw data
           0 file pointer to relocation table
           0 file pointer to line numbers
           0 number of relocations
           0 number of line numbers
    40000040 flags
             Initialized Data
             (no align specified)
             Read Only

    SECTION HEADER #7
       .rsrc name
       73480 virtual size
      130000 virtual address 77610000 - 77683480
       73600 size of raw data
      126800 file pointer to raw data
           0 file pointer to relocation table
           0 file pointer to line numbers
           0 number of relocations
           0 number of line numbers
    40000040 flags
             Initialized Data
             (no align specified)
             Read Only

    SECTION HEADER #8
      .reloc name
        5288 virtual size
      1A4000 virtual address 77684000- 77689288
        5400 size of raw data
      199E00 file pointer to raw data
           0 file pointer to relocation table
           0 file pointer to line numbers
           0 number of relocations
           0 number of line numbers
    42000040 flags
             Initialized Data
             Discardable
             (no align specified)
             Read Only




    = [0x994] : Function export of 'PssNtQuerySnapshot'            - PssNtQuerySnapshot                            - 0x2cc         - 0x775ea200    - Invalid argument to method 'getModuleSymbol' [at ImageInf... =
    = [0x995] : Function export of 'PssNtValidateDescriptor'       - PssNtValidateDescriptor                       - 0x2cd         - 0x775ea390    - Invalid argument to method 'getModuleSymbol' [at ImageInf... =
    = [0x996] : Function export of 'PssNtWalkSnapshot'             - PssNtWalkSnapshot                             - 0x2ce         - 0x775ea460    - Invalid argument to method 'getModuleSymbol' [at ImageInf... =
    = [0x997] : Function export of 'RtlAllocateMemoryBlockLooka... - RtlAllocateMemoryBlockLookaside               - 0x2fa         - 0x77605010    - Unknown exception [at ImageInfo (line 3876 col 9)]           =
    = [0x998] : Function export of 'RtlAllocateMemoryZone'         - RtlAllocateMemoryZone                         - 0x2fb         - 0x776050a0    - Invalid argument to method 'getModuleSymbol' [at ImageInf... =
    = [0x999] : Function export of 'RtlFreeMemoryBlockLookaside'   - RtlFreeMemoryBlockLookaside                   - 0x40d         - 0x77605180    - Invalid argument to method 'getModuleSymbol' [at ImageInf... =
    = [0x99a] : Function export of 'NlsAnsiCodePage'               - NlsAnsiCodePage                               - 0xc6          - 0x7760681c    - Invalid argument to method 'getModuleSymbol' [at ImageInf... =
    = [0x99b] : Function export of 'NlsMbOemCodePageTag'           - NlsMbOemCodePageTag                           - 0xc8          - 0x77609148    - Invalid argument to method 'getModuleSymbol' [at ImageInf... =
    = [0x99c] : Function export of 'NlsMbCodePageTag'              - NlsMbCodePageTag                              - 0xc7          - 0x77609149    - Invalid argument to method 'getModuleSymbol' [at ImageInf... =
    = [0x99d] : Function export of 'RtlpFreezeTimeBias'            - RtlpFreezeTimeBias                            - 0x65b         - 0x77609638    - Invalid argument to method 'getModuleSymbol' [at ImageInf... =
    = [0x99e] : Function export of 'LdrpChildNtdll'                - LdrpChildNtdll                                - 0xbc          - 0x7760b3b8    - Invalid argument to method 'getModuleSymbol' [at ImageInf... =
    = [0x99f] : Function export of 'LdrParentRtlInitializeNtUse... - LdrParentRtlInitializeNtUserPfn               - 0x94          - 0x7760b43c    - Invalid argument to method 'getModuleSymbol' [at ImageInf... =
    = [0x9a0] : Function export of 'LdrParentRtlRetrieveNtUserPfn' - LdrParentRtlRetrieveNtUserPfn                 - 0x96          - 0x7760b440    - Invalid argument to method 'getModuleSymbol' [at ImageInf... =
    = [0x9a1] : Function export of 'LdrParentRtlResetNtUserPfn'    - LdrParentRtlResetNtUserPfn                    - 0x95          - 0x7760b444    - Invalid argument to method 'getModuleSymbol' [at ImageInf... =
    = [0x9a2] : Function export of 'LdrParentInterlockedPopEntr... - LdrParentInterlockedPopEntrySList             - 0x93          - 0x7760b44c    - Invalid argument to method 'getModuleSymbol' [at ImageInf... =
    = [0x9a3] : Function export of 'Wow64Transition'               - Wow64Transition                               - 0x6e6         - 0x7760c220    - Invalid argument to method 'getModuleSymbol' [at ImageInf... =
    = [0x9a4] : Function export of 'LdrSystemDllInitBlock'         - LdrSystemDllInitBlock                         - 0xb3          - 0x7760c240    - Invalid argument to method 'getModuleSymbol' [at ImageInf... =
    ===============================================================================================================================================================================================================
![image](https://user-images.githubusercontent.com/90676852/173494348-3c6836da-e699-4ddb-b8ee-fcba26b880a4.png)


