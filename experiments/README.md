# Oblivious DNS experiments 

The sources used for these experiments with ODoH come from these github: 
- https://github.com/cloudflare/odoh-rs (server Rust)
- https://github.com/cloudflare/odoh-client-rs/ (client Rust) 
- https://github.com/cloudflare/odoh-go (server Golang)
- https://github.com/cloudflare/odoh-client-go (client Golang)


# Rust code 

Before doing some ODoH requests, I had to install Rust with this link : https://www.rust-lang.org/tools/install. 

The following code allows to do a ODoH request : 

```sh
cargo run -- example.com <record type>
```

First, I tried to do simples requests with different domain names  
