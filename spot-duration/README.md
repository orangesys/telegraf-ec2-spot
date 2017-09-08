telegraf_spot_duration.py
--------------------
**telegraf_spot_duration.py** base is **ec2-spot-labs get_spot_duration.py** 

send spot duration to influxdb use telegraf plugin exec
 
Input: 
* AWS EC2 region
* product-description
* combination of instance types and Spot bids prices for each instance type.

For example, for c3 family and bids equal to 50% of [On-demand price](https://aws.amazon.com/ec2/pricing/):

```yml
[[inputs.exec]]
  command = "sudo runuser -l ec2-user -c '/etc/telegraf/telegraf.d/exec/spot-instance/telegraf_spot_duration.py --region us-west-2 --product-description '
Linux/UNIX' --bids m4.large:0.04'"
  data_format = "influx"
  interval = "5m"
```

Notes:

* Availability Zone mapping may be different for different AWS accounts
* 168.0 means that Spot price hasn't exceeded specified bid during last week (168 hours by default) 
* Actual numbers will be different, script uses last 1-week of price history and Spot prices change continiously based on supply and demand
* Newer accounts that are VPC by default  may not see all purchase options and only see ( "Linux/UNIX", "SUSE Linux", "Windows" )

Please see **telegraf_spot_duration.py --help** for additional options.

Issues
======

Please address any issues or feedback via [issues](https://github.com/orangesys/telegraf-ec2-spot/issues).
