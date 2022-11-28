# WLAN low power

This code example demonstrates the low-power operation of a host MCU and a WLAN device using the network activity handlers provided by the [low power assistant (LPA) middleware](https://github.com/Infineon/lpa).

The code example connects to a configured network. After connecting to the network successfully, the example configures the WLAN device in a power-save mode, suspends the network stack, and puts the host MCU in a wait state. During this wait state, the host MCU enters a low-power state and wakes up on any network activity detected on the MAC interface.

[View this README on GitHub.](https://github.com/Infineon/mtb-example-wifi-wlan-lowpower)

[Provide feedback on this code example.](https://cypress.co1.qualtrics.com/jfe/form/SV_1NTns53sK2yiljn?Q_EED=eyJVbmlxdWUgRG9jIElkIjoiQ0UyMzAxMDYiLCJTcGVjIE51bWJlciI6IjAwMi0zMDEwNiIsIkRvYyBUaXRsZSI6IldMQU4gbG93IHBvd2VyIiwicmlkIjoic2RhayIsIkRvYyB2ZXJzaW9uIjoiNC4wLjAiLCJEb2MgTGFuZ3VhZ2UiOiJFbmdsaXNoIiwiRG9jIERpdmlzaW9uIjoiTUNEIiwiRG9jIEJVIjoiSUNXIiwiRG9jIEZhbWlseSI6IlBTT0MifQ==)

## Requirements

- [ModusToolbox&trade; software](https://www.infineon.com/modustoolbox) v3.0 or later (tested with v3.0)
- Board support package (BSP) minimum required version: 4.0.0
- Programming language: C
- Associated parts: All [PSoC&trade; 6 MCU](https://www.infineon.com/cms/en/product/microcontroller/32-bit-psoc-arm-cortex-microcontroller/psoc-6-32-bit-arm-cortex-m4-mcu) parts, [AIROC™ CYW43012 Wi-Fi & Bluetooth® combo chip](https://www.infineon.com/cms/en/product/wireless-connectivity/airoc-wi-fi-plus-bluetooth-combos/wi-fi-4-802.11n/cyw43012/), [AIROC™ CYW4343W Wi-Fi & Bluetooth® combo chip](https://www.infineon.com/cms/en/product/wireless-connectivity/airoc-wi-fi-plus-bluetooth-combos/cyw4343w/)


## Supported toolchains (make variable 'TOOLCHAIN')

- GNU Arm&reg; embedded compiler v10.3.1 (`GCC_ARM`) - Default value of `TOOLCHAIN`
- Arm&reg; compiler v6.16 (`ARM`)
- IAR C/C++ compiler v9.30.1 (`IAR`)

## Supported kits (make variable 'TARGET')

- [PSoC&trade; 6 Wi-Fi Bluetooth&reg; prototyping kit](https://www.infineon.com/CY8CPROTO-062-4343W) (`CY8CPROTO-062-4343W`) – Default value of `TARGET`
- [PSoC&trade; 6 Wi-Fi Bluetooth&reg; pioneer kit](https://www.infineon.com/CY8CKIT-062-WIFI-BT) (`CY8CKIT-062-WIFI-BT`)
- [PSoC&trade; 62S2 Wi-Fi Bluetooth&reg; pioneer kit](https://www.infineon.com/CY8CKIT-062S2-43012) (`CY8CKIT-062S2-43012`)
- [PSoC&trade; 62S1 Wi-Fi Bluetooth&reg; pioneer kit](https://www.infineon.com/CYW9P62S1-43438EVB-01) (`CYW9P62S1-43438EVB-01`)
- [PSoC&trade; 62S1 Wi-Fi Bluetooth&reg; pioneer kit](https://www.infineon.com/CYW9P62S1-43012EVB-01) (`CYW9P62S1-43012EVB-01`)
- Rapid IoT connect developer kit (`CYSBSYSKIT-DEV-01`)
- [PSoC&trade; 62S2 evaluation kit](https://www.infineon.com/CY8CEVAL-062S2) (`CY8CEVAL-062S2-LAI-4373M2`, `CY8CEVAL-062S2-MUR-43439M2`)
- [PSoC&trade; 64 "Secure Boot" Wi-Fi Bluetooth&reg; pioneer kit](https://www.infineon.com/CY8CKIT-064B0S2-4343W) (`CY8CKIT-064B0S2-4343W`)
- [PSoC&trade; 62S3 Wi-Fi Bluetooth&reg; prototyping kit](https://www.infineon.com/cms/en/product/evaluation-boards/cy8cproto-062s3-4343w) (`CY8CPROTO-062S3-4343W`)


## Hardware setup

This example uses the board's default configuration. See the kit user guide to ensure that the board is configured correctly.

**Note:** The PSoC&trade; 6 Bluetooth&reg; LE pioneer kit (CY8CKIT-062-BLE) and the PSoC&trade; 6 Wi-Fi Bluetooth&reg; pioneer kit (CY8CKIT-062-WIFI-BT) ship with KitProg2 installed. The ModusToolbox&trade; software requires KitProg3. Before using this code example, make sure that the board is upgraded to KitProg3. The tool and instructions are available in the [Firmware Loader](https://github.com/Infineon/Firmware-loader) GitHub repository. If you do not upgrade, you will see an error like "unable to find CMSIS-DAP device" or "KitProg firmware is out of date".


## Software setup

Install a terminal emulator if you don't have one. Instructions in this document use [Tera Term](https://ttssh2.osdn.jp/index.html.en).

This example requires no additional software or tools.


## Using the code example

Create the project and open it using one of the following:

<details><summary><b>In Eclipse IDE for ModusToolbox&trade; software</b></summary>

1. Click the **New Application** link in the **Quick Panel** (or, use **File** > **New** > **ModusToolbox&trade; Application**). This launches the [Project Creator](https://www.infineon.com/ModusToolboxProjectCreator) tool.

2. Pick a kit supported by the code example from the list shown in the **Project Creator - Choose Board Support Package (BSP)** dialog.

   When you select a supported kit, the example is reconfigured automatically to work with the kit. To work with a different supported kit later, use the [Library Manager](https://www.infineon.com/ModusToolboxLibraryManager) to choose the BSP for the supported kit. You can use the Library Manager to select or update the BSP and firmware libraries used in this application. To access the Library Manager, click the link from the **Quick Panel**.

   You can also just start the application creation process again and select a different kit.

   If you want to use the application for a kit not listed here, you may need to update the source files. If the kit does not have the required resources, the application may not work.

3. In the **Project Creator - Select Application** dialog, choose the example by enabling the checkbox.

4. (Optional) Change the suggested **New Application Name**.

5. The **Application(s) Root Path** defaults to the Eclipse workspace which is usually the desired location for the application. If you want to store the application in a different location, you can change the *Application(s) Root Path* value. Applications that share libraries should be in the same root path.

6. Click **Create** to complete the application creation process.

For more details, see the [Eclipse IDE for ModusToolbox&trade; software user guide](https://www.infineon.com/MTBEclipseIDEUserGuide) (locally available at *{ModusToolbox&trade; software install directory}/docs_{version}/mtb_ide_user_guide.pdf*).

</details>

<details><summary><b>In command-line interface (CLI)</b></summary>

ModusToolbox&trade; software provides the Project Creator as both a GUI tool and the command line tool, "project-creator-cli". The CLI tool can be used to create applications from a CLI terminal or from within batch files or shell scripts. This tool is available in the *{ModusToolbox&trade; software install directory}/tools_{version}/project-creator/* directory.

Use a CLI terminal to invoke the "project-creator-cli" tool. On Windows, use the command line "modus-shell" program provided in the ModusToolbox&trade; software installation instead of a standard Windows command-line application. This shell provides access to all ModusToolbox&trade; software tools. You can access it by typing `modus-shell` in the search box in the Windows menu. In Linux and macOS, you can use any terminal application.

This tool has the following arguments:

Argument | Description | Required/optional
---------|-------------|-----------
`--board-id` | Defined in the `<id>` field of the [BSP](https://github.com/Infineon?q=bsp-manifest&type=&language=&sort=) manifest | Required
`--app-id`   | Defined in the `<id>` field of the [CE](https://github.com/Infineon?q=ce-manifest&type=&language=&sort=) manifest | Required
`--target-dir`| Specify the directory in which the application is to be created if you prefer not to use the default current working directory | Optional
`--user-app-name`| Specify the name of the application if you prefer to have a name other than the example's default name | Optional

<br />

The following example clones the "[WLAN low power](https://github.com/Infineon/mtb-example-anycloud-wlan-lowpower)" application with the desired name "WlanLP" configured for the *CY8CPROTO-062-4343W* BSP into the specified working directory, *C:/mtb_projects*:

   ```
   project-creator-cli --board-id CY8CPROTO-062-4343W --app-id mtb-example-wlan-lowpower --user-app-name WlanLP --target-dir "C:/mtb_projects"
   ```

**Note:** The project-creator-cli tool uses the `git clone` and `make getlibs` commands to fetch the repository and import the required libraries. For details, see the "Project creator tools" section of the [ModusToolbox&trade; software user guide](https://www.infineon.com/ModusToolboxUserGuide) (locally available at *{ModusToolbox&trade; software install directory}/docs_{version}/mtb_user_guide.pdf*).

To work with a different supported kit later, use the [Library Manager](https://www.infineon.com/ModusToolboxLibraryManager) to choose the BSP for the supported kit. You can invoke the Library Manager GUI tool from the terminal using the `make library-manager` command or use the Library Manager CLI tool "library-manager-cli" to change the BSP.

The "library-manager-cli" tool has the following arguments:

Argument | Description | Required/optional
---------|-------------|-----------
`--add-bsp-name` | Name of the BSP that should be added to the application | Required
`--set-active-bsp` | Name of the BSP that should be as active BSP for the application | Required
`--add-bsp-version`| Specify the version of the BSP that should be added to the application if you do not wish to use the latest from manifest | Optional
`--add-bsp-location`| Specify the location of the BSP (local/shared) if you prefer to add the BSP in a shared path | Optional

<br />

Following example adds the CY8CPROTO-062-4343W BSP to the already created application and makes it the active BSP for the app:

   ```
   library-manager-cli --project "C:/mtb_projects/WlanLP" --add-bsp-name CY8CPROTO-062-4343W --add-bsp-version "latest-v4.X" --add-bsp-location "local"

   library-manager-cli --project "C:/mtb_projects/WlanLP" --set-active-bsp APP_CY8CPROTO-062-4343W
   ```

</details>

<details><summary><b>In third-party IDEs</b></summary>

Use one of the following options:

- **Use the standalone [Project Creator](https://www.infineon.com/ModusToolboxProjectCreator) tool:**

   1. Launch Project Creator from the Windows Start menu or from *{ModusToolbox&trade; software install directory}/tools_{version}/project-creator/project-creator.exe*.

   2. In the initial **Choose Board Support Package** screen, select the BSP, and click **Next**.

   3. In the **Select Application** screen, select the appropriate IDE from the **Target IDE** drop-down menu.

   4. Click **Create** and follow the instructions printed in the bottom pane to import or open the exported project in the respective IDE.

<br />

- **Use command-line interface (CLI):**

   1. Follow the instructions from the **In command-line interface (CLI)** section to create the application, and then import the libraries using the `make getlibs` command.

   2. Export the application to a supported IDE using the `make <ide>` command.

   3. Follow the instructions displayed in the terminal to create or import the application as an IDE project.

For a list of supported IDEs and more details, see the "Exporting to IDEs" section of the [ModusToolbox&trade; software user guide](https://www.infineon.com/ModusToolboxUserGuide) (locally available at *{ModusToolbox&trade; software install directory}/docs_{version}/mtb_user_guide.pdf*).

</details>


##  Operation

1. Connect the board to your PC using the provided USB cable through the KitProg3 USB connector.

2. Modify the `WIFI_SSID`, `WIFI_PASSWORD`, and `WIFI_SECURITY` macros to match the credentials of the Wi-Fi network that you want to connect to. These macros are defined in the *lowpower_task.h* file.

   **Note:** See the AP's configuration page for the security type. See the `cy_wcm_security_t` enumeration in *cy_wcm.h* to pass the corresponding WCM security type in the `WIFI_SECURITY` macro.

3. Ensure that your PC is connected to the same Wi-Fi AP that you have configured in **Step 2**.

4. Open a terminal program and select the KitProg3 COM port. Set the serial port parameters to 8N1 and 115200 baud.

5. Program the board using one of the following:

   <details><summary><b>Using Eclipse IDE for ModusToolbox&trade; software</b></summary>

      1. Select the application project in the Project Explorer.

      2. In the **Quick Panel**, scroll down, and click **\<Application Name> Program (KitProg3_MiniProg4)**.
   </details>

   <details><summary><b>Using CLI</b></summary>

     From the terminal, execute the `make program` command to build and program the application using the default toolchain to the default target. The default toolchain and target are specified in the application's Makefile but you can override those values manually:
      ```
      make program TOOLCHAIN=<toolchain>
      ```

      Example:
      ```
      make program TOOLCHAIN=GCC_ARM
      ```
   </details>

      **Note:** Before building the application, ensure that the *deps* folder contains the BSP file (*TARGET_xxx.lib*) corresponding to the TARGET. Execute the `make getlibs` command to fetch the BSP contents before building the application.

6. After programming, the example starts automatically. The example connects to the AP and suspends the network stack.

   **Figure 1. Connect to AP and suspend the network stack**

   ![](images/figure1.png)

7. Open a command prompt and ping the IP address displayed on the serial terminal:

    ```
    ping <IP address>
    ```

   The network stack is resumed. The device displays the deep sleep and Wi-Fi SDIO bus statistics on the terminal. The LED is toggled after resuming the network stack after which the network stack is again suspended until network activity is detected.

   **Note:** The host MCU will wake up on any network activity and not necessarily due to the ping from the PC. The reasons for network activity could be due to the broadcast or multicast packets issued by the AP. Further power savings can be made by employing offload features like packet filtering, which will increase the time the host MCU will be in deep sleep. See [AN227910 - Low-power system design with AIROC&trade; CYW43012 Wi-Fi & Bluetooth&reg; combo chip and PSoC&trade; 6 MCU](https://www.infineon.com/dgdl/Infineon-AN227910_Low-power_system_design_with_AIROC_CYW43012_Wi-Fi_%26_Bluetooth_combo_chip_and_PSoC_6_MCU-ApplicationNotes-v03_00-EN.pdf?fileId=8ac78c8c7cdc391c017d0d39b66166f3&utm_source=cypress&utm_medium=referral&utm_campaign=202110_globe_en_all_integration-application_note) for more details.

    **Figure 2. Resuming the network stack**

    ![](images/figure2.png)

See [Measuring the current consumption](#measuring-the-current-consumption) for instructions on how to measure the current consumed by the PSoC&trade; 6 MCU and the Wi-Fi device.


##  Debugging

You can debug the example to step through the code. In the IDE, use the **\<Application Name> Debug (KitProg3_MiniProg4)** configuration in the **Quick Panel**. For details, see the "Program and debug" section in the [Eclipse IDE for ModusToolbox&trade; software user guide](https://www.infineon.com/MTBEclipseIDEUserGuide).

**Note:** **(Only while debugging)** On the CM4 CPU, some code in `main()` may execute before the debugger halts at the beginning of `main()`. This means that some code executes twice – once before the debugger stops execution, and again after the debugger resets the program counter to the beginning of `main()`. See [KBA231071](https://community.infineon.com/docs/DOC-21143) to learn about this and for the workaround.


##  Design and implementation

The example uses the [lwIP](https://savannah.nongnu.org/projects/lwip) network stack, which runs multiple network timers for various network-related activities. These timers need to be serviced by the host MCU. As a result, the host MCU will not be able to stay in sleep or deep sleep state longer.

In this example, after successfully connecting to an AP, the host MCU suspends the network stack after a period of inactivity. The example uses two macros, `INACTIVE_INTERVAL_MS` and `INACTIVE_WINDOW_MS`, to determine whether the network is inactive. Monitors the network for inactivity in an interval of length `INACTIVE_INTERVAL_MS`. If the network is inactive for a continuous duration specified by `INACTIVE_WINDOW_MS`, the network stack will be suspended until there is network activity.

The host MCU is alerted by the WLAN device on network activity, after which the network stack resumes. The host MCU is in deep sleep during the time the network stack is suspended. Because there are no network timers to be serviced, the host MCU stays in deep sleep for longer. This state where the host MCU is in deep sleep waiting for network activity is referred to as the "wait state".

On the other hand, the WLAN device is configured in one of the supported power-save modes:

1. **Power-save with poll:** This mode corresponds to (legacy) 802.11 PS-Poll mode and should be used to achieve the lowest power consumption possible when the Wi-Fi device is primarily passively listening to the network.

2. **Power-save without poll:** This mode attempts to increase the throughput by waiting for a timeout period before returning to sleep rather than returning to sleep immediately.

Set the power-save mode through the `WLAN_POWERSAVE_MODE` macro. The WLAN device wakes at every DTIM interval to receive beacon frames from the AP.

For more information on low-power system design that involves offloading tasks to the WLAN device for even better power savings, see [AN227910 - Low-power system design with AIROC&trade; CYW43012 Wi-Fi & Bluetooth&reg; combo chip and PSoC&trade; 6 MCU](https://www.infineon.com/dgdl/Infineon-AN227910_Low-power_system_design_with_CYW43012_and_PSoC_6_MCU-ApplicationNotes-v02_00-EN.pdf?fileId=8ac78c8c7cdc391c017d0d39b66166f3).


###  Creating a custom device configuration for low power

This code example overrides the default device configuration provided by library-manager or bsp-assistance with the one provided in *<application_folder>/templates/TARGET_\<kit>* for the supported kits.

**Note:** This section provides instructions only for the targets CY8CPROTO-062-4343W and CY8CKIT-062S2-43012. For other targets, you can follow the same instructions to create a custom configuration. See the *bsps/TARGET_\<kit>/configs/GeneratedSource/cycfg_pins.h* file for pin details such as CYBSP_WIFI_HOST_WAKE.

The custom configuration disables the phase-locked loop (PLL) and HF clock for unused peripherals such as audio or USB, and configures the buck regulator instead of the low dropout (LDO) regulator to power the PSoC&trade; 6 MCU device. This configuration reduces the current consumed by the PSoC&trade; 6 MCU device in an active state.

If your application uses any of the disabled peripherals, the corresponding peripherals and clocks should be enabled using the device configurator. Launch this tool from the **Quick Panel** inside the Eclipse IDE for ModusToolbox&trade; software or from the command line using the following command:

```
make config TARGET=<TARGET-KIT-NAME>
```

For example,

```
make config TARGET=CY8CKIT-062S2-43012
```

Do the following to create a custom configuration for a new kit:

1. Create a new directory inside *templates* with the same name as the target you are building the example for, such as *<application_folder>/templates/TARGET_\<kit>*.

2. Copy the design.modus of the default bsp into the folder created in the previous step <application_folder>/templates/TARGET_\<kit>*/design.modus.

3. Open the copied *design.modus* file using the device configurator.

4. On the PSoC&trade; 6 MCU **Pins** tab of the device configurator, do the following:

   **CY8CKIT-062S2-43012:**

   1. Enable the Host WAKE pin **P4[1]** and name it *CYBSP_WIFI_HOST_WAKE*.

   2. In the **Parameters** pane, change the following:

      - **Drive Mode:**: Analog High-Z. Input buffer off

      - **Initial Drive State**: High(1)

      - **Interrupt Trigger Type**: Rising Edge

      **Figure 3. Configuring the Host WAKE pin for CY8CKIT-062S2-43012**

      ![](images/figure3.png)

   <br>

   **CY8CPROTO-062-4343W:**

   1. Enable the Host WAKE pin **P0[4]**, and name it *CYBSP_WIFI_HOST_WAKE*.

   2. In the **Parameters** pane, change the following:

      - **Drive Mode**: Analog High-Z. Input buffer off

      - **Initial Drive State**: High(1)

      - **Interrupt Trigger Type**: Rising Edge

      **Figure 4. Configuring the Host WAKE pin for CY8CPROTO-062-4343W**

      ![](images/figure4.png)

   **Note:** The Wi-Fi host driver takes care of the drive mode configuration of the Host WAKE pin.

5. Go to the **Wi-Fi** tab and enable the host wake configuration and set **Host Device Interrupt Pin** to **CYBSP_WIFI_HOST_WAKE**. This configuration applies to all [supported kits](#supported-kits).

    **Figure 5. Enable Host Wake pin**

    ![](images/figure5.png)

6. Switch to the **System** tab, expand the **System Clocks** resource, and do the following:

   1. Clear the box in the **FLL+PLL** section to disable the PLL.

   2. In the **High-Frequency** section, disable HF clocks for the peripherals that are not being used in this code example.

      Do the following kit-specific changes:

   <br>

   **CY8CKIT-062S2-43012:**

   1. Disable PLL0 and PLL1, and High-Frequency clocks CLK_HF2 and CLK_HF3.

   2. PLL is the source clock for CLK_HF0. After disabling the PLL, change the source clock for CLK_HF0 to **FLL**.

      **Figure 6. Clock settings in CY8CKIT-062S2-43012**

      ![](images/figure6.png)

   3. In the **System Clocks** resource, select **CLK_HF0** and modify the **Source Clock** to **CLK_PATH0**.

      **Figure 7. CLK_HF0 settings for CY8CKIT-062S2-43012**

      ![](images/figure7.png)

   <br>

   **CY8CPROTO-062-4343W:**

   1. Disable PLL1 and High-Frequency clocks CLK_HF2 & CLK_HF3.

      **Figure 8. Clock settings in CY8CPROTO-062-4343W**

      ![](images/figure8.png)

7. Under the **Power** resource, change the **Core Regulator** under **General** to **Buck**.

   **Figure 9. Configuring the core regulator as buck**

   ![](images/figure9.png)

8. Optionally, you can make higher power savings by switching to ULP mode. However, this mode requires the CM4 CPU to be limited to a maximum operating frequency of 50 MHz.

   **CY8CPROTO-062-4343W:**

   1. Under the **Power** resource, change the **System Active Power Mode** under **General** to **ULP**.

      Note that switching to ULP causes a few errors to appear for FLL and CLK_PERI because their frequencies are greater than 50 MHz and 25 MHz respectively.

      **Figure 10. Configuring System Active power mode**

      ![](images/figure10.png)

   2. Under the **System** tab, expand the **System Clocks** resource, select **FLL**, and modify the **Desired Frequency** to **50.000 MHz**.

      **Figure 11. FLL settings**

      ![](images/figure11.png)

   3. In the **System Clocks** resource, select **CLK_PERI** and modify the **Divider** to **2**.

      **Figure 12. CLK_PERI settings**

      ![](images/figure12.png)

   <br>

   **CY8CKIT-062S2-43012:**

   1. Under the **Power** resource, change the **System Active Power Mode** under **General** to **ULP**.

      Note that switching to ULP causes a few errors to appear for FLL and CLK_PEI because their frequencies are greater than 50 MHz and 25 MHz respectively.

      **Figure 13. Configuring System Active power mode**

      ![](images/figure13.png)

    2. Under the **System** tab, expand the **System Clocks** resource, select **FLL**, and modify the **Desired Frequency** to **50.000 MHz**.

        **Figure 14. FLL settings**

        ![](images/figure14.png)

9. Save the file to generate the source files.

   **Note:** See the schematic to determine the LED which is not powered directly by *P6_VDD*. If the LED is connected directly to P6_VDD, the LED current consumed will be added to the current measurement of the PSoC&trade; 6 MCU device. Find the corresponding macro for that LED in *cybsp_types.h* at *<application_folder>/libs/TARGET_\<kit>/cybsp_types.h*. Provide that macro as the value for `USER_LED` in *lowpower_task.h*.


##  Measuring the current consumption

###  CY8CKIT-062S2-43012, CYW9P62S1-43438EVB-01, and CYW9P62S1-43012EVB-01

**For PSoC&trade; 6 MCU:**

   1. Remove J25 to eliminate leakage currents across potentiometer R1.

   2. Measure the current at J15 across VTARG and P6_VDD.

**For CYW43xxx:**

   1. Measure the current at supplies VDDIO_WL used for SDIO communication interface and at VBAT used for powering CYW43xxx.

   2. Measure the current at VDDIO_WL across VDDIO_WL and VCC_VDDIO2 at J17.

   3. Measure the current at VBAT across VBAT and VCC_VBAT at J8.

**Note:** The level translator, U17, consumes approximately 110 uA and adds this leakage when measuring across VDDIO_WL. Therefore, remove U17 which is on the back of the board below J3.1. In addition, remove R114 to disconnect WL_JTAG_SEL from VDDIO_WL.


###  CYSBSYSKIT-DEV-01

**For CYSBSYS-RP01 module VBAT_WL:**

   1. Remove R174 on the back of the board towards the right and near J1.12.

   2. Connect an ammeter between the pads of R174 to measure the VBAT_WL current.

**For CYSBSYS-RP01 module VDDIO_WL:**

   1. Remove R160 on the back of the board towards the right and below R174.

   2. Connect an ammeter between the pads of R160 to measure the VDDIO_WL current.

**For CYSBSYS-RP01 module VDDD:**

   1. Remove R158 on the back of the board towards the left and near J5.15.

   2. Connect an ammeter between the pads of R158 to measure the current.

**For CYSBSYS-RP01 module VBACKUP:**

   1. Remove R182 on the back of the board towards the left and above J5.14.

   2. Connect an ammeter between the pads of R182 to measure the current.

**For CYSBSYS-RP01 module VDDIO0:**

   1. Remove R13 on the back of the board towards the left and above J5.16.

   2. Connect an ammeter between the pads of R13 to measure the current.

**For CYSBSYS-RP01 module VDDIO1:**

   1. Remove R178 on the back of the board towards the left and near U3 IC.

   2. Connect an ammeter between the pads of R178 to measure the current.

**For CYSBSYS-RP01 module VDDUSB:**

   1. Remove R15 on the back of the board towards the left and above J5.16.

   2. Connect an ammeter between the pads of R15 to measure the current.


###  CY8CPROTO-062-4343W

**For PSoC&trade; 6 MCU:**

   1. Remove R65 on the right of the board close to the USB connector of the PSoC&trade; 6 MCU device.

   2. Connect an ammeter between VTARG (J2.32) and P6_VDD (J2.24).

   3. Remove R24 at the back of the board, below J1.9, to eliminate the leakage current.

      R24 is the pull-up resistor attached to the WL_HOST_WAKE pin P0_4, which leaks approximately 330 uA because P0_4 is driven LOW when there is no network activity. In total, the PSoC&trade; 6 MCU deep sleep current is approximately 350 uA.

**For CYW4343W:**

Measure the current at the VDDIO_1LV supply used for the SDIO communication interface, and at VBAT1 and VBAT2 supplies used for powering CYW4343W. VBAT1 and VABT2 are shorted to each other.

1. Remove R87 on the back of the board towards the right and above J2.33.

2. Connect an ammeter between the pads of R87 to measure the current.

3. Measure the current at VDDIO_1LV:

   1. Remove the resistor R86 on the back of the board below J1.27.

   2. Connect an ammeter between the pads of R86 to measure the current.

Note that the current at VDDIO_1LV depends on the SDIO transactions that happen because of the pull-up resistors on the lines to VDDIO_1LV. Also, VDDIO_1LV (named VDDIO_1DX in the carrier module (CY8CMOD_062_4343W) schematic) allows a current of 38 uA through R24 because WL_HOST_WAKE is LOW. This current needs to be deducted from the observed value of VDDIO_1LV.


###  CY8CKIT-062-WIFI-BT

**For PSoC&trade; 6 MCU:**

1. Measure the current by connecting an ammeter to the PWR MON jumper J8.

**For CYW4343W:**

1. Measure the current at WL_VDDIO used for the SDIO communication interface and at WL_VBAT used for powering CYW4343W.

2. Measure the current at WL_VBAT by removing L3 along the right edge of the board close to the CYW4343W module and connecting an ammeter between the pads of L3.

3. Measure the current at WL_VDDIO by removing L7 on the top left corner of the back of the board, and connecting an ammeter between the pads of L7.


##  Typical current measurement values

The following table provides the typical current measurement values for the CY8CKIT-062S2-43012 kit. All measurements were made in the presence of external radio interference and not in an isolated environment with a single AP. Note that the typical values of current consumed by the supply powering the SDIO interface between the host MCU and WLAN device are not provided because the value of current varies with the transaction over the interface.

Here, PSoC&trade; 6 MCU is operated with Arm® Cortex®-M4 running at 50 MHz in ultra-low-power (ULP) mode with full RAM retention.

**Table 1. Typical current values for CY8CKIT_062S2_43012**

<table style="width:80%">
<tr><th>State</th><th>Device</th><th>Current</th></tr>
        <tr>
            <td rowspan=2>Deep sleep</td>
            <td>PSoC&trade; 6 MCU</td>
            <td> 12.1 uA</td>
        </tr>
        <tr>
            <td>CYW43012 (VBAT)</td>
            <td> 2.3 uA</td>
        </tr>
        <tr>
            <td rowspan=2>Average current over 3 DTIM periods for<br>AP (2.4 GHz) beacon interval of 100 and<br>AP DTIM of 1</td>
            <td>PSoC&trade; 6 MCU</td>
            <td> 12 uA</td>
        </tr>
        <tr>
            <td>CYW43012 (VBAT)</td>
            <td> 476 uA</td>
        </tr>
        <tr>
            <td rowspan=2>Average current over 3 DTIM periods for<br>AP (2.4 GHz) beacon interval of 100 and<br>AP DTIM of 3</td>
            <td>PSoC&trade; 6 MCU</td>
            <td> 12.1 uA</td>
        </tr>
        <tr>
            <td>CYW43012 (VBAT)</td>
            <td> 131 uA</td>
        </tr>
        <tr>
            <td rowspan=2>Average current over 3 DTIM periods for<br>AP (5 GHz) beacon interval of 100 and<br>AP DTIM of 1</td>
            <td>PSoC&trade; 6 MCU</td>
            <td> 12 uA</td>
        </tr>
        <tr>
            <td>CYW43012 (VBAT)</td>
            <td> 220 uA</td>
        </tr>
        <tr>
            <td rowspan=2>Average current over 3 DTIM periods for<br>AP (5 GHz) beacon interval of 100 and<br> AP DTIM of 3</td>
            <td>PSoC&trade; 6 MCU</td>
            <td> 12 uA</td>
        </tr>
        <tr>
            <td>CYW43012 (VBAT)</td>
            <td> 87 uA</td>
        </tr>
 </table>

<br>

## Related resources


Resources  | Links
-----------|----------------------------------
Application notes  | [AN228571](https://www.infineon.com/AN228571) – Getting started with PSoC&trade; 6 MCU on ModusToolbox&trade; software <br>  [AN215656](https://www.infineon.com/AN215656) – PSoC&trade; 6 MCU: Dual-CPU system design <br> [AN79953](https://www.infineon.com/AN79953) – Getting started with PSoC&trade; 4 <br>  [AN85951](https://www.infineon.com/AN85951) – PSoC&trade; 4 and PSoC&trade; 6 MCU CAPSENSE&trade; design guide
Code examples | [Using ModusToolbox&trade; software](https://github.com/Infineon/Code-Examples-for-ModusToolbox-Software) on GitHub <br> [Using PSoC&trade; Creator](https://www.infineon.com/cms/en/design-support/software/code-examples/psoc-3-4-5-code-examples-for-psoc-creator)
Device documentation | Download datasheets, TRMs, and other documents from the [PSoC&trade; 6 product page](https://www.infineon.com/cms/en/product/microcontroller/32-bit-psoc-arm-cortex-microcontroller/psoc-6-32-bit-arm-cortex-m4-mcu) <br> Download datasheets, TRMs, and other documents from the [PSoC&trade; 4 product page](https://www.infineon.com/cms/en/product/microcontroller/32-bit-psoc-arm-cortex-microcontroller/psoc-4-32-bit-arm-cortex-m0-mcu)
Development kits | Select your kits from the [Evaluation board finder](https://www.infineon.com/cms/en/design-support/finder-selection-tools/product-finder/evaluation-board) page
Libraries on GitHub  | [mtb-pdl-cat1](https://github.com/Infineon/mtb-pdl-cat1) – PSoC&trade; 6 peripheral driver library (PDL)  <br> [mtb-hal-cat1](https://github.com/Infineon/mtb-hal-cat1) – Hardware abstraction layer (HAL) library <br> [retarget-io](https://github.com/Infineon/retarget-io) – Utility library to retarget STDIO messages to a UART port <br>  [mtb-pdl-cat2](https://github.com/Infineon/mtb-pdl-cat2) – PSoC&trade; 4 peripheral driver library (PDL) <br>  [mtb-hal-cat2](https://github.com/Infineon/mtb-hal-cat2) – Hardware abstraction layer (HAL) library
Middleware on GitHub  | [capsense](https://github.com/Infineon/capsense) – CAPSENSE&trade; library and documents <br> [psoc6-middleware](https://github.com/Infineon/modustoolbox-software#psoc-6-middleware-libraries) – Links to all PSoC&trade; 6 MCU middleware
Tools  | [Eclipse IDE for ModusToolbox&trade; software](https://www.infineon.com/modustoolbox) – ModusToolbox&trade; software is a collection of easy-to-use software and tools enabling rapid development with Infineon MCUs, covering applications from embedded sense and control to wireless and cloud-connected systems using AIROC&trade; Wi-Fi and Bluetooth® connectivity devices. <br> [PSoC&trade; Creator](https://www.infineon.com/cms/en/design-support/tools/sdk/psoc-software/psoc-creator) – IDE for PSoC&trade; and FM0+ MCU development

<br />

## Other resources


Infineon provides a wealth of data at www.infineon.com to help you select the right device, and quickly and effectively integrate it into your design.

For PSoC&trade; 6 MCU devices, see [How to design with PSoC&trade; 6 MCU - KBA223067](https://community.infineon.com/docs/DOC-14644) in the Infineon community.


## Document history

Document title: *CE230106* - *WLAN low power*

 Version | Description of change
 ------- | ---------------------
 1.0.0   | New code example
 1.1.0   | Minor changes in Makefile and source files
 2.0.0   | Major update to support ModusToolbox&trade; software v2.2 and LPA v3.0.0.<br/>This version is not backward compatible with ModusToolbox&trade; software v2.1.
 2.1.0   | Added support for Rapid IoT Connect Developer Kit (CYSBSYSKIT-DEV-01)
 2.2.0   | Updated to FreeRTOS v10.3.1
 2.3.0   | Added support for new kits
 3.0.0   | Updated to BSP v3.X and added support for new kits
 4.0.0   | Major update to support ModusToolbox&trade; v3.0. <br> This version is not backward compatible with previous versions of ModusToolbox&trade; software.

<br>

---------------------------------------------------------

© Cypress Semiconductor Corporation, 2020-2022. This document is the property of Cypress Semiconductor Corporation, an Infineon Technologies company, and its affiliates ("Cypress").  This document, including any software or firmware included or referenced in this document ("Software"), is owned by Cypress under the intellectual property laws and treaties of the United States and other countries worldwide.  Cypress reserves all rights under such laws and treaties and does not, except as specifically stated in this paragraph, grant any license under its patents, copyrights, trademarks, or other intellectual property rights.  If the Software is not accompanied by a license agreement and you do not otherwise have a written agreement with Cypress governing the use of the Software, then Cypress hereby grants you a personal, non-exclusive, nontransferable license (without the right to sublicense) (1) under its copyright rights in the Software (a) for Software provided in source code form, to modify and reproduce the Software solely for use with Cypress hardware products, only internally within your organization, and (b) to distribute the Software in binary code form externally to end users (either directly or indirectly through resellers and distributors), solely for use on Cypress hardware product units, and (2) under those claims of Cypress’s patents that are infringed by the Software (as provided by Cypress, unmodified) to make, use, distribute, and import the Software solely for use with Cypress hardware products.  Any other use, reproduction, modification, translation, or compilation of the Software is prohibited.
<br />
TO THE EXTENT PERMITTED BY APPLICABLE LAW, CYPRESS MAKES NO WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, WITH REGARD TO THIS DOCUMENT OR ANY SOFTWARE OR ACCOMPANYING HARDWARE, INCLUDING, BUT NOT LIMITED TO, THE IMPLIED WARRANTIES OF MERCHANTABILITY AND FITNESS FOR A PARTICULAR PURPOSE.  No computing device can be absolutely secure.  Therefore, despite security measures implemented in Cypress hardware or software products, Cypress shall have no liability arising out of any security breach, such as unauthorized access to or use of a Cypress product. CYPRESS DOES NOT REPRESENT, WARRANT, OR GUARANTEE THAT CYPRESS PRODUCTS, OR SYSTEMS CREATED USING CYPRESS PRODUCTS, WILL BE FREE FROM CORRUPTION, ATTACK, VIRUSES, INTERFERENCE, HACKING, DATA LOSS OR THEFT, OR OTHER SECURITY INTRUSION (collectively, "Security Breach").  Cypress disclaims any liability relating to any Security Breach, and you shall and hereby do release Cypress from any claim, damage, or other liability arising from any Security Breach.  In addition, the products described in these materials may contain design defects or errors known as errata which may cause the product to deviate from published specifications. To the extent permitted by applicable law, Cypress reserves the right to make changes to this document without further notice. Cypress does not assume any liability arising out of the application or use of any product or circuit described in this document. Any information provided in this document, including any sample design information or programming code, is provided only for reference purposes.  It is the responsibility of the user of this document to properly design, program, and test the functionality and safety of any application made of this information and any resulting product.  "High-Risk Device" means any device or system whose failure could cause personal injury, death, or property damage.  Examples of High-Risk Devices are weapons, nuclear installations, surgical implants, and other medical devices.  "Critical Component" means any component of a High-Risk Device whose failure to perform can be reasonably expected to cause, directly or indirectly, the failure of the High-Risk Device, or to affect its safety or effectiveness.  Cypress is not liable, in whole or in part, and you shall and hereby do release Cypress from any claim, damage, or other liability arising from any use of a Cypress product as a Critical Component in a High-Risk Device. You shall indemnify and hold Cypress, including its affiliates, and its directors, officers, employees, agents, distributors, and assigns harmless from and against all claims, costs, damages, and expenses, arising out of any claim, including claims for product liability, personal injury or death, or property damage arising from any use of a Cypress product as a Critical Component in a High-Risk Device. Cypress products are not intended or authorized for use as a Critical Component in any High-Risk Device except to the limited extent that (i) Cypress’s published data sheet for the product explicitly states Cypress has qualified the product for use in a specific High-Risk Device, or (ii) Cypress has given you advance written authorization to use the product as a Critical Component in the specific High-Risk Device and you have signed a separate indemnification agreement.
<br />
Cypress, the Cypress logo, and combinations thereof, WICED, ModusToolbox, PSoC, CapSense, EZ-USB, F-RAM, and Traveo are trademarks or registered trademarks of Cypress or a subsidiary of Cypress in the United States or in other countries. For a more complete list of Cypress trademarks, visit cypress.com. Other names and brands may be claimed as property of their respective owners.
