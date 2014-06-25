XWiki Quickstart on OpenShift (with H2 DB)
============================

This git repository helps you get up and running quickly w/ an XWiki (http://www.xwiki.org/) installation on JBoss EAP 6.X using OpenShift

Running XWiki on OpenShift.
----------------------------

Create an account at http://openshift.redhat.com/ , don't forget to create a namespace and install Git, Ruby and the client tools.

Install the client tools on your machine if you have not already done so.

     sudo gem install rhc

After the OpenShift client tools are installed, run:

    rhc setup

The OpenShift interactive setup wizard displays and prompts you to complete the rest of the process. If you cannot run the OpenShift client tools at this point, please contact us on IRC or post in our forums for more assistance.

Now, create the application.

    rhc app create -a xwiki jbosseap-6 -g large --from-code git://github.com/rkmallik/xwiki-example-H2

XWiki requires a little more than just the 1GB of disk storage. Unfortunately, the rhc app create command does not yet allow for you to create an app with additional storage out of the gate, so we have to do that manually. Vote for that feature here: https://www.openshift.com/content/create-a-gear-with-extra-storage

Add an extra gigabyte of storage:
    
    rhc cartridge storage jbosseap-6 -a xwiki --add 1gb

Then, restart the app:

    rhc app restart xwiki

And that's it, you can now checkout your XWiki install at:

    https://xwiki-$yournamespace.rhcloud.com/

