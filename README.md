# snmp_generator_processes
SNMP generator to generate snmp.yml file to be used in prometheus to monitor running applications on linux server

Below given generator can generate snmp.yml for host-resources-MIBs.
Using snmp_exporter, use hr_mib module to get the list of running processes on any linux machine

You are welcome to modify this generator file for your needs

# Module

Below are the additional lines added in the generator file

```YAML
  hr_mib:
    walk: [1.3.6.1.2.1.25.4.2.1.2]
    lookups:
      - source_indexes: [hrSWRunIndex]
        lookup: hrSWRunName
      - source_indexes: [hrSWRunIndex]
        lookup: hrSWRunStatus
```
# Prometheus Alert Rules

You can use the following format to set an alert on any application if it goes down

```YAML
  - alert: ApplicationDown
    expr: absent(hrSWRunName{hrSWRunName="vsftpd"}) == 1
    for: 10s
    labels:
      severity: "critical"
    annotations:
      summary: "VSFTPD is down on NDOC machine"
```


