**Commands to setup WireGuard server using router SSH:**

- **interface/wireguard/add** comment="Wireguard VPN" listen-port=[PORT] mtu=1420 name="wg1"
- **interface/wireguard/peers/add** interface=wg1 public-key="%_user public key_%" allowed-address=0.0.0.0/0 comment="%_user_% WG"
- **ip/address/add** address=10.0.0.0/24 interface=wg1 comment="Wireguard VPN"
- **ip/firewall/filter/add** action=accept chain=input protocol=udp dst-port=[PORT] comment="Wireguard VPN"
 - **Важный момент**, правило созданное в данной строчке нужно переместить на второй слот:
 - ip/firewall/filter/print
 - ip/firewall/filter/move numbers=[RULE NUMBER] destination=2
- **interface/list/member/add** list=LAN interface=wireguard1 comment="Wireguard VPN"

**interface/wireguard/print**, получаем public-key необходимый пользователю для подключения. 
