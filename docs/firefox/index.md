# Firefox

## Disable ECH (Encrypted Client Hello)
  1. Navigate to "about:config" in the URL bar.
  2. In the configuration search bar enter: "ech"
  3. Locate these 2 items and change them to "false":
    - network.dns.echconfig.enabled
    - network.dns.http3_echconfig.enabled