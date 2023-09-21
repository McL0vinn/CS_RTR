# CS_RTR


Identifying rogue scheduled tasks and removing them via CrowdStrike RTR
First identify the schedule tasks you want to remove by using the get-scheduledtasks command 
You can either pipe and findstr or you can even use the argument -TaskName "" if you know the full taskname
Here it throws an error because it requires and interactive yes/no. You can pass the -Confirm:$False to force the removal without an interactive approval

C:\> runscript -Raw=```get-scheduledtask | findstr "OneStart"
```
\                                              OneStart Chromium                 Ready     
\                                              OneStart Updater                  Ready
C:\> runscript -Raw=```Unregister-ScheduledTask -TaskName "OneStart Chromium" ```
Exception calling "EndProcessing" with "0" argument(s): "A command that prompts the user failed because the host program or the command type does not support user interaction. The host was attempting to request confirmation with the following message: Are you sure you want to perform this action?
Performing operation 'Delete' on Target '\OneStart Chromium'."

C:\> runscript -Raw=```Unregister-ScheduledTask -TaskName "OneStart Chromium" -Confirm:$false```
C:\> runscript -Raw=```Unregister-ScheduledTask -TaskName "OneStart Updater" -Confirm:$false```
C:\>
