###### 1.Log into the Windows VM using the GUI with the “user” account.
###### 2.Double click on the “AdminPaint” shortcut on the Desktop.
###### 3.Open a command prompt and run:
`> tasklist /V | findstr mspaint.exe`
_Note that mspaint.exe is running with admin privileges.
104Privilege Escalation_
###### 4. In Paint, click File, then Open.
###### 5. In the navigation input, replace the contents with:
`file://c:/windows/system32/cmd.exe`
###### 6. Press Enter. A command prompt should open running with admin privileges.