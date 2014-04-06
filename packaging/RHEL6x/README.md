Saltstack packaging for RHEL6 derived systems
=============================================

I found the SRPM from epel was a bit lacking when it came to dealing
with My CentOS 6.5 systems.  I am not an RPM master, but I reworked the
non-systemctl related bits (which look very complete, by the way).

The problem I was addressing was that an enabled and running minion would
just drop off the scope once it was updated.  This was especially 
disconcerting as there doesn't seem to be semantics in the pkg module(s)
to upgrade Just One package.  So, anyway, this is what I came up with.  

If the service is enabled, the service(s) will be restarted once the upgrade
is complete.  If it/they are not, they remain disabled.  The minion service
will be enabled on initial install--the salt-master and salt-syndic services
will not.

salt.spec goes in $HOME/rpmbuild/SPECS
the contents of SOURCES go in $HOME/rpmbuild/SOURCES

Some things to note:

Automatic running of the saltstack test suite is disabled in the spec file

%global include_tests 0

Set it to '1' to reneble.  

If you find yourself needing to build a new package for the same version of 
salt, increment "Release: 1%{?dist}" before building (eg: Release: 2%{?dist}).


