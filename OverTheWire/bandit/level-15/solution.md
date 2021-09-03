# Bandit Level 15

## Goal
The password for the next level can be retrieved by submitting the password of the current level to port 30001 on localhost using SSL encryption.

Helpful note: Getting “HEARTBEATING” and “Read R BLOCK”? Use -ign_eof and read the “CONNECTED COMMANDS” section in the manpage. Next to ‘R’ and ‘Q’, the ‘B’ command also works in this version of that command…

## Solution
First connect through secure shell using `bandit15` as username and the password found in level 14
`ssh bandit15@bandit.labs.overthewire.org -p 2220`

Enter password when prompted.

This exercise is similar to previous one but with the difference that this time we will connect using secure connection using `tls` protocol. In this case we can't use `nc` because that one is not secure.

After reading a bit the `openssl` man pages we found that `openssl` command has a sub-command called `s_client` that creates a secure connection using `tls` protocol. So we decided to give it a try as follow:

`echo "<password of this level>" | openssl s_client -connect localhost:30001 -ign_eof` and we got the following output:

```
CONNECTED(00000003)
depth=0 CN = localhost
verify error:num=18:self signed certificate
verify return:1
depth=0 CN = localhost
verify return:1
---
Certificate chain
 0 s:/CN=localhost
   i:/CN=localhost
---
Server certificate
-----BEGIN CERTIFICATE-----
MIICBjCCAW+gAwIBAgIEHxhZ+zANBgkqhkiG9w0BAQUFADAUMRIwEAYDVQQDDAls
b2NhbGhvc3QwHhcNMjEwODA1MjEyMjEzWhcNMjIwODA1MjEyMjEzWjAUMRIwEAYD
VQQDDAlsb2NhbGhvc3QwgZ8wDQYJKoZIhvcNAQEBBQADgY0AMIGJAoGBALqNmx6R
csRsPgzRcRsq5oQ4BC9AT/Yu473WbK4SRjHOWwuA4Oqk9w8SLKYZ39FrDEnXSZJw
xqKPR0AH72+l7Itv7X1H07VbeMTQoJVm6NsJm3cuyyxjRwfaIOUFsRtQQyvQlmw7
3CgTbd3wEk1CD+6jlksJj801Vd0uvZh1VVERAgMBAAGjZTBjMBQGA1UdEQQNMAuC
CWxvY2FsaG9zdDBLBglghkgBhvhCAQ0EPhY8QXV0b21hdGljYWxseSBnZW5lcmF0
ZWQgYnkgTmNhdC4gU2VlIGh0dHBzOi8vbm1hcC5vcmcvbmNhdC8uMA0GCSqGSIb3
DQEBBQUAA4GBADjhbe3bTnDWsS4xt8FFg7PJIqNAxF6QjP+7xzJ4yMvWtPP6tVXo
F7SNI52juwH0nFDyM9KOrM/AknWqCYF+yfz6bLD7MaKZ+Kg3DiLaoVJOrVg6Y02+
0vq1rLsqGko5wamCFamx7X9CtFsV0WQjZdA53Na/VwehtlFpf/p20VAi
-----END CERTIFICATE-----
subject=/CN=localhost
issuer=/CN=localhost
---
No client certificate CA names sent
Peer signing digest: SHA512
Server Temp Key: X25519, 253 bits
---
SSL handshake has read 1019 bytes and written 269 bytes
Verification error: self signed certificate
---
New, TLSv1.2, Cipher is ECDHE-RSA-AES256-GCM-SHA384
Server public key is 1024 bit
Secure Renegotiation IS supported
Compression: NONE
Expansion: NONE
No ALPN negotiated
SSL-Session:
    Protocol  : TLSv1.2
    Cipher    : ECDHE-RSA-AES256-GCM-SHA384
    Session-ID: 5DF29DA063C43BF9E5E36DEB1630A48D3BB740D3743787530A500390A8AC7CF5
    Session-ID-ctx:
    Master-Key: B860BFA55A72E94DF7C7965308AA08F96E578232C7CB695BDFD90D53E09AEB69E60B074800F0B2D813D381A81DB94DA7
    PSK identity: None
    PSK identity hint: None
    SRP username: None
    TLS session ticket lifetime hint: 7200 (seconds)
    TLS session ticket:
    0000 - 3a a9 fe 3b 12 a1 ed 2b-8d a6 cf aa 23 c9 12 88   :..;...+....#...
    0010 - 20 17 e7 43 a9 85 61 d5-4c 18 7d c3 c8 fe 48 03    ..C..a.L.}...H.
    0020 - e0 3f 03 11 43 eb bd a7-dd 93 62 4b 00 66 a5 97   .?..C.....bK.f..
    0030 - c4 6a 0f e1 57 09 a0 8b-d0 4b 2e 78 45 c7 7d a6   .j..W....K.xE.}.
    0040 - 51 48 56 de cb cf 89 60-8f 27 94 4f a5 4f 5b 03   QHV....`.'.O.O[.
    0050 - cf e6 de e8 be c9 43 c9-d8 93 00 c0 13 4f 5a 22   ......C......OZ"
    0060 - b6 9b 1e cb 01 ad b8 bb-d4 07 51 e2 d3 a4 c2 e5   ..........Q.....
    0070 - 80 9b a5 d5 b6 cf 82 58-16 51 83 06 ad d2 44 bf   .......X.Q....D.
    0080 - 13 80 d8 12 54 ff d8 ac-29 5a 03 0a 4e 81 b2 d9   ....T...)Z..N...
    0090 - f9 37 e9 4a e0 52 b8 2a-1e cf 46 3b 90 fe 21 ab   .7.J.R.*..F;..!.

    Start Time: 1630202386
    Timeout   : 7200 (sec)
    Verify return code: 18 (self signed certificate)
    Extended master secret: yes
---
Correct!
cluFn7wTiGryunymYOu4RcffSxQluehd

closed
```

At the end of this huge output we can see the response from the server `Correct!` and below the password for next level.

>Note: We used the -ign_eof flag as advice in the Goal section to keep the connection open until receiving the response from server.

password: `cluFn7wTiGryunymYOu4RcffSxQluehd`