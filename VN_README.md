# Tài liệu sử dụng Mesh DIY với Xiaomi Router 3G (R3G, Phiên bản USB3)

Firmware này được tối ưu để triển khai tự động **Wi-Fi mesh** và **backhaul mesh** trên băng tần **2.4GHz**.  
Hỗ trợ các giao thức roaming liền mạch: **802.11r, 802.11k, và 802.11v**, tối ưu hóa hiệu suất **VoIP** theo mặc định.
DNS được mã hóa bằng DoH và DoT, đồng thời quảng cáo bị chặn theo mặc định thông qua AdGuard DNS.

## Thiết lập Portal Node
1. Kết nối **cáp internet** vào **cổng WAN** của **node đầu tiên**.  Node này được gọi là **Portal Node**.
2. Cổng WAN mặc định được cấu hình là DHCP client, có thể login vào để đổi sang PPPoE nếu cần thiết.

## Thêm Peer Node
1. Bật nguồn các node còn lại.  
2. Chúng sẽ **tự động kết nối** vào mạng mesh thông với **Portal Node**.  
3. Các node này được gọi là **Peer Nodes**.

## Cấu hình Wi-Fi
Cả **Portal Node** và **Peer Nodes** đều phát sóng mạng Wi-Fi với:  
- **SSID:** `OpenWrt`  
- **Mật khẩu:** `12345678`  
- Tất cả thiết bị kết nối với SSID này dùng chung **mạng lớp 2** và dải subnet `192.168.20.0/20`.

## Khuyến nghị Backhaul có dây
Để đạt **hiệu suất tối ưu**, hãy kết nối dây mạng từ **cổng LAN** của **Portal Node** đến **cổng LAN** của **Peer Nodes** (nếu khả thi).

## Mạng Quản Lý
Mỗi node cũng phát sóng một mạng Wi-Fi riêng để quản lý:  
- **SSID:** `MGMT`  
- **Mật khẩu:** `123123123`  
- **Địa chỉ IP:** `172.20.0.1`  
- Sử dụng mạng này để **cấu hình và bảo trì router**.

## Tắt chế độ Mesh tự động
Để tắt chế độ mesh tự động, SSH vào router và chạy lệnh sau:

uci set mesh11sd.setup.auto_config=0
uci commit mesh11sd
reboot
