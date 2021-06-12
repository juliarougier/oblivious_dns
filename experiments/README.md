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

First, I tried to do simples requests with different famous domain names with the AAAA record type 
<img width="1194" alt="Capture d’écran 2021-06-12 à 17 33 35" src="https://user-images.githubusercontent.com/72855563/121781721-68e85b80-cba6-11eb-8cfa-12fa7257da00.png">
<img width="1194" alt="Capture d’écran 2021-06-12 à 17 34 02" src="https://user-images.githubusercontent.com/72855563/121781725-6a198880-cba6-11eb-83de-0588ca957a13.png">
<img width="1194" alt="Capture d’écran 2021-06-12 à 17 37 28" src="https://user-images.githubusercontent.com/72855563/121781727-6b4ab580-cba6-11eb-9ca6-b1570c90e9e5.png">
<img width="1194" alt="Capture d’écran 2021-06-12 à 17 40 08" src="https://user-images.githubusercontent.com/72855563/121781728-6c7be280-cba6-11eb-9992-42601f6cc164.png">
<img width="1194" alt="Capture d’écran 2021-06-12 à 17 46 53" src="https://user-images.githubusercontent.com/72855563/121781729-6c7be280-cba6-11eb-9167-8da67faa7b85.png">
<img width="1194" alt="Capture d’écran 2021-06-12 à 17 47 13" src="https://user-images.githubusercontent.com/72855563/121781730-6d147900-cba6-11eb-871b-3828f39629f4.png">



