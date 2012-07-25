Introduction
------------

`check_ganglia_metrics` is a [Nagios](http://nagios.com/) plugin that checks values for specified
metrics from [Ganglia](http://ganglia.sourceforge.net/) and raises errors if need.

This tool is forked from Daniyalzade's project https://github.com/daysleeper/nagios-ganglia-plugin and improvements are likely pushed back to it later. 
The original was inspired by @vvuksan's blog post (http://bit.ly/qVu8Z)


Usage
-----

    > python ganglia_metric_checker.py [-G gmetadhost] [-P gmetadport] -H <hostnametocheckfor> -M <metric> {-C <critical value> | -W <warning value>} [ -W invert ]
    > python ganglia_metric_checker.py -F gmetad.xml -H <hostnametocheckfor> -M <metric> {-C <critical value> | -W <warning value>} [ -W invert ]

    normally it compares the metric to be below the warning/critical value. in case where you want to stay above, use -I to invert the test.



Notes
-----

in nagios, I use it like this:

define command{
        command_name    check_ganglia_metric
        command_line    $USER1$/check_ganglia_metric_pa -F /var/spool/nagios/gmetad.xml -H $HOSTNAME$ -M $ARG1$ -W $ARG2$ -C $ARG3$ $ARG4$
        # check_ganglia_metric!host!metric!min!max!inv
        # i.e. check_ganglia_metric!cawb34!disk_free_percent_rootfs!60!80!-I
        # calls check_ganglia_metric -H cawb34 -M disk_free_percent_rootfs  -W 60 -C 80   -I
}

define service{
        use                             generic-service
        hostgroup_name                  my-servers-with-centos-5
        service_description             ganglia_metric_load_one
        # warn if more than load 6, critical if more than 12
        check_command                   check_ganglia_metric!load_one!6!12
        notifications_enabled           1
}

define service{
        use                             generic-service
        hostgroup_name                  my-servers-with-centos-5
        service_description             ganglia_metric_disk_free_percent_rootfs
        # warn if less than 40% free space, critical if less than 20% disk space
        check_command                   check_ganglia_metric!disk_free_percent_rootfs!40!20!-I
        notifications_enabled           1
}


Dependencies
------------

* [python 2.5+](http://python.org/)


Issues
------
Please report issues via [github issues](https://github.com/MrMichaelWill/nagios-ganglia-plugin/issues) 


To Do
-----

* suggestions?
