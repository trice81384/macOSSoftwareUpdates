# macOSSoftwareUpdates
A bash script to check for updates on macOS and notify users via JAMF Helper windows.

This script is designed to be run from JAMF Pro in order to check for updates to macOS.
If no updates are found it does nothing. If updates are found that do not require a reboot they are installed silently.
If no user is logged in all available updates are installed.
If an update requires a reboot and a user is logged in the user is notified via a JAMF Helper window of the name of the update to be installed and are given
an opportunity to defer the update.
After a certain amount of deferral attempts updates are forced. Once the updates have been installed the user can chose to reboot immediately or delay the
reboot for a certain period of time. If no choice is made after a certain period of time then the computer will reboot automatically. If the machine is rebooted 
before the scheduled reboot time occurs it does nothing. 

## Requirements:
1. A policy in JAMF to call the script (we run this once a day only scoped to machines that need software updates which will require a smart group).
   This Policy should have parameter 4 set as the amount of deferral attempts, parameter 5 set as the automatic reboot time in seconds, and parameter 6 set as
   the day of the week you want the policy to run on. If none of these parameters are set they will use their defaults identified in the script.
2. A policy in JAMF to run software updates (used for updates with no restart to let JAMF handle some of the logic but this could be incorporated into the 
   script).
3. A policy to allow users to run updates from self service (or change the wording as desired)

### Some options/features include:
1.  Set how many times the user can defer the prompt.
2.  Set the amount of minutes the machine will automatically reboot if updates are applied if no reboot deferral option is selected or reboot now is not
    selected.   
    This time will also be used as the time on the on the reboot deferral prompt as well. For example if a customer chooses to give their users a 10 minute
    window  
    to make a reboot decision and they choose to defer once they deferral time has come the user will have 10 mins from that time before their machine reboots.
3.  Select the day of the week on which you want to check for updates (or leave blank for any day)
4.  Choose to delay the reboot for 30 mins, 1 hr, 2 hrs, 4, hrs, 8 hrs or 12 hrs.
5.  If a customer decides they want to change the day of the week the policy is run on the policy will stop running until the new weekday is reached.
6.  Logs show which time a customer delayed the reboot until
7.  Add wording to inform the user they can update in Self Service at any time
8.  If a machine is rebooted before the deferral time arrives user will not get prompted to reboot again.
9.  Policy knows if is needs to keep prompting the user even though weekday has advanced. That is a company selects Tuesday as the day to check for updates but
    an employee defers. The policy will keep prompting them on following days until the updates are installed.
10. Fixed a bug where users could quit the update window and not select any action (this was also negatively impacted counter values).
11. Added wording to indicate some updates may necessitate the computer to shut down as opposed to restart.

### Notes:
**All script values are stored in a plist which you must specify in the script.
**Custom branding is achieved through the self service branded icon. If self service is not branded default icons are used.
**This script will shutdown the computer upon installing certain updates to account for macs with T2 Chips.
**As the Apple is moving away from the softwareupdate binary this script might not work for all updates.

Screenshots:

![Installing Upates](../assets/1_Initial%20Notification.png)
![Installing Upates](../assets/2_InstalingUpdates.png)
![Installing Upates](../assets/3_Deferral%20Options.png)
![Installing Upates](../assets/4_Reboot%20with%20Deferral.png)
