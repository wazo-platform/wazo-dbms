# wazo-dbms

wazo-dbms is a Debian package that is responsible for installing and upgrading the
database system (PostgreSQL) used by Wazo.

# Depending on PostgreSQL

Problem:

  - a newer version of PostgreSQL is available on the Debian mirrors
  - a newer version of Wazo daemon which uses the database is available on the Wazo mirror
  - someone runs wazo-upgrade

  What can happen then is that during the wazo-upgrade:

  - PostgreSQL is unpacked (and the cluster is then stopped)
  - wazo daemon is unpacked and configured, but it doesn't try to
    update its database schema since the PostgreSQL cluster is not
    running at this stage
  - PostgreSQL is configured

  So you find yourself at the end of the wazo-upgrade with a non-upgraded
  database schema, and this is not good.


Solution:

  - The PostgreSQL package is upgraded independently at the start of the wazo-upgrade process.
