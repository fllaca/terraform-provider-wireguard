---
# generated by https://github.com/hashicorp/terraform-plugin-docs
page_title: "wireguard_config_document Data Source - terraform-provider-wireguard"
subcategory: ""
description: |-
  A WireGuard configuration document.
---

# wireguard_config_document (Data Source)

A WireGuard configuration document.

## Example Usage

```terraform
data "wireguard_config_document" "peer1" {
  private_key = wireguard_asymmetric_key.peer1.private_key
  listen_port = 1234
  dns = [
    "1.1.1.1",
    "1.0.0.1",
    "2606:4700:4700:0:0:0:0:64",
    "2606:4700:4700:0:0:0:0:6400",
  ]

  peer {
    public_key = wireguard_asymmetric_key.peer2.public_key
    allowed_ips = [
      "0.0.0.0/0",
    ]
    persistent_keepalive = 25
  }

  peer {
    public_key = wireguard_asymmetric_key.peer3.public_key
    endpoint   = "example.com:51820"
    allowed_ips = [
      "::/0",
    ]
  }
}

output "peer1" {
  value = data.wireguard_config_document.peer1.conf
}
```

<!-- schema generated by tfplugindocs -->
## Schema

### Required

- **private_key** (String) The base64 private key for this peer's interface.

### Optional

- **addresses** (Set of String) IPs (or CIDR) to be assigned to the interface. (`wg-quick`/apps only.)
- **dns** (Set of String) IPs or hostnames of Domain Name Servers to set as the interface's DNS search domains. (`wg-quick`/apps only.)
- **firewall_mark** (String) A 32-bit fwmark for outgoing packets.
- **id** (String) The ID of this resource.
- **listen_port** (Number) .
- **mtu** (Number) Manual MTU to override automatic discovery. (`wg-quick`/apps only.)
- **peer** (Block List) (see [below for nested schema](#nestedblock--peer))
- **post_down** (Set of String) Scripts to run before tearing down the interface. (`wg-quick`/apps only.)
- **post_up** (Set of String) Scripts to run after setting up the interface. (`wg-quick`/apps only.)
- **pre_down** (Set of String) Scripts to run before tearing down the interface. (`wg-quick`/apps only.)
- **pre_up** (Set of String) Script to run before setting up the interface. (`wg-quick`/apps only.)
- **routing_table** (Number) Controls the routing table (or "off") to which routes are added. (`wg-quick`/apps only.)

### Read-Only

- **conf** (String) The rendered config document.

<a id="nestedblock--peer"></a>
### Nested Schema for `peer`

Required:

- **public_key** (String) The base64 public key for this peer.

Optional:

- **allowed_ips** (Set of String) IPs (or CIDR) allowed for traffic to/from this peer.
- **endpoint** (String) An endpoint IP:port or hostname:port at which this peer can be reached initially.
- **persistent_keepalive** (Number) Period in seconds (or "off") after which to ping the peer to keep a stateful firewall or NAT mapping valid.
- **preshared_key** (String) A base64 preshared key from this peer.

