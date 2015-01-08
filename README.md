Setup COS64 as Scan Target
- download DVD toget older code
- install mysql cleint mysql server web server, php servlet 
- download from mirror with updates php-mysql for mysqli library
  http://mirror.nsc.liu.se/centos-store/6.4/updates/i386/Packages/php-mysql-5.3.3-23.el6_4.i686.rpm
  install with RPM -Uvh --nodpes --force
- create user qscanner/qscanner, usermod -G wheel qscanner, visudo uncomment wheel
- copy hb to /var/www/hb change /etc/httpd/conf.d/ssl.conf uncomment DocRoot and point to hb
- copy shellshock to /var/www/html and add README.md at end of httpd.conf
- mysqladmin -u root password heartbleed
- mysql -u root mysql - create database hb;
- /etc/sysconfig/network-scripts onboot = on for eth0
- /etc/sysconfig/iptables delete all rules 


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

