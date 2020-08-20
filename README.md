# macOSSoftwareUpdates
A bash script to check for updates on macOS and notify users via JAMF Helper windows.

**This script relies on a machine being properly enrolled in jamf as well as some jamf policies created to run on custom triggers (this can be modified to suit your needs).**


Some options/features include:
1.  Set how many times the user can defer the prompt.
2.  Set the amount of minutes the machine will automatically reboot if updates are applied if no reboot deferral option is selected or reboot now is not selected.   
    This time will also be used as the time on the on the reboot deferral prompt as well. For example if a customer chooses to give their users a 10 minute window  
    to make a reboot decision and they choose to defer once they deferral time has come the user will have 10 mins from that time before their machine reboots.
3.  Select the day of the week on which you want to check for updates (or leave blank for any day)
4.  Choose to delay the reboot for 30 mins, 1 hr, 2 hrs, 4, hrs, 8 hrs or 12 hrs.
5.  If a customer decides they want to change the day of the week the policy is run on the policy will stop running until the new weekday is reached.
6.  Logs show which time a customer delayed the reboot until
7.  Add wording to inform the user they can update in Self Service at any time
8.  If a machine is rebooted before the deferral time arrives user will not get prompted to reboot again.
9.  Policy knows if is needs to keep prompting the user even though weekday has advanced. That is a company selects Tuesday as the day to check for updates but an 
    employee defers. The policy will keep prompting them on following days until the updates are installed.
10. Fixed a bug where users could quit the update window and not select any action (this was also negatively impacted counter values).
11. Added wording to indicate some updates may necessitate the computer to shut down as opposed to restart.

Screenshots:

![InitialNotificastion](../assets/1_Initial Notification.png?raw=true)

