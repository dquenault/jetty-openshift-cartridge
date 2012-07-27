jetty-openshift-cartridge
=========================

An OpenShift cartridge that uses jetty-maven-plugin to run a webapp.

Repo layout
===========
../data - For persistent data (full path in environment var: OPENSHIFT_DATA_DIR)
.openshift/action_hooks/start - Script that gets run to start your application
.openshift/action_hooks/stop - Script that gets run to stop your application
.openshift/action_hooks/pre_build - Script that gets run every git push before the build
.openshift/action_hooks/build - Script that gets run every git push as part of the build process (on the CI system if available)
.openshift/action_hooks/deploy - Script that gets run every git push after build but before the app is restarted
.openshift/action_hooks/post_deploy - Script that gets run every git push after the app is restarted


Notes about layout
==================
Note: Every time you push, everything in your remote repo dir gets recreated
please store long term items (like an sqlite database) in ../data which will
persist between pushes of your repo.


Environment Variables
=====================

OpenShift provides several environment variables to reference for ease
of use.  The following list are some common variables but far from exhaustive:

    $_ENV['OPENSHIFT_INTERNAL_IP']  - IP Address assigned to the application
    $_ENV['OPENSHIFT_GEAR_NAME']  - Application name
    $_ENV['OPENSHIFT_GEAR_DIR']   - Application dir
    $_ENV['OPENSHIFT_DATA_DIR']  - For persistent storage (between pushes)
    $_ENV['OPENSHIFT_TMP_DIR']   - Temp storage (unmodified files deleted after 10 days)

To get a full list of environment variables, simply add a line in your
.openshift/action_hooks/build script that says "export" and push.

