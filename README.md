xivo-dbms
=========

xivo-dbms is a Debian package that is responsible to install and upgrade the
database management system (postgresql) used by Wazo.

Depend with postgresql
======================

Problem:

  * a newer version of postgresql is available on the Debian mirrors
  * a newer version of Wazo daemon with database is available on the Wazo mirror
  * someone run wazo-upgrade

  What can happens then is that during the wazo-upgrade:

  * postgresql is unpacked (and the cluster is then stopped)
  * wazo daemon is unpackaged then configured, but it doesn't try to
    update it's database schema since the postgresql cluster is not
    running at this stage
  * postgresql is configured

  So you find yourself at the end of the wazo-upgrade with an not-updated
  database schema, and this is not good.


Solution:

  * The postgresql package is cloned from debian mirror to wazo mirror
  * xivo-config provide a pinning configuration on postgresql to take postgresql from wazo mirror
  * Postgresql version is fixed in xivo-dbms to control the order of packages installation.
