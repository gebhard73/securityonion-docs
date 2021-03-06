so-import-pcap
==============

If you just want to analyze one or more pcap files, then ``so-import-pcap`` is the quickest and easiest way to get started with Security Onion!  It will import one or more pcaps into Security Onion and preserve original timestamps.

It will do the following:

-  automatically run Setup to configure the system if necessary
-  stop and disable Curator to avoid closing old indices
-  stop and disable all active sniffing processes (Zeek, Snort, Suricata, and netsniff-ng)
-  stop and disable ossec_agent
-  reconfigure and restart sguild, syslog-ng, and Logstash where necessary
-  generate IDS alerts using Snort or Suricata
-  generate Zeek logs
-  store IDS alerts and Zeek logs with original timestamps
-  split traffic into separate daily pcaps and store them where sguil's pcap_agent can find them

Minimum Requirements
--------------------

-  50GB storage
-  4GB RAM
-  2 CPU cores

Please note these are MINIMUM requirements.  If you can allocate more resources, please do so.

.. warning::

   Do NOT run so-import-pcap on an existing production deployment!
   
   It is designed for standalone systems designated for so-import-pcap.
   
Installation
------------

If you haven't already installed the latest Security Onion ISO image, here are the steps to do so:

#. `Download and verify our Security Onion ISO image <https://github.com/Security-Onion-Solutions/security-onion/blob/master/Verify_ISO.md>`__.
#. Boot the ISO image and choose the default boot menu option.
#. Once the live desktop appears, double-click the ``Install SecurityOnion`` icon.
#. Follow the prompts in the installer. If prompted with an ``encrypt home folder`` or ``encrypt partition`` option, **DO NOT** enable this feature. If asked about automatic updates, **DO NOT** enable automatic updates.
#. Once the installer completes, reboot into your new installation and login using the username and password you specified during installation.
#. NOTE! It is NOT necessary to run Setup as so-import-pcap will do this automatically.

.. tip::

   If you're running so-import-pcap in a VM with snapshot capability, you might want to take a snapshot before this program makes changes.
   
Usage
-----

Please supply the full path to at least one pcap file.

For example, to import a single pcap named ``import.pcap``:

::

    sudo so-import-pcap /full/path/to/import.pcap

To import multiple pcaps:

::

    sudo so-import-pcap /full/path/to/import1.pcap /full/path/to/import2.pcap

Example
-------

For a detailed walk-through with screenshots, please see https://blog.securityonion.net/2019/06/analyze-pcaps-in-3-simple-steps-using.html.

Warning
-------

Please note that so-import-pcap will make changes to your system! It will warn you before doing so and will prompt you to press Enter to continue or Ctrl-c to cancel.

If you want to bypass the "Press Enter to continue" prompt, you can do something like this:

::

    echo | sudo so-import-pcap /opt/samples/markofu/ie*
