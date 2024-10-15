# rustdesk-apt-repo
Marged version of RustDesk apt repo, but upload to Cloudflare R2.

## Add this repo
### Add GPG key
Nightly and latest are sharing same GPG key.
```
curl -fsSL https://rustdesk-apt-repo.xlion.dev/pubkey.gpg | sudo gpg --yes --dearmor --output /usr/share/keyrings/xlion-repo.gpg
```

### Add apt source
#### For Ubuntu 24 / Debian 12 or latter (Deb822 style format)

```bash
sudo tee /etc/apt/sources.list.d/xlion-rustdesk-repo.sources << EOF
# Two channels available: latest, nightly.
# Switch by edit the string within URIs.

Types: deb
URIs: https://rustdesk-apt-repo.xlion.dev/latest
Suites: main
Components: main
Signed-By: /usr/share/keyrings/xlion-repo.gpg
EOF
```

#### For older version

```bash
sudo tee /etc/apt/sources.list.d/xlion-rustdesk-repo.list << EOF
# Two channels available: latest, nightly.
# Switch by edit the string within URIs.

deb [signed-by=/usr/share/keyrings/xlion-repo.gpg] https://rustdesk-apt-repo.xlion.dev/latest main main
EOF
```
