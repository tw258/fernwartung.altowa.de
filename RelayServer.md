# Rustdesk

###### tags: `rustdesk` `selfhosting` `altowa`

# oss.yml -> ~/rustdesk/docker-compose.yml

```yml
services:
  hbbs:
    container_name: hbbs
    image: rustdesk/rustdesk-server:latest
    command: hbbs
    volumes:
      - ./data:/root
    network_mode: "host"
    depends_on:
      - hbbr
    restart: unless-stopped

  hbbr:
    container_name: hbbr
    image: rustdesk/rustdesk-server:latest
    command: hbbr
    volumes:
      - ./data:/root
    network_mode: "host"
    restart: unless-stopped
```

# docker-compose up

```
tobi@altowa2:~/rustdesk$ docker compose up
[+] up 6/6
 ✔ Image rustdesk/rustdesk-server:latest Pulled          2.9s
 ✔ Container hbbr                        Created         0.1s
 ✔ Container hbbs                        Created         0.0s
Attaching to hbbr, hbbs
hbbr  | [2026-04-23 09:45:35.489180 +00:00] INFO [src/relay_server.rs:61] #blacklist(blacklist.txt): 0
hbbr  | [2026-04-23 09:45:35.489266 +00:00] INFO [src/relay_server.rs:76] #blocklist(blocklist.txt): 0
hbbr  | [2026-04-23 09:45:35.489276 +00:00] INFO [src/relay_server.rs:82] Listening on tcp :21117
hbbr  | [2026-04-23 09:45:35.489287 +00:00] INFO [src/relay_server.rs:84] Listening on websocket :21119
hbbr  | [2026-04-23 09:45:35.489296 +00:00] INFO [src/relay_server.rs:87] Start
hbbr  | [2026-04-23 09:45:35.489340 +00:00] INFO [src/relay_server.rs:105] DOWNGRADE_THRESHOLD: 0.66
hbbr  | [2026-04-23 09:45:35.489348 +00:00] INFO [src/relay_server.rs:115] DOWNGRADE_START_CHECK: 1800s
hbbr  | [2026-04-23 09:45:35.489356 +00:00] INFO [src/relay_server.rs:125] LIMIT_SPEED: 32Mb/s
hbbr  | [2026-04-23 09:45:35.489363 +00:00] INFO [src/relay_server.rs:136] TOTAL_BANDWIDTH: 1024Mb/s
hbbr  | [2026-04-23 09:45:35.489370 +00:00] INFO [src/relay_server.rs:146] SINGLE_BANDWIDTH: 128Mb/s
hbbs  | [2026-04-23 09:45:35.719258 +00:00] INFO [src/common.rs:147] Private/public key written to id_ed25519/id_ed25519.pub
hbbs  | [2026-04-23 09:45:35.719324 +00:00] INFO [src/rendezvous_server.rs:1251] Key: P7uc8f3iq9d9QRBhVzDqiBcLaZXoJIndQCg1U+5oA9M=
hbbs  | [2026-04-23 09:45:35.719337 +00:00] INFO [src/peer.rs:84] DB_URL=./db_v2.sqlite3
hbbs  | [2026-04-23 09:45:35.720928 +00:00] INFO [libs/hbb_common/src/config.rs:895] Generated new keypair for id:
hbbs  | [2026-04-23 09:45:35.753502 +00:00] INFO [src/rendezvous_server.rs:107] serial=0
hbbs  | [2026-04-23 09:45:35.753546 +00:00] INFO [src/common.rs:45] rendezvous-servers=[]
hbbs  | [2026-04-23 09:45:35.753561 +00:00] INFO [src/rendezvous_server.rs:109] Listening on tcp/udp :21116
hbbs  | [2026-04-23 09:45:35.753570 +00:00] INFO [src/rendezvous_server.rs:110] Listening on tcp :21115, extra port for NAT test
hbbs  | [2026-04-23 09:45:35.753583 +00:00] INFO [src/rendezvous_server.rs:111] Listening on websocket :21118
hbbs  | [2026-04-23 09:45:35.754417 +00:00] INFO [src/rendezvous_server.rs:146] mask: None
hbbs  | [2026-04-23 09:45:35.754431 +00:00] INFO [src/rendezvous_server.rs:147] local-ip: ""
hbbs  | [2026-04-23 09:45:35.754445 +00:00] INFO [src/common.rs:45] relay-servers=[]
hbbs  | [2026-04-23 09:45:35.754510 +00:00] INFO [src/rendezvous_server.rs:161] ALWAYS_USE_RELAY=N
hbbs  | [2026-04-23 09:45:35.755926 +00:00] INFO [src/rendezvous_server.rs:193] Start
hbbs  | [2026-04-23 09:49:37.280362 +00:00] INFO [src/peer.rs:102] update_pk 221136745 [::ffff:31.19.160.145]:51796 b"02314f7fbc1f4557a158e6210d6733ec" b">\xb7\xff\xa5\x12$\x1a\xfe<u+C\xc0\xc6K\x8b\x89\x05N]ZH\xed\xad\x19r\x07\\r\xac\xab\xf5"
```

# Automatically creates data folder:

```
tobi@altowa2:~$ ls -lha rustdesk/data/
total 64K
drwxr-xr-x 3 root root 132 Apr 23 12:21 .
drwxrwxr-x 3 tobi tobi  44 Apr 23 12:18 ..
drwxr-xr-x 3 root root  22 Apr 23 11:45 .config
-rw-r--r-- 1 root root 24K Apr 23 12:13 db_v2.sqlite3
-rw-r--r-- 1 root root 32K Apr 23 12:21 db_v2.sqlite3-shm
-rw-r--r-- 1 root root   0 Apr 23 12:21 db_v2.sqlite3-wal
-rw-r--r-- 1 root root  88 Apr 23 11:45 id_ed25519
-rw-r--r-- 1 root root  44 Apr 23 11:45 id_ed25519.pub     # <-- pubkey!
```

# Pubkey for client config

```
tobi@altowa2:~$ cat rustdesk/data/id_ed25519.pub
P7uc8f3iq9d9QRBhVzDqiBcLaZXoJIndQCg1U+5oA9M=
```

# Client GUI config

![](https://pad.gfuzz.de/uploads/f0aa87ea-478e-409c-98fa-09addc25f991.png)

# Server pf.conf

```
rdr pass on $ext_if proto tcp from any to $ext_if:network port 21115 -> 10.8.0.102 port 21115
rdr pass on $ext_if proto {tcp, udp} from any to $ext_if:network port 21116 -> 10.8.0.102 port 21116
rdr pass on $ext_if proto udp from any to $ext_if:network port 21117 -> 10.8.0.102 port 21117
```
