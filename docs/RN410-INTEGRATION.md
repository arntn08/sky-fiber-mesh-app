# SKYWORTH RN410 integration notes

## Hardware and local access
- Model: SKYWORTH RN410
- Observed local admin address: `http://192.168.55.254`
- The unit inspected was warehouse stock, not connected to a live customer network.

## Confirmed firmware interface sections
- Status dashboard
- Wi-Fi: separate 2.4 GHz and 5 GHz WLAN pages; guest network, WPS, access control and Wi-Fi schedule sections are visible.
- Connected Devices: Wireless and Wired tabs; MAC, IP, hostname, upload/download rate-limit fields; refresh and submit controls.
- EasyMesh: settings expose Controller, Agent and AP roles; topology page; node-add scan page.
- Advanced: ALG (FTP, SIP, RTSP, L2TP), IP Filter, URL Filter, MAC Filter, DDNS, DMZ and Port Forwarding sections.
- DMZ and Port Forwarding were reported OFF during inspection. No settings were changed.

## First observed request
- Method: `GET`
- URL: `http://192.168.55.254/skyrouter/skyInfoStatus.asp`
- Observed response:

```json
{
  "wan_status": 0,
  "need_apply": 0,
  "web_debug": 0
}
```

The exact meaning of `wan_status: 0` is not yet verified. Compare with the router UI before assigning a connected/disconnected meaning.

## Other observed request names
- `main.dot`
- `info_windows.dot`
- `skyInfoStatus.asp`

Their purpose and request/response formats have not yet been verified.

## Integration constraints and safety
- The current GitHub Pages PWA is a static HTTPS site. Browsers may block requests from it to the router's private HTTP address due to mixed-content, CORS, and authentication restrictions.
- Do not put router passwords, cookies, session tokens, or authorization headers in this repository or frontend code.
- Do not implement write operations until the relevant request method, parameters, authentication/CSRF behavior, and response are understood.
- A local companion bridge may be required for safe browser-to-router communication. It should bind to localhost/LAN intentionally, authenticate local clients, and never expose router credentials to a public service.
- Treat all interface capabilities above as UI-confirmed, not proof that the custom app can already control them.

## Next investigation when the RN410 is available
1. Inspect `info_windows.dot` and `main.dot` request methods, URLs, and sanitized responses.
2. Inspect the request triggered by Connected Devices > Refresh.
3. Inspect Wi-Fi page load requests (read-only) for 2.4 GHz and 5 GHz.
4. Inspect Mesh topology and node-scan read requests.
5. Record only sanitized request paths, methods, non-secret parameters, and response shapes.
6. Do not press Apply/Save or trigger pairing/reset actions during discovery.
