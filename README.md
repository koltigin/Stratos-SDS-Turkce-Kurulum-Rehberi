# SDS
![image](https://user-images.githubusercontent.com/102043225/181995321-e90e0991-3154-4d74-a009-9326ea357ba3.png)

Stratos Merkezi Olmayan Depolama (SDS) ağı, veri trafiği tarafından yönlendirilen, ölçeklenebilir, güvenilir, kendi kendini dengeleyen esnek bir hızlandırma ağıdır. Verilere verimli ve güvenli bir şekilde erişir. Kullanıcı, boyutu ve türü ne olursa olsun herhangi bir veriyi saklama esnekliğine sahiptir.

SDS, verileri depolayan birçok kaynak düğümünden (PP düğümleri olarak da adlandırılır) ve her şeyi koordine eden birkaç meta düğümden (dizin oluşturma veya SP düğümleri olarak da adlandırılır) oluşur.
Geçerli depo, yalnızca kaynak düğümlerinin kodunu içerir. Meta düğümler hakkında daha fazla bilgi için, hazır olduğunda kaynağı açacağız.

Burada, bir SDS kaynak düğümünün kurulmasına ve çalıştırılmasına yardımcı olacak kısa bir hızlı başlangıç kılavuzu sunuyoruz. SDS ve Tropos-Incentive-Testnet ödül dağıtımı hakkında daha fazla bilgi için lütfen [Tropos Incentive Testnet](https://github.com/stratosnet/sds/wiki/Tropos-Incentive-Testnet) sayfasına bakın.

# Stratos Tropos-4 Kurulum Rehberi 

##  Sistem Gereksinimleri
* 4vCPU
* 8GB RAM
* 200GB SSD

## Root Yetkisi Alma Ve Root Dizinine Geçme 
```shell
sudo su
cd /root
```

## Sistemi Güncelleme
* 👉 Bu Adımı Tropos-4 Node'u ile Aynı Sunucuya Kuranlar Atlayabilir 👈
```shell
apt update && apt upgrade -y
```

## Gerekli Kütüphanelerin Kurulması
* 👉 Bu Adımı Tropos-4 Node'u ile Aynı Sunucuya Kuranlar Atlayabilir 👈
```shell
apt install make clang pkg-config libssl-dev build-essential git jq ncdu bsdmainutils htop screen -y < "/dev/null"
```
## Go Kurulumu 
* 👉 Bu Adımı Tropos-4 Node'u ile Aynı Sunucuya Kuranlar Atlayabilir 👈
```shell
ver="1.18.4"
wget "https://golang.org/dl/go$ver.linux-amd64.tar.gz"
rm -rf /usr/local/go
tar -C /usr/local -xzf "go$ver.linux-amd64.tar.gz"
rm -rf "go$ver.linux-amd64.tar.gz"
echo 'export GOROOT=/usr/local/go' >> $HOME/.bash_profile
echo 'export GOPATH=$HOME/go' >> $HOME/.bash_profile
echo 'export GO111MODULE=on' >> $HOME/.bash_profile
echo 'export PATH=$PATH:/usr/local/go/bin:$HOME/go/bin' >> $HOME/.bash_profile
source $HOME/.bash_profile
go version
```

## Stratos SDS Kurulumu
```shell
cd $HOME
git clone https://github.com/stratosnet/sds.git
cd sds
git checkout v0.8.1
make build
cp target/ppd $HOME/bin
make install
```

## Node Dosyası Oluşturma
```shell
cd $HOME
mkdir rsnode
cd rsnode
ppd config -w -p
```

## Config Dosyasında Düzenleme Yapma
Dosya içerisine giriyoruz.
```shell
nano $HOME/rsnode/configs/config.toml
```
Sırasıyla şunları yapalım;
* `network_address` bölümüne node ip adresimizi yazaıyoruz.
* `p2p_address`, `p2p_password`, `wallet_address` ve `wallet_password` bölümünü not edip kaydediyoruz.
* `chain_id` kısmı `tropos-4` olmalı öyle değilse düzeltiyoruz.
* `stratos_chain_url` bölümüne bu adresi 👉 `https://rest-tropos.thestratos.org:443` ekliyoruz.
* `version` bölümü `v0.8.1` olmalı.
* ` [[sp_list]]` bölümünü silip aşağıdakileri ekliyoruz;
```shell
[[sp_list]]
p2p_address = 'stsds1mr668mxu0lyfysypq88sffurm5skwjvjgxu2xt'
p2p_public_key = 'stsdspub1zcjduepq4v8yu6nzem787nfnwvzrfvpc5f7thktsqjts6xp4cy4a2j4rgm7sgdy4zy'
network_address = '35.73.160.68:8888'
[[sp_list]]
p2p_address = 'stsds1ftcvm2h9rjtzlwauxmr67hd5r4hpxqucjawpz6'
p2p_public_key = 'tsdspub1zcjduepqq9rk5zwkzfnnszt5tqg524meeqd9zts0jrjtqk2ly2swm5phlc2qtrcgys'
network_address = '46.51.251.196:8888'
[[sp_list]]
p2p_address = 'stsds12uufhp4wunhy2n8y5p07xsvy9htnp6zjr40tuw'
p2p_public_key = 'stsdspub1zcjduepqkst98p2642fv8eh8297ppx7xuzu7qjz67s9hjjhxjxs834md7e0s5rm3lf'
network_address = '18.130.202.53:8888'
[[sp_list]]
p2p_address = 'stsds1wy6xupax33qksaguga60wcmxpk6uetxt3h5e3e'
p2p_public_key = 'stsdspub1zcjduepqyyfl7ljwc68jh2kuaqmy84hawfkak4fl2sjlpf8t3dd00ed2eqeqlm65ar'
network_address = '35.74.33.155:8888'
[[sp_list]]
p2p_address = 'stsds1nds6cwl67pp7w4sa5ng5c4a5af9hsjknpcymxn'
p2p_public_key = 'stsdspub1zcjduepq6mz8w7dygzrsarhh76tnpz0hkqdq44u7usvtnt2qd9qgp8hs8wssl6ye0g'
network_address = '52.13.28.64:8888'
[[sp_list]]
p2p_address = 'stsds1403qtm2t7xscav9vd3vhu0anfh9cg2dl6zx2wg'
p2p_public_key = 'stsdspub1zcjduepqzarvtl2ulqzw3t42dcxeryvlj6yf80jjchvsr3s8ljsn7c25y3hq2fv5qv'
network_address = '3.9.152.251:8888'
[[sp_list]]
p2p_address = 'stsds1hv3qmnujlrug00frk86zxr0q23rnqcaquh62j2'
p2p_public_key = 'stsdspub1zcjduepqj69eeq07yfdgu4cdlupvga897zjqjakuru0qar5na7as4kjr7jgs0k7aln'
network_address = '18.223.175.117:8888'
```

* CTRL X, Y ve Enter diyip dosyayı kaydedip çıkıyoruz.

## Faucet / Token Alma
`CUZDAN_ADRESINIZ` bölümünü değiştirmeyi unutmayın.
```shell
curl --header "Content-Type: application/json" --request POST --data '{"denom":"ustos","address":"CUZDAN_ADRESINIZ"} ' https://faucet-tropos.thestratos.org/credit
```

## TMUX Kurulumu
```shell
apt-get install tmux
```

## TMUX Oturum Açma
```shell
tmux new-session -s sds
```

## SDS Node'u Başlatma
```shell
cd ~/rsnode
ppd start
```

## SDS Node'u Başlatma
```shell
cd ~/rsnode
ppd start
```

Aşağıdaki gibi bir çıktı aldıysanız sorun yoktur;
```shell

```

## Kaynak Node İçinde Terminal Açma

```shell
screen -S terminal
cd ~/rsnode
ppd terminal
```

## Register Peer Ekleme
```shell
registerpeer
```

## Aktivasyon
```shell
activate 9000000000 10000 1000000
```

## Node Durumuna Bakma
```shell
status
```

## Ozone Alma
```shell
prepay 1000000000 10000 600000
```

## Cüzdan Kontrolü
```shell
getoz CUZDAN_ADRESINIZ
```

## upload Klasörü Oluşturma
Önce `upload` adında screen açıyoruz.
```shell
screen -S upload
```
Sonra klasör açıp `upload.sh` dosyasını açıyoruz;
```shell
mkdir -p ~/upload
nano $HOME/rsnode/upload.sh
```

Dosyanın içerisine aşağıdaki kodları giriyoruz.
```shell
#!/bin/bash
while true;
do /usr/bin/head -c 25M /dev/urandom > "$HOME/upload/test-$(date '+%Y%m%d%H%M')" ; ppd terminal exec put "$HOME/upload/test-$(date '+%Y%m%d%H%M')";
sleep 900;
/usr/bin/rm -rf "$HOME/upload/test*";
sleep 1;
done
```

Dosyaya yetki veriyoruz;
```shell
cd $HOME/rsnode
chmod +x upload.sh 
./upload.sh
```


## Kazanılan Ödülleri Kontrol Etme

`https://rest-tropos.thestratos.org/pot/rewards/wallet/CUZDAN_ADRESINIZ` adresini tarayıcımızda açıyoruz. Ödüllerin yansıması zaman alır. günlük olarak kontrol edebilirsiniz.

## DAHA FAZLA SORUNUZ VARSA STRATOS TÜRKİYE TELEGRAM GRUBU
[Stratos Türkiye Telegram Sayfası](https://t.me/StratosTurkish)

##  FAYDALI KOMUTLAR

### Cüzdanı Görmek
```shell
wallets
```

### Ozone Almak
```shell
prepay 500000000 10000 1000000
```

### Ozone Miktarına Bakmak
```shell
getoz CUZDAN_ADRESINIZ
```

### Mining'in Suspend / Offline Sorununu Çözme
```shell
updateStake 1000000000 10000 1000000 1
```

# License

Copyright 2021 Stratos

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the [License](http://www.apache.org/licenses/LICENSE-2.0)

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.
