NixOS Mailz
===========

> Self-hosted email solution using NixOS.
>
> Proudly inspired by [Docker Mailz][docker-mailz].

[docker-mailz]: https://github.com/aimxhaisse/docker-mailz

Overview
--------

NixOS Mailz is a NixOS module to preconfigure OpenSMTPD, SpamAssassin
and Dovecot in perfect harmony with the bare minimum configuration
options.

It's either meant to be directly included in your NixOS configuration or
just to show an example of a working configuration of OpenSMTPD,
SpamAssassin and Dovecot on NixOS, from which you can find inspiration.

Usage
-----

### Encrypt your users' passwords

```sh
nix-shell -p opensmtpd --command 'smtpctl encrypt'
```

For each line you'll enter, the encrypted equivalent will be printed.

### NixOS configuration

```nix
{ config, pkgs, ... }:

{
  imports = [
    # ...
    /path/to/mailz
    # ...
  ];

  services.mailz = {
    domain = "example.com";

    users = {
      foo = {
        password = "encrypted";
        aliases = [ "postmaster" ];
      };
    };
  };
}
```
