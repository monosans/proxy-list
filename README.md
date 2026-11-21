# <img src="assets/logo.svg" alt="" width="40" align="top"> proxy-list

Free HTTP, SOCKS4 and SOCKS5 proxies, re-checked every hour.

Every proxy here was verified minutes before the last commit by [proxy-scraper-checker](https://github.com/monosans/proxy-scraper-checker). To make the list, a proxy had to fetch a real URL in full, so proxies that connect and then stall never appear. Each one comes with its response time, exit IP, network owner and location.

No signup, no API key, no rate limit: these are plain files served by GitHub.

## Get the list

| File                                                                                                    | Contents                                 |
| ------------------------------------------------------------------------------------------------------- | ---------------------------------------- |
| [`proxies/all.txt`](https://raw.githubusercontent.com/monosans/proxy-list/main/proxies/all.txt)         | every proxy, prefixed with `protocol://` |
| [`proxies/http.txt`](https://raw.githubusercontent.com/monosans/proxy-list/main/proxies/http.txt)       | HTTP only                                |
| [`proxies/socks4.txt`](https://raw.githubusercontent.com/monosans/proxy-list/main/proxies/socks4.txt)   | SOCKS4 only                              |
| [`proxies/socks5.txt`](https://raw.githubusercontent.com/monosans/proxy-list/main/proxies/socks5.txt)   | SOCKS5 only                              |
| [`proxies.json`](https://raw.githubusercontent.com/monosans/proxy-list/main/proxies.json)               | every proxy, with metadata               |
| [`proxies_pretty.json`](https://raw.githubusercontent.com/monosans/proxy-list/main/proxies_pretty.json) | the same JSON, indented                  |

Each line is `host:port`, or `username:password@host:port` for a proxy that needs credentials. Only `all.txt` puts `protocol://` in front.

Every file is sorted fastest first, so the top lines are the best of what worked at the last update. Each update's commit message lists how many proxies of each protocol made it.

```bash
# Download the SOCKS5 list
curl -fsSL https://raw.githubusercontent.com/monosans/proxy-list/main/proxies/socks5.txt -o socks5.txt

# Send a request through the fastest one
curl -x "socks5h://$(head -n 1 socks5.txt)" https://example.com
```

## What's in the JSON

`proxies.json` is an array of objects like this one:

```json
{
  "protocol": "socks5",
  "username": null,
  "password": null,
  "host": "1.2.3.4",
  "port": 1080,
  "timeout": 0.14,
  "exit_ip": "1.2.3.4",
  "asn": {
    "autonomous_system_number": 12345,
    "autonomous_system_organization": "Example Networks"
  },
  "geolocation": {
    "country": { "iso_code": "US", "names": { "en": "United States" } },
    "city": { "names": { "en": "Chicago" } },
    "location": {
      "latitude": 41.85,
      "longitude": -87.65,
      "time_zone": "America/Chicago"
    }
  }
}
```

- `timeout` is how long the whole check took, in seconds: connecting, sending the request and receiving the full response. The fastest-first order follows it.
- `exit_ip` is the address the target site saw. When it differs from `host`, the proxy forwards traffic through another machine.
- `asn` and `geolocation` describe `exit_ip`. They follow the GeoLite ASN and City records, shortened above: fields with no data are left out, and names are English only. The [proxy-scraper-checker README](https://github.com/monosans/proxy-scraper-checker#output) documents the full shape.

## Read this before using them

These are open proxies collected from public sources. Whoever runs one can see, log and change everything that passes through it.

- Never send passwords, tokens or personal data through them.
- Use HTTPS, so the operator can neither read nor rewrite your traffic.
- Expect them to die. A proxy that worked at the top of the hour may be gone by the next update, so download the list again instead of keeping an old copy.

If you need proxies you can rely on, use a paid provider.

## Run it yourself

[proxy-scraper-checker](https://github.com/monosans/proxy-scraper-checker) builds the same kind of list from your own sources, checks it against your own URL and runs on your own schedule. It is a single binary for Windows, Linux, macOS and Android, and also a Docker image.

## Support the project

Star the repository so more people can find it. To sponsor the project and get your name listed here, [message me on Telegram](https://t.me/monosans).

## License

The proxy lists are available under the [MIT License](LICENSE).

The `asn` and `geolocation` fields of the JSON files are GeoLite Data created by MaxMind, available from <https://www.maxmind.com>. They are licensed under the [Creative Commons Attribution-ShareAlike 4.0 International License](https://creativecommons.org/licenses/by-sa/4.0/), as the [GeoLite End User License Agreement](https://www.maxmind.com/en/geolite2/eula) provides. If you reuse them, credit MaxMind and share them under the same license.

_This product includes GeoLite Data created by MaxMind, available from <https://www.maxmind.com>._
