# So how to play?

First, do you want your username to be displayed if you beat the world record? If yes, stay here, if not continue to the next-next paragraph.
To register you need to choose a username, when you have selected one go to the next Url and replace the [username] with your username : flappybird.eu.pythonanywhere.com/register/[username] .
Great so now you registered your account. And the site gave you a command.

> [!NOTE]
If you have MacOS, I am sorry, bc I am not gonna spend my time trying to make it work on apple devices and 
then not being able to test it because simulating MacOS in a virtual machine is illegal, if you have linux, you'll have to wait for some time as i didn't make the code for linux yet + the game uses powershell escape characters,
which probably work differently on linux.

Now open powershell on your Windows machine and enter the command the website gave you, if you didn't register just enter this next command: 

```powershell
cls; $id = "notregistered";$global:response = ""; $timer = New-Object System.Timers.Timer 100; $timer.AutoReset = $true; Register-ObjectEvent -InputObject $timer -EventName Elapsed -Action { try { $global:response = Invoke-RestMethod "http://flappybird.eu.pythonanywhere.com/$($id)" } catch { $global:response = "ERROR: $($_.Exception.Message)" } } -SourceIdentifier PollEvent; $timer.Start(); while ($true) { [Console]::SetCursorPosition(0, 0); [Console]::SetCursorPosition(0, 0); Write-Host $global:response; if ([Console]::KeyAvailable) { $key = [Console]::ReadKey($true).Key; Invoke-RestMethod "http://flappybird.eu.pythonanywhere.com/jumped/$id" | Out-Null; if ($key -eq 'Q') { break } } }; $timer.Stop(); Unregister-Event -SourceIdentifier PollEvent; $timer.Dispose(); Write-Host "`nExited. Timer stopped and resources cleaned up"
```
Now Enjoy the game you can press any key to jump and 'q' to quit

I guess this is all, **if somebody wants to contribute to make the linux terminal work I would be very thankful.**

I think the source code contains enough comments so I don't have to talk about how it works here.

test linux command, not sure if works
```bash
clear; id="notregistered"; stty -echo -icanon time 0 min 0; trap "stty sane; echo -e '\nExited. Timer stopped and resources cleaned up'; exit" SIGINT SIGTERM; while true; do response=$(curl -s "http://flappybird.eu.pythonanywhere.com/$id"); [ $? -ne 0 ] && response="ERROR: Failed to connect"; tput cup 0 0; echo -e "$response"; read -rsn1 -t 0.1 key; if [[ $key == "q" || $key == "Q" ]]; then stty sane; echo -e '\nExited. Timer stopped and resources cleaned up'; exit; elif [[ -n $key ]]; then curl -s "http://flappybird.eu.pythonanywhere.com/jumped/$id" > /dev/null; fi; done
```
