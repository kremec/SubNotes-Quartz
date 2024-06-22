1. Open `Task scheduler`
2. Select `Task Scheduler Library` (left pane)
3. Click `Create task` in right `Actions pane`
4. In `General` tab:
	1. Set the task `Name`
	2. Check the `Run with highest privileges` tickbox
	3. Select `Windows 10` in `Configure for:` dropdown menu
5. In `Actions` tab:
	1. Click `New` button
	2. Type `cmd.exe` in the `Program/script:` field
	3. Type `/c start "<TASK NAME>" "<FULL PATH OF APPLICATION FILE>"`
	4. Click `OK`
6. In `Conditions` tab:
	1. Uncheck `Start the task only if the computer is on AC power` tickbox
7. Click on `OK`

You should see the new elevated task listed in `Task Scheduler Library`

8. On desktop, right click, click `New` -> `Shortcut`
9. Type `schtasks /run /tn "<TASK NAME>"` into the location field
10. Type `<SHORTCUT NAME>` into the name field

Then you can change the icon of shortcut in the `Properties` pagew