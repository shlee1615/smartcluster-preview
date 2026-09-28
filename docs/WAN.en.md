# Connecting Across Networks

[Home](../README.md) · [繁體中文](WAN.zh-TW.md) · [User guide](USER_GUIDE.en.md)

The first preview provides Tailscale setup guidance, not a managed VPN. Current-version LAN testing passed; limited Tailscale testing exists for an older version. Current-version WAN and extended operation still require acceptance.

## Accounts and responsibilities

Customers or their IT teams manage their own Tailscale accounts, tailnets, devices, and access rules. Do not place unrelated customers in a supplier's personal network or share logins. Check the current [official plans](https://tailscale.com/pricing) and applicable terms for your actual use; do not assume a free individual plan covers a customer deployment. This document grants no product or third-party commercial license.

An enterprise VPN, WireGuard, or NetBird may provide the required routing, but these have not been validated for this preview. A VPN supplies reachability; SmartCluster pairing, mTLS, and local permissions are still required.

## Setup sequence

1. Install [official Tailscale](https://tailscale.com/download) under your IT policy and join the approved tailnet.
2. Verify the Hub's stable address. The VPN interface must be ready before its service starts.
3. Use that Hub's actual Tailscale IPv4 when creating the group. Complete a local diagnostic first. There is no graphical editor for an existing gateway address.
4. Start the Hub, create an invitation, and deliver it privately to the intended member. Verify the group, Hub URL, and CA fingerprint.
5. Permit only the required sources and destination TCP port from the invitation URL. Ports differ between groups. Do not expose local management pages or unrelated remote services.
6. Join, start the member service, enable intake for the group, and complete a diagnostic. This alone does not validate AI, App intake, or all WAN behavior.

For timeouts, check routing, actual ports, service health, and rules. For TLS errors, check clocks, addresses, and invitation provenance; keep verification enabled. Address changes and key lifecycles require separate maintenance; no complete renewal wizard is available. Stopping the Hub disconnects its members. SmartCluster does not install VPN software, modify firewalls automatically, or promise a public relay service.
