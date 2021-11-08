snip.uchacz.it
==============

It is source code of snip.uchacz.it. You can generate same version of this on your site.  


Install & Build & Run (Apache2)
=========================

```
apt-get install git python3-pip apache2
git clone git@github.com:leszekuchacz/snip.uchacz.it.git
cd snip.uchacz.it/
pip3 install -r requirements.txt
pwd=`pwd`; echo -e  "<VirtualHost *:80>\n DocumentRoot $pwd/target\n  <Directory $pwd/target>\nOptions Indexes FollowSymLinks\nAllowOverride None\n</Directory>\n</VirtualHost>" > /etc/apache2/sites-available/snip.cof
a2dissite 000-default.conf
a2enmod snip.conf
service apache2 restart
sphinx-build -b html source/ target/
```

Build & Run (Docker)
=========================
TODO: Prepeare dockerfile based on https://hub.docker.com/r/sphinxdoc/sphinx
