How to add test metadata
========================

For Windows 8, the Windows Driver Kit (WDK) uses the [Test Authoring and Execution Framework (TAEF)](https://msdn.microsoft.com/en-us/Library/Windows/Hardware/Hh439725) for creating test content. A TAEF test is an object implemented as a dynamic-link library (DLL) that contains multiple methods, where each method maps to a specific test scenario. The TAEF object combines related methods into a group of tests. For each test, there is a set of metadata that describes the test. To improve test portability and encapsulation, TAEF stores test metadata within the test object itself. When you create your own driver tests using the Driver Test templates, you need to add this metadata so that your driver tests are available and can be deployed using Visual Studio.

### <span id="Prerequisites"></span><span id="prerequisites"></span><span id="PREREQUISITES"></span>Prerequisites

-   The source code for a driver test written by using one of the Driver Test templates. For information, see [How to write a driver test using a Driver Test template](how_to_write_a_driver_test_.md).

### <span id="To_add_test_metadata_attributes"></span><span id="to_add_test_metadata_attributes"></span><span id="TO_ADD_TEST_METADATA_ATTRIBUTES"></span>To add test metadata attributes

1.  Add the required test property metadata to the source files for your test.
2.  For example, if you use the Driver Test template to create your version of the SurpriseRemove test, the following metadata is added. Edit the test description, display name, category, and results file attributes.

    <span codelanguage="ManagedCPlusPlus"></span>
    <table>
    <colgroup>
    <col width="100%" />
    </colgroup>
    <thead>
    <tr class="header">
    <th align="left">C++</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td align="left"><pre><code>// Declare the test class method DoSurpriseRemove - the main test method within this class
        BEGIN_TEST_METHOD(DoSurpriseRemove)
        // Required properties for driver tests
        TEST_METHOD_PROPERTY(L"Kits.Drivers", L"TRUE")
        TEST_METHOD_PROPERTY(L"Kits.Parameter", L"DQ")
        TEST_METHOD_PROPERTY(L"Kits.Parameter.DQ.Description", L"A WDTF SDEL query that is used to identify the target device(s) - http://go.microsoft.com/fwlink/p/?linkid=232678")
        TEST_METHOD_PROPERTY(L"Kits.Parameter.DQ.Default", L"INF::OriginalInfFileName='%InfFileName%'")  
        TEST_METHOD_PROPERTY(L"RebootPossible", L"true")
        // TODO: Required properties to be customized to match your test requirements
        TEST_METHOD_PROPERTY(L"Description", L"Plug and Play Surprise Remove Generated Template")
        TEST_METHOD_PROPERTY(L"Kits.DisplayName", L"My Plug and Play Surprise Remove Test") 
        TEST_METHOD_PROPERTY(L"Kits.Category", L"My Test Category")
        // Optional properties for driver tests
        TEST_METHOD_PROPERTY(L"Kits.Drivers.ResultFile", L"TestTextLog.log")
        // TODO: (see Windows Driver Kit documentation for additional optional properties)
        END_TEST_METHOD()</code></pre></td>
    </tr>
    </tbody>
    </table>

    <span codelanguage="CSharp"></span>
    <table>
    <colgroup>
    <col width="100%" />
    </colgroup>
    <thead>
    <tr class="header">
    <th align="left">C#</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td align="left"><pre><code>//*************************************************
        // DoSurpriseRemove is a test method as identified by the [TestMethod] tag. 
        // More methods can be added by following this basic pattern.
        // The name of the function defines the name of the test.
        //*************************************************
        [TestMethod]
        // Required properties (see Windows Driver Kit documentation for more information):
        [TestProperty("Kits.Drivers", "TRUE")]
        [TestProperty("Kits.Parameter", "DQ")]
        [TestProperty("Kits.Parameter.DQ.Description", "A WDTF SDEL query that is used to identify the target device(s) - http://go.microsoft.com/fwlink/p/?linkid=232678")]
        [TestProperty("Kits.Parameter.DQ.Default", "INF::OriginalInfFileName='%InfFileName%'")]
        // TODO: Required properties to be customized to match your test requirements.
        [TestProperty("Description", "Plug and Play Surprise Remove Generated Template")]
        [TestProperty("Kits.DisplayName", "My Plug and Play Surprise Remove Test")]
        [TestProperty("Kits.Category", "My Test Category")]
        [TestProperty("RebootPossible", "true")]
        // Optional properties (see Windows Driver Kit documentation for additional optional properties):
        [TestProperty("Kits.Drivers.ResultFile", "TestTextLog.log")]</code></pre></td>
    </tr>
    </tbody>
    </table>

    Windows Script Component (.wsc)

    <span codelanguage=""></span>
    <table>
    <colgroup>
    <col width="100%" />
    </colgroup>
    <tbody>
    <tr class="odd">
    <td align="left"><pre><code><!-- Define a test method with metadata: -->
        <method name="PlugAndPlaySurpriseRemoveTest">
        <!-- Required properties for ERT-->
        <TestMethodProperty name="Kits.Drivers" value="TRUE"/>
        <TestMethodProperty name="Kits.Parameter" value="DQ"/>
        <TestMethodProperty name="Kits.Parameter.DQ.Description" value="A WDTF SDEL query that is used to identify the target device(s) - http://go.microsoft.com/fwlink/p/?linkid=232678"/>
        <TestMethodProperty name="Kits.Parameter.DQ.Default" value="INF::OriginalInfFileName='%InfFileName%'"/>
        <TestMethodProperty name="RebootPossible" value="true" />
        <!-- TODO: Properties to be customized to match your test requirements -->
        <TestMethodProperty name="Description" value="Plug and Play Surprise Remove Generated Template"/>
        <TestMethodProperty name="Kits.DisplayName" value="My Plug and Play Surprise Remove Test"/>
        <TestMethodProperty name="Kits.Category" value="My Test Category"/>
        <!-- Optional properties for ERT-->
        <TestMethodProperty name="Kits.Drivers.ResultFile" value="TestTextLog.log"/>
        <!-- (see Windows Driver Kit documentation for additional optional properties) -->
        </method></code></pre></td>
    </tr>
    </tbody>
    </table>

3.  The following table describes the test property attributes. Use the examples for guidance as you edit or add the metadata for your tests.

    <span id="Description"></span><span id="description"></span><span id="DESCRIPTION"></span>**Description**  
    A short description of what the test does.

    <span codelanguage=""></span>
    <table>
    <colgroup>
    <col width="100%" />
    </colgroup>
    <tbody>
    <tr class="odd">
    <td align="left"><pre><code>[Script] 
      < TestProperty name="Description" value= "This test cycles the system through various sleep states and performs IO on devices before and after each sleep state cycle"/>
    </code></pre></td>
    </tr>
    </tbody>
    </table>

    <span codelanguage="ManagedCPlusPlus"></span>
    <table>
    <colgroup>
    <col width="100%" />
    </colgroup>
    <thead>
    <tr class="header">
    <th align="left">C++</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td align="left"><pre><code>[C++]
     TEST_METHOD_PROPERTY(L"Description", L"Plug and Play Surprise Remove Generated Template")</code></pre></td>
    </tr>
    </tbody>
    </table>

    <span id="DisplayName"></span><span id="displayname"></span><span id="DISPLAYNAME"></span>**DisplayName**  
    The name of the test as it shown in Driver Test.

    <span codelanguage=""></span>
    <table>
    <colgroup>
    <col width="100%" />
    </colgroup>
    <tbody>
    <tr class="odd">
    <td align="left"><pre><code>[Script] 
     < TestProperty name="Kits.DisplayName" value="Sleep with IO Before and After"/></code></pre></td>
    </tr>
    </tbody>
    </table>

    <span codelanguage="ManagedCPlusPlus"></span>
    <table>
    <colgroup>
    <col width="100%" />
    </colgroup>
    <thead>
    <tr class="header">
    <th align="left">C++</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td align="left"><pre><code> [C++]
      TEST_METHOD_PROPERTY(L"Kits.DisplayName", L"My Plug and Play Surprise Remove Test") </code></pre></td>
    </tr>
    </tbody>
    </table>

    <span id="Kits.Parameter"></span><span id="kits.parameter"></span><span id="KITS.PARAMETER"></span>**Kits.Parameter**  
    A standard parameter for a method call. A test can have multiple parameters.

    <span codelanguage=""></span>
    <table>
    <colgroup>
    <col width="100%" />
    </colgroup>
    <tbody>
    <tr class="odd">
    <td align="left"><pre><code>[Script] 
    <ModuleProperty name="Kits.Parameter" value="TM"/></code></pre></td>
    </tr>
    </tbody>
    </table>

    <span codelanguage="ManagedCPlusPlus"></span>
    <table>
    <colgroup>
    <col width="100%" />
    </colgroup>
    <thead>
    <tr class="header">
    <th align="left">C++</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td align="left"><pre><code>[C++]
    TEST_METHOD_PROPERTY(L"Kits.Parameter", L"DQ")</code></pre></td>
    </tr>
    </tbody>
    </table>

    <span id="Kits.Parameter._ParameterName_.Description"></span><span id="kits.parameter._parametername_.description"></span><span id="KITS.PARAMETER._PARAMETERNAME_.DESCRIPTION"></span>**Kits.Parameter.***&lt;ParameterName&gt;***.Description**  
    The description for the parameter.

    <span codelanguage=""></span>
    <table>
    <colgroup>
    <col width="100%" />
    </colgroup>
    <tbody>
    <tr class="odd">
    <td align="left"><pre><code>[Script] 
    < TestProperty name="Kits.Parameter.TM.Description" value="Test mode parameter: Logo or Simple"/> </code></pre></td>
    </tr>
    </tbody>
    </table>

    <span codelanguage="ManagedCPlusPlus"></span>
    <table>
    <colgroup>
    <col width="100%" />
    </colgroup>
    <thead>
    <tr class="header">
    <th align="left">C++</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td align="left"><pre><code> 
    [C++]
    TEST_METHOD_PROPERTY(L"Kits.Parameter.DQ.Description", L"A WDTF SDEL query that is used to identify the target device(s)")</code></pre></td>
    </tr>
    </tbody>
    </table>

    <span id="Kits.Parameter._ParameterName_.Default"></span><span id="kits.parameter._parametername_.default"></span><span id="KITS.PARAMETER._PARAMETERNAME_.DEFAULT"></span>**Kits.Parameter.***&lt;ParameterName&gt;***.Default**  
    The default value for the parameter.

    <span codelanguage=""></span>
    <table>
    <colgroup>
    <col width="100%" />
    </colgroup>
    <tbody>
    <tr class="odd">
    <td align="left"><pre><code>[Script] 
    < TestProperty name="Kits.Parameter.TM.Default" value="Logo"/></code></pre></td>
    </tr>
    </tbody>
    </table>

    <span codelanguage="ManagedCPlusPlus"></span>
    <table>
    <colgroup>
    <col width="100%" />
    </colgroup>
    <thead>
    <tr class="header">
    <th align="left">C++</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td align="left"><pre><code>[C++]
     TEST_METHOD_PROPERTY(L"Kits.Parameter.DQ.Default", L"INF::OriginalInfFileName='%InfFileName%'")  </code></pre></td>
    </tr>
    </tbody>
    </table>

    <span id="Kits.Drivers"></span><span id="kits.drivers"></span><span id="KITS.DRIVERS"></span>**Kits.Drivers**  
    This attribute marks the test for inclusion in the WDK.

    <span codelanguage=""></span>
    <table>
    <colgroup>
    <col width="100%" />
    </colgroup>
    <tbody>
    <tr class="odd">
    <td align="left"><pre><code>[Script] 
    < TestProperty name="Kits.Drivers" value=""/></code></pre></td>
    </tr>
    </tbody>
    </table>

    <span codelanguage="ManagedCPlusPlus"></span>
    <table>
    <colgroup>
    <col width="100%" />
    </colgroup>
    <thead>
    <tr class="header">
    <th align="left">C++</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td align="left"><pre><code>[C++]
     TEST_METHOD_PROPERTY(L"Kits.Drivers", L"TRUE")</code></pre></td>
    </tr>
    </tbody>
    </table>

    <span id="Kits.Category"></span><span id="kits.category"></span><span id="KITS.CATEGORY"></span>**Kits.Category**  
    Describes the category of a test.

    <span codelanguage=""></span>
    <table>
    <colgroup>
    <col width="100%" />
    </colgroup>
    <tbody>
    <tr class="odd">
    <td align="left"><pre><code> [Script] 
    < TestProperty name="Kits.Category" value="Logo\Device Fundamentals"/></code></pre></td>
    </tr>
    </tbody>
    </table>

    <span codelanguage="ManagedCPlusPlus"></span>
    <table>
    <colgroup>
    <col width="100%" />
    </colgroup>
    <thead>
    <tr class="header">
    <th align="left">C++</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td align="left"><pre><code> [C++]
    TEST_METHOD_PROPERTY(L"Kits.Category", L"My Test Category")</code></pre></td>
    </tr>
    </tbody>
    </table>

    <span id="Deploymentitem"></span><span id="deploymentitem"></span><span id="DEPLOYMENTITEM"></span>**Deploymentitem**  
    Identifies files and/or folders as test dependencies. These may contain any resources needed to run the tests. For more information about using this metadata, see [DeploymentItem Metadata](https://msdn.microsoft.com/en-us/Library/Windows/Hardware/Hh439604).

<span id="related_topics"></span>Related topics
-----------------------------------------------

* [How to write a driver test using a Driver Test template](how_to_write_a_driver_test_.md)





[send comments about this topic to microsoft](mailto:wsddocfb@microsoft.com?subject=documentation%20feedback%20[vsdriver\vsdriver]: %20How%20to%20add%20test%20metadata%20%20RELEASE:%20%289/30/2015%29&body=%0A%0APRIVACY%20STATEMENT%0A%0AWe%20use%20your%20feedback%20to%20improve%20the%20documentation.%20We%20don't%20use%20your%20email%20address%20for%20any%20other%20purpose,%20and%20we'll%20remove%20your%20email%20address%20from%20our%20system%20after%20the%20issue%20that%20you're%20reporting%20is%20fixed.%20While%20we're%20working%20to%20fix%20this%20issue,%20we%20might%20send%20you%20an%20email%20message%20to%20ask%20for%20more%20info.%20Later,%20we%20might%20also%20send%20you%20an%20email%20message%20to%20let%20you%20know%20that%20we've%20addressed%20your%20feedback.%0A%0AFor%20more%20info%20about%20Microsoft's%20privacy%20policy,%20see%20http://privacy.microsoft.com/en-us/default. "Send comments about this topic to Microsoft""
<!--HONumber=Jan16_HO2-->
