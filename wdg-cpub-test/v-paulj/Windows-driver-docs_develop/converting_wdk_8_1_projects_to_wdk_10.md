Converting WDK 8.1 Projects to WDK 10
=====================================

This topic describes how to convert a driver project that was created using Microsoft Visual Studio 2013 and Windows Driver Kit (WDK) 8.1 to a driver project that builds in Microsoft Visual Studio 2015 with the Windows Driver Kit (WDK) 10.

Visual Studio 2015 has new compiler warnings and errors. Even if your driver project built with no errors in Visual Studio 2013, you might see errors when you build it in Visual Studio 2015.

Use these steps to convert the projects in a driver solution.

1.  In Visual Studio 2015, open the legacy driver solution.

    Visual Studio automatically runs ProjectUpgradeTool to convert the projects in this solution. You can also run this tool from the command line. By default, when you install the WDK, ProjectUpgradeTool.exe installs in Windows Kits\\10\\bin\\x86.

    Visual Studio opens a **Review Solution Actions** dialog with the title **Upgrade VC++ Compiler and Libraries**. Click **OK** and Visual Studio attempts to upgrade all projects in the solution.

    If you see a **File Modification Detected** dialog, choose **Reload All**.

2.  In the Solution Explorer pane, right-click the driver project name and choose **Properties**. Click the **Configuration Manager** button. In the **Active solution configuration** list, choose **<New...>**. Type a name and copy the settings from a Windows 8.1 project context. Click **OK**.

    Typically, the converted solution contains two configuration profiles, one for debug (testing) and one for release. To create a similar environment with WDK 10, simply choose **<New...>** twice. To create a debug profile, copy from the **Win 8.1 Debug** profile. To create a release profile, copy from the **Win 8.1 Release** profile.

3.  In WDK versions prior to WDK 10, your driver solution always needed a package project. In WDK 10, you only need a package project if you are including multiple drivers in a driver package. Use the following guidelines:

    -   If you have only one driver in the solution and a package project exists, delete it.

    -   If you have more than one driver in the solution, ensure that your solution contains a package project. Then, for each driver project in the solution, open project properties and navigate to **Configuration Properties > Driver Settings**. Set **BuildPackage** to **No**. If you are building from the command line, set **/p:SupportsPackaging=false**.

4.  Again in driver project properties, choose **Properties**. Navigate to **Configuration Properties > Driver Settings > General > Target OS Version**. Select Windows 10.

    Verify that **Target Platform** is set to **Desktop**, and build the solution. Fix any errors that occur.

5.  Once the solution builds successfully, change **Target Platform** to **Universal**.

Build the solution again. At this point, the only errors are from the ApiValidator tool, which checks if the driver calls any non-universal functionality. Replace any calls to non-universal DDIs with calls to universal DDIs.

For more information about ApiValidator, see [Validating Universal Windows drivers](validating_universal_drivers.md).

To learn how to determine the target platform for a given DDI, see [Target platform on MSDN driver reference pages](windows_10_editions_for_universal_drivers.md).





[send comments about this topic to microsoft](mailto:wsddocfb@microsoft.com?subject=documentation%20feedback%20[vsdriver\vsdriver]: %20Converting%20WDK%208.1%20Projects%20to%20WDK%2010%20%20RELEASE:%20%289/30/2015%29&body=%0A%0APRIVACY%20STATEMENT%0A%0AWe%20use%20your%20feedback%20to%20improve%20the%20documentation.%20We%20don't%20use%20your%20email%20address%20for%20any%20other%20purpose,%20and%20we'll%20remove%20your%20email%20address%20from%20our%20system%20after%20the%20issue%20that%20you're%20reporting%20is%20fixed.%20While%20we're%20working%20to%20fix%20this%20issue,%20we%20might%20send%20you%20an%20email%20message%20to%20ask%20for%20more%20info.%20Later,%20we%20might%20also%20send%20you%20an%20email%20message%20to%20let%20you%20know%20that%20we've%20addressed%20your%20feedback.%0A%0AFor%20more%20info%20about%20Microsoft's%20privacy%20policy,%20see%20http://privacy.microsoft.com/en-us/default. "Send comments about this topic to Microsoft""
<!--HONumber=Jan16_HO2-->
