# pritunl
pritunl Install

#Configure source
cat >>/etc/yum.repos.d/mongodb.repo<<'OPO'
[mongodb-org-3.6]
name=MongoDB Repository
baseurl=https://repo.mongodb.org/yum/redhat/7/mongodb-org/3.6/x86_64/
gpgcheck=1
enabled=1
gpgkey=https://www.mongodb.org/static/pgp/server-3.6.asc
OPO

cat >>/etc/yum.repos.d/pritunl.repo<<'OPO'
[pritunl]
name=Pritunl Repository
baseurl=https://repo.pritunl.com/stable/yum/centos/7/
gpgcheck=1
enabled=1
OPO

yum makecache

yum -y install pritunl mongodb-org

gpg --keyserver hkp://keyserver.ubuntu.com --recv-keys 7568D9BB55FF9E5287D586017AE645C0CF8E292A
gpg --armor --export 7568D9BB55FF9E5287D586017AE645C0CF8E292A > key.tmp; sudo rpm --import key.tmp; rm -f key.tmp


systemctl start mongod pritunl
systemctl enable mongod pritunl


#Generate initial setup key
pritunl setup-key

#Get initial user name password get command

#https://docs.pritunl.com/docs


