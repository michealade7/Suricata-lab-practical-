# Suricata IDS Lab

A GitHub-ready workflow for the Suricata IDS setup and custom ICMP detection lab.

## Lab Objective
Configure Suricata on Kali Linux, identify the correct network interface, configure
`HOME_NET` and `af-packet`, update the Suricata ruleset, create a custom ICMP alert rule,
validate the configuration, start Suricata, generate controlled ICMP traffic, and verify
the resulting alerts.

## Workflow
1. Check Suricata installation
2. Identify the network interface
3. Back up `suricata.yaml`
4. Configure `HOME_NET`
5. Configure the network interface
6. Configure the rule path
7. Install/update Suricata rules
8. Create `local.rules`
9. Add `local.rules` to `suricata.yaml`
10. Test the configuration
11. Verify the custom rule
12. Start/restart Suricata
13. Check `suricata.log`
14. Generate ICMP traffic
15. Check `fast.log`
16. Check `eve.json`
17. Document evidence and results

## Custom Test Rule
```text
alert icmp any any -> any any (msg:"SURICATA ICMP TEST ALERT"; sid:1000001; rev:1;)
```

## Important
Do not blindly use `eth0` or a sample IP/network. Use the interface and network shown by
your own Kali VM with `ip addr` and `ip route`.

## Evidence
Store real screenshots and terminal output in the `evidence/` directory. Do not fabricate
successful results.
