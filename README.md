



Bu, sizin adınıza port taraması yapabilen web sitelerini kullanan bir Python komut satırı aracı ve kütüphanesidir.

## Desteklenen Online Port Tarama Araçları

* [ipfingerprints](http://www.ipfingerprints.com/portscan.php)
* [spiderip](https://spiderip.com/online-port-scan.php)
* [standingtech](https://portscanner.standingtech.com/)
* [viewdns](http://viewdns.info/)
* [yougetsignal](http://www.yougetsignal.com/tools/open-ports/)

## Kurulum

Pip ile kurulum:  pip install scanless --user

## CLI Kullanımı

$ scanless --help
kullanım: scanless [-h] [-v] [-t HEDEF] [-s TARAYICI] [-r] [-l] [-a] [-d]

scanless, bir online port tarama scraper'ı.

seçenekler:
-h, --help bu yardım mesajını gösterir
-v, --version mevcut sürümü gösterir
-t HEDEF, --target HEDEF
tarama yapılacak IP veya domain
-s TARAYICI, --scanner TARAYICI
kullanılacak tarama aracı (varsayılan: yougetsignal)
-r, --random rastgele bir tarama aracı kullan
-l, --list tarama araçlarını listele
-a, --all tüm tarama araçlarını kullan
-d, --debug hata ayıklama modu (CLI modunu kapatır & ağ hatalarını gösterir)

$ scanless --list
+----------------+--------------------------------------+
| Tarama Aracı | Websitesi |
+----------------+--------------------------------------+
| ipfingerprints | https://www.ipfingerprints.com |
| spiderip | https://spiderip.com |
| standingtech | https://portscanner.standingtech.com |
| viewdns | https://viewdns.info |
| yougetsignal | https://www.yougetsignal.com |
+----------------+--------------------------------------+

$ scanless -t scanme.nmap.org -s spiderip
scanless v2.2.1 çalışıyor ...

spiderip:
PORT DURUM SERVİS
21/tcp kapalı ftp
22/tcp açık ssh
25/tcp kapalı smtp
80/tcp açık http
110/tcp kapalı pop3
143/tcp kapalı imap
443/tcp kapalı https
465/tcp kapalı smtps
993/tcp kapalı imaps
995/tcp kapalı pop3s
1433/tcp kapalı ms-sql-s
3306/tcp kapalı mysql
3389/tcp kapalı ms-wbt-server
5900/tcp kapalı vnc
8080/tcp kapalı http-proxy
8443/tcp kapalı https-alt

bash


## Kütüphane Kullanımı

```python
>>> import scanless
>>> sl = scanless.Scanless()
>>> cikti = sl.scan('scanme.nmap.org', scanner='yougetsignal')
>>> print(cikti['raw'])
PORT      DURUM   SERVİS
21/tcp    kapalı  ftp
22/tcp    açık    ssh
23/tcp    kapalı  telnet
25/tcp    kapalı  smtp
53/tcp    kapalı  domain
80/tcp    açık    http
110/tcp   kapalı  pop3
115/tcp   kapalı  sftp
135/tcp   kapalı  msrpc
139/tcp   kapalı  netbios-ssn
143/tcp   kapalı  imap
194/tcp   kapalı  irc
443/tcp   kapalı  https
445/tcp   kapalı  microsoft-ds
1433/tcp  kapalı  ms-sql-s
3306/tcp  kapalı  mysql
3389/tcp  kapalı  ms-wbt-server
5632/tcp  kapalı  pcanywherestat
5900/tcp  kapalı  vnc
6112/tcp  kapalı  dtspc
>>> import json
>>> print(json.dumps(cikti['parsed'], indent=2))
[
  {
    "port": "21",
    "state": "kapalı",
    "service": "ftp",
    "protocol": "tcp"
  },
  {
    "port": "22",
    "state": "açık",
    "service": "ssh",
    "protocol": "tcp"
  },
  {
    "port": "23",
    "state": "kapalı",
    "service": "telnet",
    "protocol": "tcp"
  },
  {
    "port": "25",
    "state": "kapalı",
    "service": "smtp",
    "protocol": "tcp"
  },
  {
    "port": "53",
    "state": "kapalı",
    "service": "domain",
    "protocol": "tcp"
  },
  {
    "port": "80",
    "state": "açık",
    "service": "http",
    "protocol": "tcp"
  },
  ...
]
