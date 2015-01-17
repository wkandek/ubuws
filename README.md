Setup UbuWS as Scan Target

- Ubuntu 12.04 LTS no updates
- only openssh server
- user: user1/password1 has sudo
- user: qscanner/qscanner for scanning - no sudo
- firewall via iptables
  - in /etc/network/interfaces after the last eth0 line:
    pre-up iptables-restore < /etc/iptables-rules
  - iptables-rules
  :INPUT ACCEPT [0:0]
  :FORWARD ACCEPT [0:0]
  :OUTPUT ACCEPT [10778:3311031]
  -A INPUT -s 10.0.0.0/8 -j ACCEPT
  -A INPUT -s 192.168.0.0/16 -j ACCEPT
  -A INPUT -s 64.39.96.0/20 -j ACCEPT
  -A INPUT -j DROP
  COMMIT

- for Bodge IT app under Tomcat
  - tomcat7
  - install BodgeIT code (bodgeit.war) to /var/lib/tomcat7/webapps
  - get from github wkandek bodgeit

- for HB webapp: mysql-server php5-mysql libapache2-mod-php5 unzip
  - logrotation to weekly 7 in /etc/logrotate.d/apache2

