https://github.com/user-attachments/assets/87fa5b01-9f5e-4265-924e-feeaa257fa11



# So how to play?

First, do you want your username to be displayed if you beat the world record? If yes, stay here, if not continue to the next-next paragraph.
To register you need to choose a username, when you have selected one go to the next Url and replace the [username] with your username : flappybird.eu.pythonanywhere.com/register/[username] . It is also possible to use any network request command, just enter the url there.
Great so now you registered your account. And the site should answer with a powershell and a bash command

> [!NOTE]
> If you have MacOS, I am sorry, because I am not gonna spend my time trying to make it work on apple devices and 
then not being able to test it because simulating MacOS in a virtual machine is illegal. If you have knowledge on apple devices and want to contribute to this project
and make it work even on Mac, I am open to it.


Now open powershell or terminal on your machine and enter the command the website gave you depending on your os, if you didn't register just enter this next command: 


Windows:
```powershell
cls; $id = "notregistered";$global:response = ""; $timer = New-Object System.Timers.Timer 100; $timer.AutoReset = $true; Register-ObjectEvent -InputObject $timer -EventName Elapsed -Action { try { $global:response = Invoke-RestMethod "http://flappybird.eu.pythonanywhere.com/$($id)" } catch { $global:response = "ERROR: $($_.Exception.Message)" } } -SourceIdentifier PollEvent; $timer.Start(); while ($true) { [Console]::SetCursorPosition(0, 0); [Console]::SetCursorPosition(0, 0); Write-Host $global:response; if ([Console]::KeyAvailable) { $key = [Console]::ReadKey($true).Key; Invoke-RestMethod "http://flappybird.eu.pythonanywhere.com/jumped/$id" | Out-Null; if ($key -eq 'Q') { break } } }; $timer.Stop(); Unregister-Event -SourceIdentifier PollEvent; $timer.Dispose(); Write-Host "`nExited. Timer stopped and resources cleaned up"
```

Linux:
```bash
clear; stty -echo -icanon time 0 min 0; trap "stty sane; echo -e '\nExited.'; exit" SIGINT; id="notregistered"; while true; do tput cup 0 0; read -rsn1 -t 0.05 key; if [ $? -eq 0 ]; then [[ $key == "q" || $key == "Q" ]] && break || curl -s http://flappybird.eu.pythonanywhere.com/jumped/$id; else curl -s http://flappybird.eu.pythonanywhere.com/$id; fi; done; stty sane; echo -e "\nExited."
```
https://github.com/user-attachments/assets/ca4f5f84-f401-43d1-8ed0-976fee1234f0

Now Enjoy the game you can press any key to jump and 'q' to quit

# System Requirements:

OS: Linux / Windows 10,
> [!NOTE]
> (only tested on Ubuntu, but all other popular distros should work as well)

Processor: Works on Intel Core i3-5010U and higher, lower cpus weren't tested

Network Connection: required


# Self Hosting and possible problems with my current hosting
> [!NOTE]
Now it is very possible that it won't work, because I am currently making use of PythonAnywhere hosting which requires me to click a button once in three months
to make the site run for the next 3 months, so i will put a quick guide on how to host your own server here:

1) Download this repo on your computer
2) Setup a python flask project through something like VSCode (tutorial: https://code.visualstudio.com/docs/python/tutorial-flask)
3) Load the folder you downloaded there
4) Change the ips in the powershell.txt and bash.txt files from flappybird.eu.pythonanywhere.com/ to 127.0.0.1:5000/
> [!IMPORTANT]
> there are links like flappybird.eu.pythonanywhere.com/jumped/$id so accordingly you would change that to be 127.0.0.1:5000/jumped/$id
5) After that, start the project. And connect the same way you would usually but replace the ips when registering
