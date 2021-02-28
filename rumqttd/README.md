# rumqttd

[![crates.io page](https://img.shields.io/crates/v/rumqttd.svg)](https://crates.io/crates/rumqttd)
[![docs.rs page](https://docs.rs/rumqttd/badge.svg)](https://docs.rs/rumqttd)

## `native-tls` support

This crate, by default uses the `tokio-rustls` crate. There's also support for the `tokio-native-tls` crate.
Add it to your Cargo.toml like so:

```
rumqttd = { version = "0.5", default-features = false, features = ["use-native-tls"] }
```

Then in your config file make sure that you use the `pkcs12` options for your cert instead of `cert_path`, `key_path`, etc.

```toml
[rumqtt.servers.1]
port = 8883
pkcs12_path = "/root/identity.pfx"
pkcs12_pass = ""
# cert_path = "/root/issued/test.crt"
# key_path = "/root/private/test.key"
# ca_path = "/root/ca.crt"
```

You can generate the `.p12`/`.pfx` file using `openssl`:

```
openssl pkcs12 -export -out identity.pfx -inkey ~/pki/private/test.key -in ~/pki/issued/test.crt -certfile ~/pki/ca.crt
```

Make sure if you use a password it matches the entry in `pkcs12_pass`. If no password, use an empty string `""`.