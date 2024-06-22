1. Create `<SCRIPT NAME>.vbs` file and open it in editor

Alt-Tab:
```vbscript
Set WshShell = WScript.CreateObject("WScript.Shell")
WshShell.SendKeys "%{TAB}"
```
Ctrl-c:
```vbscript
Set WshShell = WScript.CreateObject("WScript.Shell")
WshShell.SendKeys "^(v)"
```
2. Right click on the script, click `New` -> `Shortcut`

### Usage for Microsoft Surface pen
You can use this shortcut in the pen menu - `Open a program` and select the shortcut