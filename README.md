# sniproxy-tutorial
Handle incoming port 80 HTTP and 443 HTTPS requests based on domain names.

![alt text](https://raw.githubusercontent.com/ran-sama/sniproxy-tutorial/master/overview.png)

## Why bother?
* you only have one port 80 and one port 443 per IP
* run as many servers as your hardware can handle on just these ports
* requests that did not include a domain-/hostname can be trashed
* is a transparent proxy and doesn't need your secret certs

## Install and configure

### Build chain A:
```
sudo apt install golang-go
```
For your "old" debian arm boxes like raspi and odroid. The "reference" implementation (available as golang-go) is the de-facto standard compiler. There is also ```gcc-go```, but I didn't use that.
### Alternative 1:
```
git clone --recursive https://github.com/inetaf/tcpproxy
cd tcpproxy/cmd/tlsrouter
go build .
```
1232 stars, 1 dependency, confirmed working, very easy config
### Alternative 2a:
```
git clone --recursive https://github.com/atenart/sniproxy/tree/archive/go
cd sniproxy/cmd/sniproxy
go build .
```
24 stars, 0 dependencies, confirmed working, also easy config
### Build chain B:
```
https://www.rust-lang.org/tools/install
```
The rust programming language installed via rustup from official site, default setup.  
Remember to put it on path as explained in terminal afterwards.
### Alternative 2b:
```
git clone --recursive https://github.com/atenart/sniproxy
cd sniproxy
cargo build --release
```
Same, but written in Rust.

## Honeypots for disconnecting bots

https://github.com/ran-sama/http-and-https-honeypot  

## License
Licensed under the WTFPL license.
