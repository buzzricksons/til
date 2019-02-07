# TODO List
* Change date and time format.
* 

# Install app
* AutoHotkey
	* https://www.autohotkey.com/
* clibor
	* https://www.vector.co.jp/soft/winnt/util/se472890.html
* Sublime Text
* Visualstudio code


# AutoHotkey
### language
https://autohotkey.com/docs/misc/Languages.htm

### input same key twice
```shell
; In this case, F1 is key of twice input.

F1::
If (A_PriorHotKey = "F1 Up" AND A_TimeSincePriorHotkey < 500)
{
	Send, +{End}
	KeyWait, F1
}
return

F1 Up::
Send, {F1 Up}
Send ^c
return
```



