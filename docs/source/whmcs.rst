.. _whmcs-label:

WHMCS Integrations
========================

Liquid ResellerCamp WHMCS Registrar Module Installations
---------------------------------------------------------

1. Get the API key
	a. Login to the ResellerCamp’s reseller control panel (the url will be in the email you received when you signed up) and then go to Settings -> API.
	b. Please note your reseller ID at the bottom of the page.
	c. Click Add API Key button, enter the label and the IP address of the server where WHMCS is installed to authorize it for API access.
	d. On the same page, note down the API Key.
2. Copy the whmcs module files
	a. Download `ResellerCamp’s WHMCS Registrar Module here <https://s3-ap-southeast-1.amazonaws.com/liqu.id/resellercamp-whmcs-module.zip>`_. 
	b. Extract the zip files to /YourLocalPath/whmcs/modules/registrars
	c. Remember to replace “/YourLocalPath” with the actual location where you installed WHMCS.
3. Setup WHMCS Configuration
	a. Now, login to your WHMCS Administration Area
	b. Go to Setup > Products/Services > Domain Registrars
	c. Choose "Liquid" in the registrar dropdown menu and enter both the Reseller ID and API Key noted above.
	d. Then click Save Changes

.. image:: resellercamp-whmcs.jpg

And that's it, WHMCS will now be able to communicate with your ResellerCamp account to automate domain registration & management for your customers.

Demo Mode
----------
To use the ResellerCamp demo mode or test mode, it's not as simple as ticking the demo mode option in the configuration area. You must setup an account separately on the dedicated resellercamp’s demo system. Read the :ref:`demoaccount-label` documentation.

Next enter your demo account details under Setup > Domain Registrars > ResellerCamp. With the Test Mode checkbox ticked you can now place domain registration orders in WHMCS, the domains will appear on your demo ResellerCamp account but no domain will actually be registered and you will not be charged.

.. note::
	Live nameservers created at the Registry will return a Nameserver is not a valid Nameserver error unless they are created/registered in the demo environment.


	The demo control panel will try to check the validity of the nameservers in the demo platform and not on the Registry, so you must register the nameservers first before attempting any domain registrations on the demo platform.


Feedback
---------

If you find any issues with Resellercamp's WHMCS registrar module, please use our `ticketing support systems <https://liqudotid.freshdesk.com/support/tickets/new>`_ where we’ll be available and actively listening to all of your feedback.
