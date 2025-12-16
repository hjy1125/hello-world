def is_valid_ipv4(ip: str) -> bool:
    parts = ip.split('.')
    if len(parts) != 4:
        return False
    for p in parts:
        if not p.isdigit():
            return False
        n = int(p)
        if n < 0 or n > 255:
            return False
    return True

def ip_to_int(ip: str) -> int:
    parts = [int(p) for p in ip.split('.')]
    return (parts[0]<<24) + (parts[1]<<16) + (parts[2]<<8) + parts[3]

def in_same_subnet(ip1: str, ip2: str, mask: str) -> bool:
    return (ip_to_int(ip1) & ip_to_int(mask)) == (ip_to_int(ip2) & ip_to_int(mask))

if __name__ == "__main__":
    ip1 = input("请输入第一个IP地址: ").strip()
    ip2 = input("请输入第二个IP地址: ").strip()
    mask = input("请输入子网掩码 (如255.255.255.0): ").strip()

    if not is_valid_ipv4(ip1):
        print(f"{ip1} 不是合法的IPv4地址。")
    elif not is_valid_ipv4(ip2):
        print(f"{ip2} 不是合法的IPv4地址。")
    elif not is_valid_ipv4(mask):
        print(f"{mask} 不是合法的IPv4掩码。")
    else:
        if in_same_subnet(ip1, ip2, mask):
            print(f"{ip1} 和 {ip2} 在子网 {mask} 下同一网段。")
        else:
            print(f"{ip1} 和 {ip2} 不在子网 {mask} 下同一网段。")
