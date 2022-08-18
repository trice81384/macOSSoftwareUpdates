# macOSSoftwareUpdates
A bash script to check for updates on macOS and notify users via JAMF Helper windows.
### This script has undergone a major rewrite to include additional functionality and Apple Silicon functionality.
#### At this point a wiki is probably needed but the basics are: 

This script is designed to be run from JAMF Pro in order to check for updates to macOS.
If no updates are found it does nothing.
If updates are needed by a client machine and a user is logged in the user is notified via a JAMF Helper window of the name of the update to be installed and given an opportunity to defer the update.
After a X amount of deferral attempts updates are forced. Once the updates have been installed the user can chose to reboot immediately or delay the
reboot for a certain period of time. If no choice is made after a certain period of time then the computer will reboot automatically. If the machine is rebooted 
before the scheduled reboot time occurs the script does nothing. 

## Requirements:
1. A policy in JAMF to call the script (run once a day only scoped to machines that need software updates which will require a smart group).
   This Policy should have parameter 4 set as the amount of deferral attempts, parameter 5 set as the automatic reboot time in seconds, and parameter 6 set as
   the day of the week you want the policy to run on. If none of these parameters are set they will use their defaults identified in the script.
2. A policy to allow users to run updates from self service if desired. If there is no associated self service policy some dialog messages would need to be    updated.


### Some options/features include:
1.  Set how many times the user can defer the prompt.
2.  Set the amount of minutes the machine will automatically reboot if updates are applied and no reboot deferral option is selected or reboot now is not
    chosen.   
    This time will also be used as the delay period once a reboot deferral prompt appears. For example if you choose to give your users a 10 minute
    window to make a reboot decision and they choose to defer once the deferral time has come the user will have 10 mins from that time before their      machine reboots.
3.  Select the day of the week on which you want to check for updates.
4.  Select what day of the year you want to start the script.
5.  Determine an interval (in days) between when updates are last installed and when the script should run again.
6.  For larger fleets introduce a randomized initial delay so that the script does not run for all clients on the same day.
7.  If a customer decides they want to change any of the above options the script will stop running until the new settings are reached.
8.  Options 3 through 6 are optional and if none are set the script will run every day software updates are available.
9.  Choose to delay the reboot (if required) for 30 mins, 1 hr, 2 hrs, 4, hrs, 8 hrs or 12 hrs.
10. On machines running Apple Silicon the software update preference pane will be opened for users to install updates instead of them being installed
    automatically.
11. Detailed logging showing script actions.
12. If a machine is rebooted before the deferral time arrives user will not get prompted to reboot again.
13. Once a user has been notified updates are available the script will keep running until the updates are installed (either by the user or forced) regardless of the options set above.
14. Fixed a bug where users could quit the update window and not select any action (this was also negatively impacted counter values).
11. Added wording to indicate some updates may necessitate the computer to shut down as opposed to restart.

### Notes:
**All script values are stored in a plist which is determined in the script based upon the set organization name.
**Custom branding is achieved through the self service branded icon. If self service is not branded default icons are used.
**This script will shutdown the computer upon installing certain updates to account for macs with T2 Chips.
**As the Apple is moving away from the softwareupdate binary this script might not work for all updates.

Screenshots:

![Installing Upates](../assets/1_Initial%20Notification.png)
![Installing Upates](../assets/2_InstalingUpdates.png)
![Installing Upates](../assets/3_Deferral%20Options.png)
![Installing Upates](../assets/4_Reboot%20with%20Deferral.png)
