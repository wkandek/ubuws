Setup COS65 as Scan Target
- download DVD to get older code
- install mysql client mysql server web server, php - also php-mysql in the options 
- create user qscanner/qscanner, usermod -G wheel qscanner, visudo uncomment wheel
- disable SELINUX in /etc/sysconfig/selinux
- copy hb to /var/www/hb change /etc/httpd/conf.d/ssl.conf uncomment DocRoot and point to hb
- copy shellshock to /var/www/html and add README.md at end of httpd.conf
- mysqladmin -u root password heartbleed
- mysql -u root mysql - create database hb;
- /etc/sysconfig/network-scripts onboot = on for eth0
- /etc/sysconfig/iptables delete all rules - add rules from README.md
- chkconfig --level 3 mysqld and also httpd
- tomcat6 installed - bodgeit.war in /var/lib/tomcat6/webapps
- demo1.key and demo1.crt installed in /etc/pki/tls/certs and private, generated on debian etch (weak RND) with 1024 bits
  /etc/ssl/conf.d/ssl.conf configured to use those certs

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
  - install BodgeIT code (bodgeit.war) to /var/.../webapps

- for HB webapp: mysql-server php5-mysql libapache2-mod-php5

