# Documentation for Setting Up a DIY Mesh Network with the Xiaomi Router 3G (also called R3G, USB3 Version)

This firmware is optimized for deploying automatic Wi-Fi mesh and backhaul mesh on the 2.4GHz band.  
Supports seamless roaming protocols: **802.11r, 802.11k, and 802.11v**, optimized for VoIP performance by default.
DNS is encrypted using DoH and DoT, and ads are blocked by default with AdGuard DNS.

## Initial Setup
1. Connect the internet cable to the **WAN** port of the first node. This node is called the **Portal Node**.
2. The default WAN port is configured as a DHCP client. You can log in to switch to PPPoE if needed.

## Adding Peer Nodes
1. Power on the remaining nodes.  
2. They will automatically join the mesh network via the **Portal Node** (the first node).  
3. These nodes are referred to as **Peer Nodes**.

## Wi-Fi Configuration
Both **Portal Node** and **Peer Nodes** broadcast a Wi-Fi network with:  
- **SSID:** `OpenWrt`  
- **Password:** `12345678`  
- All devices connected to this SSID share the same **Layer 2** network and the subnet `192.168.20.0/20`.

## Wired Backhaul Recommendation
For optimal performance, connect a ethernet cable from the **LAN port** of the **Portal Node** to the **LAN port** of a **Peer Node** (if feasible).

## Management Network
Each node also broadcasts a dedicated management Wi-Fi network:  
- **SSID:** `MGMT`  
- **Password:** `123123123`  
- **IP Address:** `172.20.0.1`  
- Use this network for **router configuration and maintenance**.

## Disabling Auto Mesh
To disable auto mesh, SSH into the router and run:

uci set mesh11sd.setup.auto_config=0
uci commit mesh11sd
reboot
