VPN gateway of Tencent Cloud is developed based on [strongSwan](https://www.strongswan.org/). It uses a non-routable ip address 169.254.x.x as its WAN interface private ip address. And it is mandatory to use FQDN method for peer identity. Otherwise, IKE establishment will be failed with the following error:



```
TANS/IKE_SA_ESTABLISH_FAIL: Failed to establish IKE SA for the reason of no peer config found by ID payload.
```



On Cisco ASA, you are recommended to config hostname and domain-name, and config `crypto isakmp identity hostname`.

There are many things that need to be taken care of when connecting Cisco ASA to Tencent Cloud VPN gateway.

IPSec fragmentation must be set to `after-encryption` instead of `before-encryption` by default. Otherwise, Tencent VPN gateway will be failed to parse hash payload.

Besides, tunnel-group name must be same as peer ip address. Otherwise, ASA cannot find a valid tunnel group.