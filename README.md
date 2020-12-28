# mikrotik-battery-discharge-procedure
This is a very dirty Idea to measurement a Battery Status over Time with a old Mikrotik Board via Voltage Meter.

1. You need E-Mail Configuration:
```
/tool e-mail set address=mail.exampledomain.com from=voltmonitor@exampledomain.com password=V3rIS3cur3PAASw0rd port=587 start-tls=yes user=voltmonitor@exampledomain.com
```

2. Use your favorite NTP-Server and Time Zone for Time:
```
/system ntp client set enabled=yes primary-ntp=162.159.200.123
/system clock set time-zone-name=Europe/Berlin
```

3. Give your RouterBoard an Name to see a difference in the Maillog:
```
/system identity set name=Voltmonitor-Akku1
```

4. Edit the Mailadress in:
```
voltmonitor.script line 18
voltreport.script line 26
```

5. Add a scheduler:
```
/system scheduler add interval=10m name=voltmonitor on-event=voltmonitor policy=ftp,reboot,read,write,policy,test,password,sniff,sensitive,romon start-date=dec/25/2020 start-time=00:00:00
```

Notice!: The Voltage Values from the RouterBoard are not good enough, i have a difference from - 0.7 V to a normal Multimeter. 

Original from:
https://wiki.mikrotik.com/wiki/Monitor_input_voltage_on_RB333/433AH
