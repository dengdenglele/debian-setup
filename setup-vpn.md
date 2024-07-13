# Set up wireguard

```bash
# import .conf file generated by FritzBox
nmcli connection import type wireguard file /path/to/wg_config.conf

# turn on/off wireguard connection
## use the following commands in separate shell script or as alias for easy access
nmcli connection up wg_config
nmcli connection down wg_config

# disable autostart of wireguard VPN connection at startup
nmcli con mod wg_config connection.autoconnect no
```

- Use wireguard instead of port forwarding for access to FritzBox from the internet
- Wireguard tunnel is using asymmetric x25519 keys for authentication for each registered device
- HTTPS access to Fritzbox from the internet can be disabled (password authentication = never good!)
- Allows the usage of landline number (with Fritz Fon app) outside of local area network
- [Wireguard VPN unter Linux nutzen - Video Tutorial](https://www.youtube.com/watch?v=npDDELuiqxY)
- [How to stop wireguard vpn from auto connecting at startup?](https://www.reddit.com/r/kde/comments/17ud9kj/how_to_stop_wireguard_vpn_from_auto_connecting_at/)

# Set up University of Bamberg VPN

- Setup VPN first [(VPN unter Linux - Mit Bordmitteln)](https://www.uni-bamberg.de/its/dienstleistungen/netz/vpn/einrichten/linux/)
- Use integrated Linux solutions instead of GUI tools such as FortiClient

```bash 
# turn on/off vpn connection with Uni Bamberg
## use the following commands in separate shell script or as alias for easy access
nmcli connection up vpn_bamberg
nmcli connection down vpn_bamberg
```