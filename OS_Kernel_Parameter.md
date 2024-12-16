# Tuning OS kernel parameters
This custom is still experimental, 
uses JP-Tokyo region-1a in region AWS, and uses the i4i.xlarge 

## Apply (root user)
```bash
cat <<EOL > /etc/sysctl.d/99-a-custom.conf
net.core.rmem_max = 268435456
net.core.wmem_max = 268435456
net.ipv4.conf.all.arp_announce = 2
net.ipv4.conf.all.arp_filter = 1
net.ipv4.conf.all.arp_ignore = 1
net.ipv4.conf.default.arp_filter = 1
net.ipv4.tcp_no_metrics_save = 1
net.ipv4.tcp_rmem = 4096 87380 134217728
net.ipv4.tcp_wmem = 4096 65536 134217728
net.core.default_qdisc=fq
net.ipv4.tcp_congestion_control=bbr
EOL

sysctl -p /etc/sysctl.d/99-a-custom.conf
```

## Rationale
The number of blocks signing in one hour.
```
0x1720..30b3: 59974
0x3c83..1a76: 53687
0x4dbf..aef4: 53503
0x946b..5b21: 42552
0xd54a..a1dc: 40974
0x4700..ea9b: 40959
0x0569..d45d: 39940
0xf4db..520f: 39773
0x8f34..a79b: 38796
0x1cb2..04f0: 38589
0x979f..be76: 38247
0xef22..d5ac: 37264 -> Existing VULTR, GCP Tokyo region showed about 15000sign performance.(not custom)
0xf100..8026: 36043
0x21c9..67ff: 35627
0x9600..bb93: 35210
0xeb10..1fdc: 34083
0x2b56..de08: 33222
0xacec..7d5c: 32926
0xafe1..347a: 31803
0xd412..b3f0: 31283
0xc685..df66: 24838
0x48e2..21a4: 24834
0x7d23..2d3a: 23181
0xc715..9956: 21277
0x2cab..d462: 20560
0x21d4..73ef: 19127
0x709f..132e: 18876
0xcaf8..95bf: 15256
0xc257..c8e8: 15021
0x1ab1..ac79: 11107
0x287d..9289: 10546
0x3821..2e98: 10532
0x2f8b..7a66: 2130
0x93f8..3193: 1658
0xf587..6784: 1525
0x9a7d..c191: 221
0xfb56..4f89: 15
0x9005..45a4: 13
0xa72b..a713: 12
```
