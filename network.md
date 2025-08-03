# Port & HTTP Testing Cheatsheet

## 1. **When to Use `nc` (Netcat)**
Check if a **TCP/UDP port is open** (reachability test).  
Works for any protocol.

**Basic TCP check**
```bash
nc -vz 127.0.0.1 3000     # Check if port 3000 is open (IPv4)
nc -vz [::1] 3000         # Check IPv6 loopback
```

**UDP check**
```bash
nc -vzu 127.0.0.1 5353    # Check UDP port
```

> ✅ Use `nc` for raw connectivity — tells you if *something* is listening.

---

## 2. **When to Use `curl`**
Check if an **HTTP/HTTPS endpoint** responds correctly.

**Status/headers only**
```bash
curl -I http://localhost:3000/auth/callback
```

**Verbose HTTP request**
```bash
curl -v http://localhost:3000/
```

> ✅ Use `curl` for protocol-level testing — confirms status codes, redirects, TLS, etc.

---

## 3. **Quick Debug Flow for Azure Entra ID Redirect**
1. **Check port is open (IPv4 & IPv6)**:
```bash
nc -vz 127.0.0.1 3000
nc -vz [::1] 3000
```

2. **Check HTTP endpoint**:
```bash
curl -I http://localhost:3000/auth/callback
```

3. **If IPv4 works but IPv6 fails** → Bind server to `0.0.0.0` or `::` with `ipv6Only: false`.

---

**Tip:** For binding fixes in Node.js:
```js
server.listen({ port: 3000, host: '::', ipv6Only: false });
```
