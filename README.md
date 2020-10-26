# A first look at the African's ccTLDs technical environment repository

> **A first look at the African's ccTLDs technical environment**,<br>
> Alfred Arouna, Amreesh Phokeer and Ahmed Elmokashfi.<br>
> [EAI AFRICOMM – 12th EAI International Conference on e‐Infrastructure and e‐Services for Developing Countries](https://africommconference.eai-conferences.org/2020/accepted-papers/)

Leveraging multiple datasets, we evaluated the current status of African ccTLDs, technical environment with regard to best practices. 

We have evaluated 54 African ccTLDs technical environment on several aspects: ccTLD reachability, Prefixes origin (RIR) of NS, Anycast, DNSSEC (zone signing) and misconfiguration report with zonemaster tool.

As overall, African  ccTLDs are characterised by the usage of out of region resources. 


## Scripts
### python requirements
* `getdns`: to collect NS records from ccTLD namesersers instead of IANA Whois.
* `pandas`: to save result as dataframe.
* `pytricia`: to store prefixe in a trie.
* `pickle`: to dump/load external files data.

### Zonemaster requirements
We have installed  the [Zonemaster-LDNS](https://github.com/zonemaster/zonemaster-ldns/blob/master/README.md), the [Zonemaster-Engine](https://github.com/zonemaster/zonemaster-engine/blob/master/docs/Installation.md)  and the [Zonemaster-CLI](https://github.com/zonemaster/zonemaster-cli/blob/master/docs/Installation.md) following zonemaster installation documentation.  Zonemaster-Engine and Zonemaster-LDNS are dependencies of Zonemaster-CLI.

### Data collection script
We use the script [`data_collector.py`](./scripts/data_collector.py) to collect data for African ccTLDs and top 10 ccTLDs.


## Dataset
Data are available in folder `datasets`. The structure will be similar to the one below, after the script has been run. Data are daily structured. Note that Deploy320 file use for our analysis is no more available on the Internet. We have added the latest version of this file i.e. `deploy360_dnssec_last20200713.csv` to the repository and the script is using this file instead.

```
$ tree datasets/
./datasets/
└── raw
│   ├── 20201024
│   │   ├── anycast_dataset
│   │   ├── deploy360_dnssec
│   │   ├── dnssec_algo
│   │   ├── nro_delegated
│   │   ├── prefixes_asn
│   │   ├── results
│   │   │   ├── top_cctld_cctld_ns.csv
│   │   │   ├── top_cctld_cctld_zonemaster_data.csv
│   │   │   └── top_cctld_cctld_zonemaster_result.csv
│   │   └── zonemaster_result
│   │       ├── zonemaster_BR.json
│   │       ├── zonemaster_CN.json
│   │       ├── zonemaster_DE.json
│   │       ├── zonemaster_EU.json
│   │       ├── zonemaster_FR.json
│   │       ├── zonemaster_IT.json
│   │       ├── zonemaster_NL.json
│   │       ├── zonemaster_RU.json
│   │       ├── zonemaster_TK.json
│   │       └── zonemaster_UK.json
│   └── deploy360_dnssec_last20200713.csv
├── afri_cctld_ns.csv
├── afri_cctld_zonemaster_data.csv
├── afri_cctld_zonemaster_result.csv
└── top_cctld_cctld_ns.csv
```

## Jupyter notebook
For our analisys/results, we have use jupyter notebook available [here](./notebooks/AfTLDTechEnv.ipynb)

## Figures
All paper figures are available [here](./figures)

## Data collection
With all requirements satisfied, the script can be run as follow:

```
$ python3 data_collector.py
usage: data_collector.py [-h] -k {afri,top_cctld}
data_collector.py: error: the following arguments are required: -k/--kind
```
The script need one argument: `afri` to collect African ccTLDs data and `top_cctld` to collect top 10 ccTLDs data. Fo instance, to get top 10 ccTLDs data:

```
$ python3 data_collector.py -k top_cctld
Getting DNS Security Algorithm Numbers
Getting NRO Extended Allocation and Assignment Reports
Getting DNSSEC Deployment Maps
Getting PASSIVE ANYCAST result file
Getting GREEDY ANYCAST result file
Getting CAIDA IPv4 prefixes to ASN log   ../datasets/raw//20201024/prefixes_asn//pfx42as-creation.log
Getting CAIDA IPv4 prefixes to ASN mapping file   ../datasets/raw//20201024/prefixes_asn//pfx42as.gz
Getting CAIDA IPv6 prefixes to ASN log   ../datasets/raw//20201024/prefixes_asn//pfx62as-creation.log
Getting CAIDA IPv6 prefixes to ASN mapping file   ../datasets/raw//20201024/prefixes_asn//pfx62as.gz
Getting DNSSEC Algos
Formating DNSSEC Deployment Maps dataframe
Formating NRO allocation to file
IPv4 allocations 216508
IPv6 allocations 52768
Getting Prefix:ASN mapping...
Saving Prefix:ASN mapping to file ../datasets/raw//20201024/prefixes_asn//prefix_asn_pytricia.pickle
Formating ANYCAST to file
IPv4 anycast 3707
IPv6 anycast 5
Getting zone master results for TK
Checking NS records for TK
[]
No anycast 194.0.38.1
No anycast 2001:678:50:0:0:0:0:1
No anycast 194.0.39.1
No anycast 2001:678:54:0:0:0:0:1
No anycast 194.0.40.1
No anycast 2001:678:58:0:0:0:0:1
No anycast 194.0.41.1
No anycast 2001:678:5c:0:0:0:0:1
Getting zone master results for CN
Checking NS records for CN
Checking DS records for CN
[]
No anycast 2001:dc7:0:0:0:0:0:1
No anycast 203.119.25.1
No anycast 203.119.26.1
No anycast 203.119.27.1
No anycast 2001:dc7:1000:0:0:0:0:1
No anycast 203.119.28.1
No anycast 203.119.29.1
No anycast 195.219.8.90
No anycast 66.198.183.65
No anycast 202.112.0.44
Getting zone master results for DE
Checking NS records for DE
Checking DS records for DE
[]
No anycast 194.0.0.53
No anycast 2001:678:2:0:0:0:0:53
No anycast 2a02:568:0:2:0:0:0:53
No anycast 81.91.164.5
No anycast 2001:668:1f:11:0:0:0:105
No anycast 77.67.63.105
No anycast 2001:67c:1011:1:0:0:0:53
No anycast 195.243.137.26
No anycast 2003:8:14:0:0:0:0:53
No anycast 194.246.96.1
No anycast 2a02:568:fe02:0:0:0:0:de
Getting zone master results for UK
Checking NS records for UK
Checking DS records for UK
[]
No anycast 213.248.216.1
No anycast 2a01:618:400:0:0:0:0:1
No anycast 103.49.80.1
No anycast 2401:fd80:400:0:0:0:0:1
No anycast 213.248.220.1
No anycast 2a01:618:404:0:0:0:0:1
No anycast 2401:fd80:404:0:0:0:0:1
No anycast 43.230.48.1
No anycast 2001:502:ad09:0:0:0:0:3
No anycast 156.154.102.3
Getting zone master results for NL
Checking NS records for NL
Checking DS records for NL
[]
No anycast 194.0.28.53
No anycast 2001:678:2c:0:194:0:28:53
No anycast 194.0.25.24
No anycast 2001:678:20:0:0:0:0:24
Getting zone master results for RU
Checking NS records for RU
Checking DS records for RU
[]
No anycast 193.232.128.6
No anycast 2001:678:17:0:193:232:128:6
No anycast 194.85.252.62
No anycast 2001:678:16:0:194:85:252:62
No anycast 194.190.124.17
No anycast 2001:678:18:0:194:190:124:17
No anycast 193.232.142.17
No anycast 2001:678:15:0:193:232:142:17
No anycast 193.232.156.17
No anycast 2001:678:14:0:193:232:156:17
Getting zone master results for BR
Checking NS records for BR
Checking DS records for BR
[]
No anycast 200.219.148.10
No anycast 2001:12f8:6:0:0:0:0:10
No anycast 200.189.41.10
No anycast 2001:12f8:8:0:0:0:0:10
No anycast 200.192.233.10
No anycast 2001:12f8:a:0:0:0:0:10
No anycast 200.219.154.10
No anycast 2001:12f8:4:0:0:0:0:10
No anycast 200.229.248.10
No anycast 2001:12f8:2:0:0:0:0:10
No anycast 200.219.159.10
No anycast 2001:12f8:c:0:0:0:0:10
Getting zone master results for EU
Checking NS records for EU
Checking DS records for EU
[]
No anycast 91.200.16.100
No anycast 193.2.221.60
No anycast 2001:1470:8000:100:0:0:0:1
No anycast 194.0.25.28
No anycast 2001:678:20:0:0:0:0:28
No anycast 185.151.141.1
No anycast 2a02:568:fe00:0:0:0:0:6575
Getting zone master results for FR
Checking NS records for FR
Checking DS records for FR
[]
No anycast 194.0.9.1
No anycast 2001:678:c:0:0:0:0:1
No anycast 193.176.144.22
No anycast 2a00:d78:0:102:193:176:144:22
No anycast 2001:678:4c:0:0:0:0:1
Getting zone master results for IT
Checking NS records for IT
Checking DS records for IT
[]
No anycast 194.0.16.215
No anycast 2001:678:12:0:194:0:16:215
No anycast 192.12.192.5
No anycast 2a00:d40:1:1:0:0:0:5
No anycast 2001:1ac0:0:200:0:a5d1:6004:2
No anycast 217.29.76.4
No anycast 194.119.192.34
No anycast 2a00:1620:c0:220:194:119:192:34
No anycast 193.206.141.46
No anycast 2001:760:ffff:ffff:0:0:0:ca
```