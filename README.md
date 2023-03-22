# homebridge-cmd4-bondbridge
For ceiling fans fitted with **Hunter Pacific LOGIC remote control** or **equivalent** via **Bond Bridge RF Controller**

## Introduction

This `homebridge-cmd4-bondbridge` plugin is specially designed to control ceiling fans fitted with **[Hunter Pacific LOGIC remote control A2003](https://www.hunterpacificinternational.com/remotes)** (see image below) or **equivalent** via **[Bond Bridge RF Controller](https://bondhome.io/product/bond-bridge/)**.

![image](https://user-images.githubusercontent.com/96530237/224465046-3ee8211e-c92c-4c8f-9119-77256fd9e0e9.png)

You can make use of this plugin only if your ceiling fan remote is not in the Bond Bridge database and it has a Light with Dimmer, otherwise you should use the **[homebridge-bond](https://github.com/aarons22/homebridge-bond)** plugin instead.

## How to programme my remote functions onto Bond Bridge RF Controller
To work as intended, the remote functions need to be programmed onto the Bond Bridge RF Controller as two separate "Celing Fan" devices, one for the Fan and one for the Light:
1. Add a "Ceiling Fan" device onto **Bond Bridge RF Controller** and programme The `Fan Off` function and the `Fan Speed` functions under "Fan". Name the device ending with " Fan" (e.g. Bed 4 Fan). Do not programme the `Light On/Off` functions here.  

     Note that the Fan Speed has intrinsic On function, as such the "Fan On" functino is not required, only the "Fan Off" function need to be programmed.  No harm done also if you do programme both On/Off functions.

2. Add another "Ceiling Fan" device onto **Bond Bridge RF Controller** and programme The `Light On/Off` functions under "Light" and programme the `Light Dimmer` functions under "Fan" as "Fan Speed". This LOGIC remote has 7-levels dimmer, so programme them as "Speed 1", "Speed 2", etc.  Name this device ending with " Light" (e.g. Bed 4 Light).

This plugin does not use the built-in timers but use customer-built timers within a bash script. These timers have greater flexibility and capability to turn on or off the fan and the light. 

These timers used 'Lightbulb' accessory as proxy and `time-to-on` and `time-to-off` is set in % in a scale of 6 minutes per 1%, or 10% = 1.0 hour. Setting the Fan Timer when the Fan is in Off state will be a `time-to-on` timer and vice versa.

## Installation:
### Raspbian/HOOBS/macOS/NAS:
1. If you have not already, install Homebridge via these instructions for [Raspbian](https://github.com/homebridge/homebridge/wiki/Install-Homebridge-on-Raspbian), [HOOBS](https://support.hoobs.org/docs) or [macOS](https://github.com/homebridge/homebridge/wiki/Install-Homebridge-on-macOS).
2. Install the `homebridge-cmd4` plug-in via the Homebridge UI `Plugins` tab search function. Once installed, a pop-up box with a small config in it will appear. Do not edit anything and make sure you click `SAVE`.
3. Install `homebridge-cmd4-bondbridge` plug-in via the Homebridge UI `Plugins` tab search function.
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


6. Go to the 'Plugins' tab in Homebridge UI and locate your newly installed `homebridge-cmd4-bondbridge`. Click `SETTINGS` and it should launch the **Homebridge Cmd4 BondBridge** setting dialogue page.

7. Scroll down to the 'Bond Bridge Device Settings' area and fill out the `IP Address` and `Token` of your Bond Bridge device (if you have more than one Bond Bridge devices, you can click `Add new device` to setup the others), and then click `SAVE`. It will close the UI and you will need to open it once more as per Step 6.
8. Tick/untick the `"Setup"` and `"Timer"`checkboxes depending what you would like to control in Homekit, then press the `CONFIG CREATOR` button to create your Bond Bridge config. This Bond Bridge config created is stored under `homebridge-cmd4`.  You can have a look at this config by clicking `SETTING` of `homebridge-cmd4` plugin.
9. You may click `CHECK CONFIGURATION`to check the config created satisfies all requirements. On a success it will say `Passed`; if something is incorrect, an error message will pop up telling you what it is that you have missed and need to fix.

## How You Can Help:
* Report Bugs/Errors by opening Issues/Tickets.
* Suggest Improvements and Features you would like to see!

## Special Thanks:
1. Many thanks to [Mitch Williams](https://github.com/mitch7391) who has created the wonderful [Homebridge-cmd4-AdvantageAir](https://github.com/mitch7391/homebridge-cmd4-AdvantageAir) plugin and has allowed me to participate in its development and in the process I have leant a lot on **bash** and **javascript** coding in homebridge environment.
2. And never foeget to thank my beautiful wife who has put up with my obsession of sitting in front of a computer trying to get this plugin up and running.
