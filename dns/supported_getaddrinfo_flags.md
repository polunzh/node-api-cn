
以下内容可以作为 hints 标志传给 [`dns.lookup()`]。

- `dns.ADDRCONFIG`: 返回当前系统支持的地址类型。例如，如果当前系统至少配置了一个 IPv4 地址，则返回 IPv4 地址。不考虑回环地址。
- `dns.V4MAPPED`: 如果指定了 IPv6 地址族，但是没有找到 IPv6 地址，则返回 IPv4 映射的 IPv6 地址。在有些操作系统中不支持（例如 FreeBSD 10.1）。

