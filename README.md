# proxy-list

Free HTTP, SOCKS4 and SOCKS5 proxies, re-checked every hour.

Every proxy in this repository was verified minutes ago by [monosans/proxy-scraper-checker](https://github.com/monosans/proxy-scraper-checker) running on my server. Each one had to fetch a real URL _in full_ to make the list, so proxies that connect and then stall never appear. Response time, exit IP, network owner and city come attached.

No signup, no API key, no rate limit. They are raw files served by GitHub.

## Get the list

| File                                                                                                    | Contents                                 |
| ------------------------------------------------------------------------------------------------------- | ---------------------------------------- |
| [`proxies/all.txt`](https://raw.githubusercontent.com/monosans/proxy-list/main/proxies/all.txt)         | every proxy, prefixed with `protocol://` |
| [`proxies/http.txt`](https://raw.githubusercontent.com/monosans/proxy-list/main/proxies/http.txt)       | HTTP only, bare `host:port`              |
| [`proxies/socks4.txt`](https://raw.githubusercontent.com/monosans/proxy-list/main/proxies/socks4.txt)   | SOCKS4 only, bare `host:port`            |
| [`proxies/socks5.txt`](https://raw.githubusercontent.com/monosans/proxy-list/main/proxies/socks5.txt)   | SOCKS5 only, bare `host:port`            |
| [`proxies.json`](https://raw.githubusercontent.com/monosans/proxy-list/main/proxies.json)               | everything, with metadata                |
| [`proxies_pretty.json`](https://raw.githubusercontent.com/monosans/proxy-list/main/proxies_pretty.json) | the same JSON, indented                  |

Proxies are sorted fastest first, so the top of each file is the best of what was working at the last update. The commit message for every update lists the per-protocol counts.

```bash
curl -fsSL https://raw.githubusercontent.com/monosans/proxy-list/main/proxies/socks5.txt
```

## What's in the JSON

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

`timeout` is how long the complete request took, in seconds: connection, request and full response. That is what the fastest-first ordering uses. `exit_ip` is the address the target site actually saw; compare it with `host` to spot proxies that forward through somewhere else.

`geolocation` mirrors the GeoLite2 City record, abbreviated here. Fields the database has no data for are omitted, and names are English only. The [tool's README](https://github.com/monosans/proxy-scraper-checker#output) documents the full shape.

## Read this before using them

These are anonymous proxies collected from public sources. Whoever runs one can see, log and modify everything that passes through it.

So never send credentials, tokens or personal data through a proxy from this list, and stick to HTTPS, which keeps the operator from reading or rewriting the response.

Expect them to die, too. They are free and volatile, and a proxy that worked at the top of the hour may be gone by the next update, so re-fetch the list rather than caching it.

If you need proxies you can actually rely on, use a paid provider.

## Run it yourself

[monosans/proxy-scraper-checker](https://github.com/monosans/proxy-scraper-checker) builds the same kind of list from your own sources, checked against your own URL, on your own schedule. It is a single binary for Windows, Linux, macOS and Android.

## Sponsors

|                                                              |                                                                                                                                                               |
| ------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **[RapidProxy.io](https://www.rapidproxy.io/?ref=monosans)** | <a href="https://www.rapidproxy.io/?ref=monosans"><img width="400" src="https://github.com/user-attachments/assets/143ed7cc-c200-4563-9253-4ccedcd3ecd5"></a> |

Want your name in this section? Support the project and it goes here.

### Support this project

Star the repository so other people can find it. If you are interested in sponsoring, [DM me on Telegram](https://t.me/monosans).

## License

[MIT](LICENSE)

_This product includes GeoLite2 Data created by MaxMind, available from <https://www.maxmind.com>_
