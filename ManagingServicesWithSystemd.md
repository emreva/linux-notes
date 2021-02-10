

# Chapter 2. Servislerin systemd ile Yönetilmesine Dair Kısa Komutlar



Örnek bir systemd servis dosyası 



```
[Unit]
Description=OpenBSD Secure Shell server
After=network.target auditd.service
ConditionPathExists=!/etc/ssh/sshd_not_to_be_run

[Service]
EnvironmentFile=-/etc/default/ssh
ExecStartPre=/usr/sbin/sshd -t
ExecStart=/usr/sbin/sshd -D $SSHD_OPTS
ExecReload=/usr/sbin/sshd -t
ExecReload=/bin/kill -HUP $MAINPID
KillMode=process
Restart=on-failure
RestartPreventExitStatus=255
Type=notify
RuntimeDirectory=sshd
RuntimeDirectoryMode=0755

[Install]
WantedBy=multi-user.target
Alias=sshd.service
```



- Mevcut init sistemi hangisi ? 

```
stat /sbin/init

/sbin/init
```

```
sudo stat /proc/1/exe

/proc/1/exe -> /lib/systemd/systemd
```



- Bir SysV sisteminde init'e bağlanır:

```
sudo stat /proc/1/exe

File: /proc/1/exe -> /sbin/init
```



- /proc/1/comm dosyası, aktif init sisteminizi bildirir:

```
$ sudo cat /proc/1/comm
systemd
```

Process ID'si  (PID) 1'e eklenen komut sizin initinizdir. PID 1, başlangıçta başlatılan ve daha sonra diğer tüm işlemleri başlatan ilk işlemdir. Bunu ps komutuyla görebilirsiniz:



```
$ ps -ef
UID        PID  PPID  C STIME TTY          TIME CMD
root         1     0  0 10:06 ?        00:00:01 /sbin/init splash
root         2     0  0 10:06 ?        00:00:00 [kthreadd]
root         3     2  0 10:06 ?        00:00:00 [rcu_gp]
root         4     2  0 10:06 ?        00:00:00 [rcu_par_gp]
[...]
```

Pstree komutu, bu process liste bilgilerini bir ağaç diyagramı halinde düzenler. Bu örnek, küme ayraçları içine alınmış tüm süreçleri, alt süreçlerini, PID'leri ve iş parçacıkları gösterir:



```
$ pstree -p
systemd(1)─┬─ModemManager(925)─┬─{ModemManager}(944)
           │                   └─{ModemManager}(949)
           ├─NetworkManager(950)─┬─dhclient(1981)
           │                     ├─{NetworkManager}(989)
           │                     └─{NetworkManager}(991)
           ├─accounts-daemon(927)─┬─{accounts-daemon}(938)
           │                      └─{accounts-daemon}(948)
           ├─acpid(934)
           ├─agetty(1103)
           ├─avahi-daemon(953)───avahi-daemon(970)
[...]


```

