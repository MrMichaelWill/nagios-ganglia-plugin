Introduction
------------

`check_ganglia_metrics` is a [Nagios](http://nagios.com/) plugin that checks values for specified
metrics from [Ganglia](http://ganglia.sourceforge.net/) and raises erros if need.

This tool is forked from Daniyalzade's project https://github.com/daysleeper/nagios-ganglia-plugin and improvements are likely pushed back to it later. 
The original was inspired by @vvuksan's blog post (http://bit.ly/qVu8Z)


Usage
-----

    > python ganglia_metric_checker.py [-G gmetadhost] [-P gmetadport] -H <hostnametocheckfor> -M <metric> {-C <critical value> | -W <warning value>}


Dependencies
------------

* [python 2.5+](http://python.org/)


Issues
------
Please report issues via [github issues](https://github.com/MrMichaelWill/nagios-ganglia-plugin/issues) 


To Do
-----

* suggestions?
