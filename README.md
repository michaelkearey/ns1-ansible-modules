nsone-ansible-module
====================

This is the temporary home for the nsone-ansible modules. Once additional resources are completed and reviewed we will have these merged into the community core modules so they can be distributed with mainline ansible.

Project Overview
================

NSONE is an authoritative DNS platform providing data-driven global traffic routing and a fully featured REST API. This module unlocks some of the functionality NSONE can offer for ansible. For more information about what is possible check out [nsone.com](nsone.com) and [api docs](https://nsone.net/api/).

Completed Modules:
 - ns1_zone
 - ns1_record

Still Needed:
 - ns1_facts
 - ns1_data_source
 - ns1_data_feed
 - ns1_monitoring_job

Installation
============

The easiest way to install these modules is to copy them into your ansible library directory. You will need the nsone python client version 0.9.2 or greater. This can be installed by running: `pip install nsone`. Additional information can be found here [nsone-python](https://github.com/nsone/nsone-python)

Testing
=======

This module is tested by using ansible directly. 

	git clone git@github.com/nsone/nsone-ansible-module.git
	cd nsone-ansible-module
	ansible -i local, test.yml --extra-vars key=<your nsone api key> --extra-vars debug=yes --extra-vars test_zone=<a zone you have at nsone

The debug flag is optional. You can use any test zone to get started, the only requirement is that it's not yet defined on the NSONE platform. That is, you do not need to make the zone authoritative through your registrar for the ansible module to work correctly.

The current version of the module has been tested with ansible 1.9.2 and python 2.7.10.

Examples
========

Check out test.yml which is all working ansible code. All of the resources try to model the [api](https://nsone.net/api/) objects as closely as possible. We will be adding the standard ansible documentation to the modules themselves shortly.

Contributing
============

Contributions, ideas and criticisms are all welcome. Please keep the ansible test.yml up to date if you do wind up hacking on the project.

Notes:
=====
When creating filters on records you have to use the full syntax required by the REST API to prevent ansible from updating the resources each time. For example the filters field should look like 

	filters:
	  - filter: "up"
	    config: {}

 Not

 	filters:
 	  - filter: {}

 Even though it still creates the correct resources. It calls out to the api to update each time.
