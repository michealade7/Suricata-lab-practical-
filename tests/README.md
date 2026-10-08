# Suricata Tests

Use this folder to document validation and controlled detection tests.

Primary configuration test:
```bash
sudo suricata -T -c /etc/suricata/suricata.yaml
```

Primary traffic test:
```bash
ping -c 4 <LAB-TARGET-IP>
```

Expected custom alert:
`SURICATA ICMP TEST ALERT`
