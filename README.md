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

## Cloudflare R2 test

Starting from 2024/10/15, this repo and [rustdesk-rpm-repo](https://github.com/xlionjuan/rustdesk-rpm-repo) will push to Cloudflare R2 every day, it **should not** charge any fees.

Because the free plan has Class A Operations 1 million requests / month, and 10GB storage / month.

Egress (data transfer to Internet) is free.

<https://developers.cloudflare.com/r2/pricing/>

<hr>

Lets's calc the total oprations if we run both APT and RPM repo everyday:

The total generated files excluding `*.repo`, `pubkey.gpg` and `index.html` is 116, let's overestimate it: 150

1 million = 1,000,000

I'm new to S3 or R2, I'm not sure how deleting caculated in oprations.

And let me overestimate again!:

1,000,000/(150\*31day\*5(overestimate)) = 21.5 Still have left! 