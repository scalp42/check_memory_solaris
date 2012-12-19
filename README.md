check_memory_solaris
====================

### Why :
--------
After looking around, I didn't find any script satisfying my needs so here is another Nagios memory check for Solaris (SmartOS/Joyent compatible).

### Requirements :
--------

* Bash
* `jinf` or `sm-meminfo` on the system.

### Usage :
--------


**Set up your `nrpe.cfg` with the check :**

	command[check_memory_solaris]=/usr/local/nagios/libexec/check_memory_solaris -w $ARG1$ -c $ARG2$

**Set up `services.cfg` in your Nagios conf (just an example) :**

	define service{
        use                          generic-service
        hostgroup_name               Prod,!Postgres,!Riak,!Redis
        service_description          check_memory_solaris
        check_command                check_nrpe!check_memory_solaris\!90\!95
        event_handler                restart-unicorn!$SERVICESTATE$!$SERVICESTATETYPE$!$SERVICEATTEMPT$
        servicegroups                health
        notifications_enabled        1
        retain_status_information    1
        retry_check_interval         5
	}
	

**To test the script (no elevated privileges required):**

	$> ./check_memory_solaris -w 90 -c 95

### Contributing :
--------

Bug reports and pull requests welcome!

### Questions or suggestions :
--------

Create an issue: [https://github.com/scalp42/check_memory_solaris/issues](https://github.com/scalp42/check_memory_solaris/issues)