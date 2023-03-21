# homebridge-cmd4-bondbridge
For ceiling fan with **Hunter Pacific LOGIC remote control** via **Bond Bridge**

## Introduction
This `homebridge-cmd4-bondbridge` plugin is specially designed to control the ceiling fan with **[Hunter Pacific LOGIC remote control A2003](https://www.hunterpacificinternational.com/remotes)** (see image below) via **[Bond Bridge RF Controller](https://bondhome.io/product/bond-bridge/)**.

![image](https://user-images.githubusercontent.com/96530237/224465046-3ee8211e-c92c-4c8f-9119-77256fd9e0e9.png)

This plugin does not use the built-in timers but use customer-built timers within a bash script. These timers have greater flexibility and capability to turn on or off the fan and light.

## Installation:
### Raspbian/HOOBS/macOS/NAS:
1. If you have not already, install Homebridge via these instructions for [Raspbian](https://github.com/homebridge/homebridge/wiki/Install-Homebridge-on-Raspbian), [HOOBS](https://support.hoobs.org/docs) or [macOS](https://github.com/homebridge/homebridge/wiki/Install-Homebridge-on-macOS).
2. Install the [homebridge-cmd4](https://github.com/ztalbot2000/homebridge-cmd4) plug-in via the Homebridge UI ['plugins'](https://github.com/oznu/homebridge-config-ui-x#plugin-screen) tab search function. Once installed, a pop-up box with a small config in it will appear. Do not edit anything and make sure you click `SAVE`.
3. Install `homebridge-cmd4-bondbridge` plug-in via the Homebridge UI 'plugins' tab search function.
4. If you have not already, install  <B>jq</B> and <B>curl</B> via your terminal or Homebridge UI terminal or through ssh: 


     #### Raspbian/Hoobs:
     ```shell
     sudo apt-get install jq
     sudo apt-get install curl
     ```
     #### macOS:
     ```shell
     brew install jq
     brew install curl
     ```
     #### Synology NAS:

     ```shell
     apt-get install jq
     apt-get install curl
     ```
     #### QNAP NAS:

     ```shell
     apk add jq
     apk add curl
     ```

5. Create the configuration file needed to run this plugin:
     * Homebridge users with access to the Homebridge web UI can jump ahead to `Step 6`.
     * Other users (e.g. HOOBS users) who do not have access to  Homebridge UI will have to run the **ConfigCreator.sh** from your terminal.  Use the following terminal commands to locate and run the **ConfigCreator.sh**:
     ```shell
     cd
     config=$(find /usr 2>&1 | grep -v find | grep "homebridge-cmd4-bondbridge/ConfigCreator.sh$")
     echo "${config}"
     ``` 
     if `echo "${config}"` returns nothing, try the following:
     ```shell
     config=$(find /var/lib 2>&1 | grep -v find | grep "homebridge-cmd4-bondbridge/ConfigCreator.sh$")
     ``` 
     if `echo "${config}"` returns something then use the following command to run **ConfigCreator.sh**
     ```shell
     ${config}
     ``` 


6. Go to the 'plugins' tab in Homebridge UI and locate your newly installed `homebridge-cmd4-bondbridge`. Click `SETTINGS` and it should launch the 'Bond Bridge Configuration Creator'.

7. Scroll down to the 'Bond Bridge Device Settings' area and fill out the `IP Address` and `Token` of your Bond Bridge device (if you have more than one Bond Bridge devices, you can click `Add new device` to setup the others), and then click `SAVE`. It will close the UI and you will need to open it once more as per Step 6.
10. Tick/untick the `"Setup"` and `"Timer"`checkboxes depending what you would like to control in Homekit, then press the `CONFIG CREATOR` button; your Bond Bridge config will be created!
11. You may click `CHECK CONFIGURATION`to check the config created satisfies all requirements. On a success it will say `Passed`; if something is incorrect, an error message will pop up telling you what it is that you have missed and need to fix.

## Special Thanks:
1. Many thanks to [Mitch Williams](https://github.com/mitch7391) who has created the wonderful [Homebridge-cmd4-AdvantageAir](https://github.com/mitch7391/homebridge-cmd4-AdvantageAir) plugin and with which I have learnt so much in  bash and javascript coding in homebridge environment by allowing me to contribute to it.  
2. And never foeget to thank my beautiful wife who has put up with my obsession of sitting in front of a computer trying to get this plugin up and running.
