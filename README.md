# README #

### OpenVPN with local user account auth ###

* Version 15.07.16

### How do I get set up? ###

* Server side

* First step - update system:
  `apt-get update && apt-get upgrade`

* After install OpenVPN:
  `apt-get install openvpn`

* Then
  `cd /usr/share/doc/openvpn/examples/easy-rsa/2.0/`
  `nano ./vars`

* Initialize enviroment 
  `. ./vars`
  `. ./clean-all`

* Build Certificate
  `./build-ca # ROOT certificate`
  `./build-key-server server # server certificate`
  `./build-dh # Diffie-Hellman key`

* If you want use tls-auth, to protect hide port/service, protect from DDoS and some more
  `openvpn --genkey --secret ./keys/ta.key`

* After enable tls-auth don't forget give tls key to clients

* Copy certificates to work directory
  `cp ./keys/ca.crt /etc/openvpn`
  `cp ./keys/server.crt /etc/openvpn`
  `cp ./keys/server.key /etc/openvpn`
  `cp ./keys/dh1024.pem /etc/openvpn`

* For tls-auth copy tls key
  `cp ./keys/ta.key /etc/openvpn`

* Server config 
  `nano /etc/openvpn/server.conf`

* Edit 
  `nano /etc/rc.local`
 for create permanent firewall rules

* Edit
  `nano /etc/sysctl.conf`
 for enable ip forwarding
 
 * Edit 
  `nano /etc/openvpn/update-resolv-conf`

* Reboot server to prove all works

* Client side settings:

* Copy certificate `ca.crt` and `ta.key` to client device.

* Use OpenVPN client for Linux or Windows with myvpnconfig.ovpn config file.

* For start without GUI use start script start_vpn.run

* Authentificate with local user accounts.

### А кому можно доверять в этом мире? ###

Инь Фу Во два дня настраивал VPN-туннель для своего персонального компьютера. Когда туннель заработал, Инь уселся, почтительно повернувшись лицом к югу, и стал читать свою френдленту.

– О, Учитель, – спросил его Сисадмин, – я не могу понять, зачем вам VPN?

– Ты разве не знаешь, что в VPN-туннеле весь трафик шифруется? – удивился Инь.

– Знаю. Но ваш туннель терминируется на обычном сервере в стране западных варваров. А далее весь ваш яшмовый трафик идёт по Сети в открытом виде.

– Сети нет дела до моего трафика, чего не скажешь о провайдере, – ответил Учитель. Видя, что Сисадмин не понял, он добавил. – Вот, например, ты доверил свои деньги банку.

Сисадмин кивнул.

– Но ты не можешь доверить все свои деньги собственной супруге, – продолжал мудрый Инь. – Почему? Потому что она может посчитать эти деньги своими. А с банком такого не случится.

Просветлённый Сисадмин ушёл поднимать себе VPN-туннель.

### Who do I talk to? ###

* Repo owner CyberManiac
