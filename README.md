
# 🛡️ h2socket Cloudflare Firewall Rules (Ultimate Defense)

These are **battle-tested, custom-made rules** to maximize protection using Cloudflare’s WAF. Built for real-world attacks, headless detection, ASN blocking, and high-threat scoring.

---

## 🚫 Global Protection

```txt
(http.request.method in {"PURGE" "PUT" "OPTIONS" "DELETE" "PATCH"}) or (not http.request.uri.path in {"/" "/login" "/register" "/dashboard" "/hub" "/hub.php" "/pricing" "/profile" "/api" "/profile.php" "/logout.php" "/logout" "/api.php" "/admin" "/admin/dashboard" "/admin/dashboard.php" "/admin/methods" "/admin/methods.php" "/admin/users" "/admin/users.php" "/admin/attacks" "/admin/attack.php" "/login.php" "/register.php"}) or (http.request.version in {"HTTP/1.0" "HTTP/1.2" "HTTP/1.1"} and not http.request.version in {"HTTP/2" "HTTP/3"} and http.user_agent contains "java") or (cf.threat_score ge 20)
```
Action = block

Blocks uncommon and risky HTTP methods and requests look + whitelist path only (you need to change that if you apply to your own site).

---

## 🚫 Known ASN (Cloud, Proxy, and Bot Providers)

```txt
(ip.src.asnum in {51167 14061 16276 24940 8075 200373 8560 60729 26548 210848 9087 4837 44477 210644 132203 40021 60223 60223 202656 200373})
```
Action = block

Block known ASN.

---

## 🧠 Suspect Countries and origins

```txt
(ip.geoip.asnum in {174 3236 4134 4766 4837 5650 6939 7203 7713 8075 12252 12586 14061 14576 14618 16276 16509 17552 17676 18779 20278 20473 21769 22612 23470 24940 28840 31898 32505 33387 35048 35624 35830 35913 36352 37963 38136 40676 43624 44066 45102 45899 46573 49505 51167 52000 54252 55081 55256 55286 59441 62005 62240 63949 64267 200000 206092 207633 207728 212238 265465 265579 271806 396982 397630} and ip.geoip.continent in {"T1" "XX"}) or (ip.geoip.country in {"T1" "XX"}) or (ip.geoip.country in {"T1"} and http.user_agent eq "") or (ip.geoip.continent in {"T1" "XX"}) or (ip.geoip.country in {"T1"}) or (http.host contains ":") or (ip.geoip.asnum eq 8075) or (http.request.uri contains "rand") or (http.request.uri contains "$") or (http.request.uri contains "%") or (http.request.uri contains "@") or (http.request.uri eq "~") or (cf.threat_score ge 5) or (http.request.version eq "HTTP/1.2") or (ip.geoip.asnum eq 17054) or (ip.geoip.asnum eq 577) or (http.user_agent contains "Slik") or (http.user_agent eq "") or (http.user_agent eq " ") or (http.user_agent eq "-") or (http.user_agent eq "'") or (http.user_agent contains "ALittle") or (http.user_agent contains ".NET") or (http.x_forwarded_for contains "192.0.") or (http.x_forwarded_for contains ".0.0") or (http.user_agent contains "NT 6.2") or (http.user_agent contains "NT 6.3") or (http.user_agent contains "NT 5.1") or (ip.geoip.asnum eq 211720) or (ip.geoip.asnum eq 271633) or (ip.geoip.asnum eq 266542) or (ip.geoip.asnum eq 45317) or (ip.geoip.asnum eq 64267) or (ip.geoip.asnum eq 6939) or (ip.geoip.asnum eq 54252) or (http.user_agent contains "LM-Q") or (not http.user_agent contains "Mozilla/5.0") or (ip.geoip.asnum eq 24961 and http.request.version ne "HTTP/3")
```
Action = block

Block suspect countries/origins.

---

## ⚠️ Captcha

```txt
(http.request.uri.path ne "/gjjgu7gkug" and not cf.client.bot and not http.user_agent contains "Googlebot")
```
Action = interractive challenge

Gives challenge to everyone except google bots (for ranking).

---

## 💾 Site-wide Settings

| Setting         | Value               |
|----------------|---------------------|
| Cache Level     | Cache Everything    |
| Always Online   | Enabled             |
| Under Attack Mode (UAM) | Enabled when under attack |

---

## ✅ How to Use

Paste these expressions into your **Cloudflare → Security → WAF → Custom Rules**, and apply the corresponding actions (`Block`, `JS Challenge`, or `Managed Challenge`).

Use **Rate Limiting**, **Bot Fight Mode**, and **Managed Rulesets** to further enhance protection.

---

Made by **h2socket** ⚔️  
Hardening the internet one rule at a time.
