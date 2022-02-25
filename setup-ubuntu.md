when setting up a new ubuntu machine:

Firstly

`apt update && apt update -y && reboot`

when it returns

```
apt install -y screen emacs-nox git python3 python3-pip python3-wheel nodejs postgresql-12 libpq-dev gcc g++ libssl-dev pkg-config openssl software-properties-common libgmp-dev libsecp256k1-dev python3-dev python-is-python3
useradd -s /bin/bash tezos
mkdir /home/tezos
cp -a /etc/skel/.[a-zA-Z]* /home/tezos
chown -R tezos:tezos /home/tezos
```
execute `visudo` and add the following line somewhere:
```
tezos ALL=NOPASSWD: ALL
```
and then perform the following:
```
su - tezos
mkdir -m 700 .ssh
cat > .ssh/authorized_keys
```
paste in your public keys
```
chmod 600 .ssh/authorized_keys

cat > .screenrc <<EOF
autodetach on 
startup_message off 
hardstatus alwayslastline 
shelltitle 'bash'

hardstatus string '%{gk}[%{wk}%?%-Lw%?%{=b kR}(%{W}%n*%f %t%?(%u)%?%{=b kR})%{= w}%?%+Lw%?%? %{g}][%{d}%l%{g}][ %{= w}%Y/%m/%d %0C:%s%a%{g} ]%{W}'
EOF

cat > .pgpass <<EOF
localhost:5432:*:tezos:tezos
EOF
chmod 600 .pgpass

curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh

sudo add-apt-repository ppa:serokell/tezos && sudo apt-get update
sudo apt-get install tezos-client

wget https://ligolang.org/bin/linux/ligo && sudo mv ligo /usr/local/bin && sudo chmod 755 /usr/local/bin/ligo

python3 -m pip install pytezos


```
