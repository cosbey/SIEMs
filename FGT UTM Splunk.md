
# FGT UTM Splunk


**Identify by dst_ip, port and if the action was blocked**
```
index="botsv1" earliest=0 sourcetype=fgt_utm "date=2016-08-10"  dest_port=80  dstip="192.168.250.70"  action=blocked | table  date, time, dstip, srcip, dstport, action, msg, catdesc
```

**Identify by Action**
```
index="botsv1" earliest=0 sourcetype=fgt_utm action=blocked "date=2016-08-10" 
| stats count by srcip
```

**Identify by Attack**
```
index="botsv1" earliest=0 sourcetype=fgt_utm attack="*" "date=2016-08-10" 
| stats count by srcip
```

