# Suricata IDS Lab Workflow

## Phase 1 — Check installation
```bash
suricata --build-info
suricata -V
```

If Suricata is not installed:
```bash
sudo apt update
sudo apt install suricata -y
suricata -V
```

## Phase 2 — Identify the interface
```bash
ip addr
ip route
```

Use the interface shown by the default route. Example:
`default via 192.168.1.1 dev eth0`

Do not assume the interface is `eth0`.

## Phase 3 — Back up configuration
```bash
sudo cp /etc/suricata/suricata.yaml /etc/suricata/suricata.yaml.backup
ls -l /etc/suricata/
```

## Phase 4 — Configure Suricata
Open:
```bash
sudo nano /etc/suricata/suricata.yaml
```

Review:
- `HOME_NET`
- `af-packet`
- `default-rule-path`
- `rule-files`

Set `HOME_NET` to the appropriate network for the lab.

Set the `af-packet` interface to the actual interface discovered with `ip route`.

## Phase 5 — Update rules
```bash
sudo suricata-update
ls -lh /var/lib/suricata/rules/
```

## Phase 6 — Create custom rule
```bash
sudo nano /etc/suricata/rules/local.rules
```

Add:
```text
alert icmp any any -> any any (msg:"SURICATA ICMP TEST ALERT"; sid:1000001; rev:1;)
```

## Phase 7 — Add the custom rule
In `suricata.yaml`, ensure:
```yaml
default-rule-path: /var/lib/suricata/rules
```

and:
```yaml
rule-files:
  - suricata.rules
  - /etc/suricata/rules/local.rules
```

## Phase 8 — Validate
```bash
sudo suricata -T -c /etc/suricata/suricata.yaml
```

Check the custom SID:
```bash
sudo suricata -T -c /etc/suricata/suricata.yaml 2>&1 | grep 1000001
```

Check the message:
```bash
sudo suricata -T -c /etc/suricata/suricata.yaml 2>&1 | grep "SURICATA ICMP TEST ALERT"
```

## Phase 9 — Start Suricata
```bash
sudo systemctl restart suricata
sudo systemctl status suricata
```

## Phase 10 — Generate traffic
Find the target on the controlled lab network and generate ICMP traffic:
```bash
ping -c 4 <LAB-TARGET-IP>
```

## Phase 11 — Verify alerts
```bash
sudo tail -f /var/log/suricata/fast.log
```

Structured events:
```bash
sudo tail -f /var/log/suricata/eve.json
```

Optional:
```bash
sudo apt install jq -y
sudo tail -f /var/log/suricata/eve.json | jq
```
