# Add Observable to XDR Feeds

The script shared here adds an observable into it's XDR Feed.

XDR Feeds are blocking lists into which XDR can store objects to be blocked ( or allowed ) into company firewalls or into any enforcement solutions.

The principle is to use Cisco XDR to expose these lists thru public URLs, and configure any enforcement point that must block objects in these list to consume these URLs.

Then updating Firewall Security rules become very simple, we just have to add or delete objets into these list in order to have them blocked or not into firewalls.

The script in this repo gives you a ready to use python example that add a new object into one of these feeds.

The feeds we are talking about are the feeds created thanks to the **0015A-SecureFirewall-BlockObservable-Setup** Cisco Workflow.

If you have not studied these XDR/SecureX feeds yet, then have a look to this article :

[Create Text Public Feeds for firewalls](https://github.com/pcardotatgit/SecureX_Workflows_and_Stuffs/tree/master/12-create_securex_blocking_lists_for_firewalls)

Having these Feeds created into your XDR tenant is a mandatory pre requisit.

## Installation

You must have an up and running python 3.x environment and you must have the **crayons** and **requests** modules installed. We assume that you kniow how to setup that.

### Edit the config.txt file

You must first edit the **config.txt** file and assigned correct values to the following variables

- ctr_client_id=example_of_client_id
- ctr_client_password=example_of_client_password
- host=https://private.intel.eu.amp.cisco.com
- host_for_token=https://visibility.eu.amp.cisco.com

Don't use quotes for the value you assign to the variables. and don't use spaces between = sign and the value.

**ctr_client_id** and **ctr_client_password** are the values you got when you created your XDR API client.

Possible values for **host** depending on your region, are :

- https://private.intel.eu.amp.cisco.com
- https://private.intel.apjc.amp.cisco.com
- https://private.intel.amp.cisco.com

Possible values for **host_for_token** depending on your region, are :

### Run the script

You just have to run the script :

    python 1-add_observable_to_XDR_feeds.py
    
You will be asked to enter the observable value.  It can be either an IPv4 address, an IPv6 address, an URL, a domain or a SHA256.

Enter the value and type enter. You will see all the process that add the object to the XDR Feed.

The script check the observable type, then map it to the matching indicator depending on the object type. Indicators are linked to the XDR feeds. Then it creates a new judgement for the object and finally create a new relationship that link the observable into judgment to the matching Indicator. Once done the observabl appears into the XDR feed.

