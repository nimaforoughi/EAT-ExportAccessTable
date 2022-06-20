# EAT-ExportAddressTable
EAT - Export Address Table diagram writeup



## WinDBG tool:
How to retreive the DLL base address:

lmf
<img src="https://github.com/nimaforoughi/EAT-ExportAddressTable/blob/main/Images/EAT-Export%20Table%20Address%200.png" width="1000">
How to retreive the Export Directory address:

!dh

<img src="https://github.com/nimaforoughi/EAT-ExportAddressTable/blob/main/Images/EAT-Export%20Table%20Address%201.png" width="400">
dc 774e0000+110340

How to parse the EAT:
The full explanation is presented by Alice Climent Pommeret in <https://alice.climent-pommeret.red/posts/direct-syscalls-hells-halos-syswhispers2/#what-is-a-hook->

![image](https://user-images.githubusercontent.com/90676852/174516198-99d8ec8e-1fe5-4cab-823f-18da3d549a79.png)

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

![image](https://user-images.githubusercontent.com/90676852/174515889-50d40d49-1b22-49ef-938b-6ea4b72a594d.png)

![image](https://github.com/nimaforoughi/EAT-ExportAddressTable/blob/main/Images/EAT.drawio%20(1).png)





