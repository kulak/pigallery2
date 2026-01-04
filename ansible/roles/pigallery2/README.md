# README

The directory `pigallery2` contains an example ansible role that can be used to install PiGallery2 on Fedora 43 Linux distribution.

Reverse proxy is omitted.  Caddy is recommended for simplicity of certificate management.

Sample caddy file:

```caddy
# PiGallery2 https://github.com/bpatrik/pigallery2
YOUR_FQDN_HERE {
	reverse_proxy "127.0.0.1:{{pigallery_port}}"

	@acme {
		path /.well-known/acme-challenge/*
	}
	handle @acme

	# restrict to private network, https://caddyserver.com/docs/caddyfile/matchers#remote-ip
    # comment the following to make server accessible to anyone on internet
	@denied not remote_ip private_ranges
	abort @denied
}
```
