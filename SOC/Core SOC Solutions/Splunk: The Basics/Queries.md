# Splunk Search Processing Language (SPL) Cheat Sheet

This document contains the most common SPL commands that every SOC Analyst should know.

---

# search

```spl
search UserName=Maleena
```

### Description

Searches for events matching the specified condition.

### Common Use Cases

- Find a user
- Search an IP
- Search a hostname
- Search an Event ID

---

# index

```spl
index=vpn_logs
```

### Description

Limits the search to a specific index.

### Common Use Cases

- Search Windows logs
- Search Firewall logs
- Search VPN logs

---

# sourcetype

```spl
sourcetype=_json
```

### Description

Filters events based on the log format.

---

# source

```spl
source="VPNlogs.json"
```

### Description

Searches events from a specific log file.

---

# host

```spl
host="VPN_Connections"
```

### Description

Filters logs generated from a specific host.

---

# table

```spl
index=vpn_logs
| table UserName Source_ip Source_Country
```

### Description

Displays only the selected fields.

---

# fields

```spl
index=vpn_logs
| fields UserName Source_ip
```

### Description

Keeps only the specified fields.

---

# sort

```spl
index=vpn_logs
| sort UserName
```

### Description

Sorts the results alphabetically or numerically.

---

# head

```spl
index=vpn_logs
| head 10
```

### Description

Displays the first 10 events.

---

# tail

```spl
index=vpn_logs
| tail 10
```

### Description

Displays the last 10 events.

---

# stats count

```spl
index=vpn_logs
| stats count
```

### Description

Counts the total number of events.

---

# stats by

```spl
index=vpn_logs
| stats count by UserName
```

### Description

Counts events for each user.

---

# dedup

```spl
index=vpn_logs
| dedup UserName
```

### Description

Removes duplicate values.

---

# where

```spl
index=vpn_logs
| where Source_Country!="France"
```

### Description

Filters results using conditional expressions.

---

# eval

```spl
index=vpn_logs
| eval Country=upper(Source_Country)
```

### Description

Creates or modifies fields.

---

# rename

```spl
index=vpn_logs
| rename UserName as Username
```

### Description

Renames fields.

---

# rex

```spl
index=vpn_logs
| rex field=_raw "(?<IP>\d+\.\d+\.\d+\.\d+)"
```

### Description

Extracts data using Regular Expressions.

---

# timechart

```spl
index=vpn_logs
| timechart count
```

### Description

Displays events over time.

---

# top

```spl
index=vpn_logs
| top UserName
```

### Description

Shows the most common values.

---

# rare

```spl
index=vpn_logs
| rare UserName
```

### Description

Shows the least common values.

---

# lookup

```spl
| lookup users.csv UserName OUTPUT Department
```

### Description

Enriches events using an external lookup table.

---

# Common Operators

### Equal

```spl
UserName="Maleena"
```

### Not Equal

```spl
Source_Country!="France"
```

### AND

```spl
UserName="Maleena" AND Source_Country="USA"
```

### OR

```spl
UserName="Maleena" OR UserName="Smith"
```

### NOT

```spl
NOT Source_Country="France"
```

### Wildcard

```spl
UserName=Mal*
```

---

# SOC Analyst Commands Used Most Frequently

- search
- index
- source
- sourcetype
- host
- table
- fields
- stats
- eval
- where
- dedup
- sort
- top
- rare
- timechart
- rex
- lookup
