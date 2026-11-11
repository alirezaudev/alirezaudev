<picture>
  <source media="(max-width: 640px)" srcset="assets/header-narrow.svg">
  <img src="assets/header.svg" alt="Alireza Mousavi, backend engineer since 2021. I like knowing why things are built the way they are, so I keep going one layer down. So far: Go and Laravel in production, algorithm practice in Go, Python and PHP, and Redis, DNS and HTTP rebuilt in Go. Now: operating system and networking internals. Next: my own SQLite from scratch, then system design in depth." width="100%">
</picture>

## <a href="https://github.com/alirezaudev/ttype"><img src="assets/ttype-wordmark.svg" alt="ttype" height="44"></a> <a href="https://github.com/alirezaudev/ttype/stargazers"><img src="https://img.shields.io/github/stars/alirezaudev/ttype?style=social" alt="GitHub stars" align="right"></a>

A typing test for people who live in the terminal. I kept tabbing out to a browser to warm up,
so I wrote the thing I kept opening. Code modes (Go, SQL, Python, shell, regex), keystroke
replays, a wpm chart, and a heatmap of the keys you actually miss. One static Go binary.

<a href="https://github.com/alirezaudev/ttype"><img src="https://raw.githubusercontent.com/alirezaudev/ttype/main/docs/demo.svg" alt="ttype: one sentence typed with one typo, and the results screen" width="100%"></a>

```sh
curl -fsSL https://raw.githubusercontent.com/alirezaudev/ttype/main/install.sh | sh
```

## Rebuilt from scratch, in Go

I rebuild tools I use every day to see how they work, with the standard library only.
Each one came down to one trade-off:

| &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | The problem | What I did | What it costs |
|:---:|---|---|---|
| <a href="https://github.com/alirezaudev/redis-from-scratch"><img src="assets/redis.svg" alt="Redis" height="34"></a> | A hundred clients share one map. A command that reads and then writes must not have another client land in between. | One goroutine owns the map. Every command is a message to it, so each one runs whole. | Commands run one at a time, on one core. Real Redis makes the same trade. |
| <a href="https://github.com/alirezaudev/dns-server-from-scratch"><img src="assets/dns.svg" alt="DNS" height="34"></a> | A reply repeats the same name in every record and has to fit in 512 bytes. | Point back at bytes already sent (name compression). | Every parser now follows pointers written by strangers. A hostile packet can loop them forever, so I stop at 20 hops. |
| <a href="https://github.com/alirezaudev/http-server-from-scratch"><img src="assets/http.svg" alt="HTTP" height="34"></a> | On a reused connection, a handler that skips the body leaves the next request starting mid-sentence. | Drain whatever the handler didn't read before parsing the next request. | Mine reads all of it, so a client can make me read 10 GB nobody asked for. `net/http` drains 256 KB, then hangs up. |

---

<sub>
Silver medal, <a href="https://quera.org/certificate/tbXa2fCE/">Quera Tech Olympics 2024</a> (PHP/Laravel) ·
practice and older work in <a href="https://github.com/alirezaudev-archive">alirezaudev-archive</a>
</sub>
