Distributing a driver package
=============================

<span id="ddk_distributing_a_driver_pg"></span><span id="DDK_DISTRIBUTING_A_DRIVER_PG"></span>
----------------------------------------------------------------------------------------------

This topic describes how to securely distribute your driver package. This information includes how to distribute a driver package through the Microsoft Windows Update program. This topic also describes how Windows protects system files.

<span id="ddk_windows_update_pg"></span><span id="DDK_WINDOWS_UPDATE_PG"></span>Windows Update
----------------------------------------------------------------------------------------------

* [Driver packages](https://msdn.microsoft.com/en-us/Library/Windows/Hardware/Ff544840) that pass [Windows Hardware Certification Kit (HCK)](http://go.microsoft.com/fwlink/p/?linkid=254893) testing can be digitally-signed by WHQL. If your driver package is digitally-signed by WHQL, it can be distributed through the Windows Update program or other Microsoft-supported distribution mechanisms.

Obtaining a WHQL release signature is part of the [Windows Hardware Certification Kit (HCK)](http://go.microsoft.com/fwlink/p/?linkid=254893). A WHQL release signature consists of a digitally-signed [catalog file](https://msdn.microsoft.com/en-us/Library/Windows/Hardware/Ff537872). The digital signature does not change the driver binary files or the INF file that you submit for testing.

You can distribute a driver package through the Windows Update program if the driver package:

-   Passes the WHQL test program and receives a [WHQL release signature](https://msdn.microsoft.com/en-us/Library/Windows/Hardware/Ff553976).

-   Qualifies for the Windows Certification Program.

-   Meets additional requirements that ensure that Windows Update can determine the correct driver package for the user's device, can legally distribute it, and can automatically download it.

Because the requirements of the Windows Update program are frequently updated, you should regularly check the [Windows Update driver publishing](http://go.microsoft.com/fwlink/p/?linkid=8712) Web site.

<span id="ddk_protection_for_system_files_pg"></span><span id="DDK_PROTECTION_FOR_SYSTEM_FILES_PG"></span>Protection for System Files
-------------------------------------------------------------------------------------------------------------------------------------

Windows File Protection (WFP) protects Windows operating system files from being replaced with unknown or incompatible versions.

WFP prevents programs from replacing critical Windows system files. Programs must not overwrite these files because they are used by the operating system and by other programs. Protecting these files prevents problems with programs and the operating system.

The types of system files that WFP protects include .sys, .exe, .ocx, and .dll files that ship "in the box" with the operating system.

During WHQL testing, the [**Signability**](https://msdn.microsoft.com/en-us/Library/Windows/Hardware/Ff547089) program checks a driver's INF file to ensure that it does not attempt to replace system files. A driver package that attempts to replace system files cannot receive a digital signature. A driver package can, however, contain updated versions of files that the vendor supplied to Microsoft to ship with Windows 2000 or later versions of the operating system.

For additional information about Windows File Protection, see the Windows SDK documentation.






[send comments about this topic to microsoft](mailto:wsddocfb@microsoft.com?subject=documentation%20feedback%20[vsdriver\vsdriver]: %20Distributing%20a%20driver%20package%20%20RELEASE:%20%289/30/2015%29&body=%0A%0APRIVACY%20STATEMENT%0A%0AWe%20use%20your%20feedback%20to%20improve%20the%20documentation.%20We%20don't%20use%20your%20email%20address%20for%20any%20other%20purpose,%20and%20we'll%20remove%20your%20email%20address%20from%20our%20system%20after%20the%20issue%20that%20you're%20reporting%20is%20fixed.%20While%20we're%20working%20to%20fix%20this%20issue,%20we%20might%20send%20you%20an%20email%20message%20to%20ask%20for%20more%20info.%20Later,%20we%20might%20also%20send%20you%20an%20email%20message%20to%20let%20you%20know%20that%20we've%20addressed%20your%20feedback.%0A%0AFor%20more%20info%20about%20Microsoft's%20privacy%20policy,%20see%20http://privacy.microsoft.com/en-us/default. "Send comments about this topic to Microsoft""
<!--HONumber=Jan16_HO2-->
