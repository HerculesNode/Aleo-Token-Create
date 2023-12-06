## 🟢 Ön bilgi

Bu rehberde Aleo ile Token Oluşturmayı anlatacağım işlemleri ücretsiz Codespaces ile yapabilirsiniz.  <br><br>

Daha önce VPS üzerinde kurulum yaptıysanız aşağıdaki adımları tekrar yapmanıza gerek yoktur. Klasör oluşturalım bölümünden başlamanız yeterli.


 ### Linkler
 * [Hercules Telegram](https://t.me/HerculesNode)
 * [Hercules Twitter](https://twitter.com/HerculesNode)
 * [Aleo Dc](https://discord.gg/aleohq)


## 🟢 Sistem Kurulumu

```shell
cd
```

```shell
sudo su
```


```shell
#!/bin/bash
sudo apt update && sudo apt upgrade -y
sudo apt-get install git-all -y
sudo apt-get install curl -y
sudo su
```

#### Cargo kuralım : 

```shell
curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh
```
```shell
source "$HOME/.cargo/env"
```

## 🟢 Leo Dosyalarını çekelim

```shell
git clone https://github.com/AleoHQ/leo
```
```shell
cd leo
```
```shell
cargo install --path .
```

```shell
cd ..
```

## 🟢  üstteki güncellemeleri yaptıysanız buradan başlayalım

#### 1- Klasör oluşturalım

```shell
mkdir aleo_token_herculesnode && cd aleo_token_herculesnode
```

![image](https://github.com/HerculesNode/Aleo-Contract-Deploy/assets/101635385/16243d42-a49d-46b3-8519-d0902521f5b4)


#### 2- Cüzdan adresi girelim 

```shell
WALLETADDRESS=CÜZDANINIZIN-ADRESİ
```

![image](https://github.com/HerculesNode/Aleo-Contract-Deploy/assets/101635385/6828fcf1-901c-4b62-bbe0-ca5bf027e8d2)


#### 3- Program ismi oluşturacağız burası önemli hercules yazan yeri kendi istediğiniz bir isimle değiştirin !  Burası değişecek = herculestoken  , kendi isminizi yazın 

*Not isminizi 8 karakterden fazla yapın yoksa fee yüksek çıkar. !!! <br>

```shell
APPNAME=herculestoken
```

![image](https://github.com/HerculesNode/Aleo-Token-Create/assets/101635385/d408b62a-e9ff-4778-a462-960e7e155e4a)



#### 4- Leo test uygulaması oluşturalım  Buradaki çıktıyı not alalım kendi program ismimizi oluşturduk aşağıda kullanacağız önemli

```shell
leo new ${APPNAME}
```

![image](https://github.com/HerculesNode/Aleo-Token-Create/assets/101635385/2989b1ae-e62c-4f23-af4f-da3d47dc1c04)


#### 5- Leo uygulamasını başlatalım

```shell
cd ${APPNAME} && leo run && cd -
```

![image](https://github.com/HerculesNode/Aleo-Token-Create/assets/101635385/b840f235-e343-462a-9674-14458c06a639)


#### 6- Yolu kaydedelim

```shell
PATHTOAPP=$(realpath -q $APPNAME)
```

![image](https://github.com/HerculesNode/Aleo-Contract-Deploy/assets/101635385/24179275-b6e7-4b52-926a-5d5068a549e2)


<hr> 



## 🟢 Şimdi buraya kadar işlemleri bitirdik artık aleo SDK üzerinden devam edeceğiz. 

#### 1- Bu adrese Gidelim :  https://aleo.tools/develop

<br> 

Alt tarafta bulunan kodları Deploy Program bölümüne gelin ve oraya kopyalayın.  (  program herculestoken.aleo; herculestoken yazan yeri değiştirmeyi unutmayın )

<br> 3. adımda yazdığınız isim ile değiştirmeyi unutmayın.

```shell
program herculestoken.aleo;

record Token:
    owner as address.private;
    amount as u64.private;


function mint:
    input r0 as address.private;
    input r1 as u64.private;
    cast r0 r1 into r2 as Token.record;
    output r2 as Token.record;


function transfer:
    input r0 as Token.record;
    input r1 as address.private;
    input r2 as u64.private;
    sub r0.amount r2 into r3;
    cast r0.owner r3 into r4 as Token.record;
    cast r1 r2 into r5 as Token.record;
    output r4 as Token.record;
    output r5 as Token.record;
```


![image](https://github.com/HerculesNode/Aleo-Token-Create/assets/101635385/8de185f6-91f3-4e44-aad7-1552613ff15c)

#### 2- Deploy doğrulamaya bakalım.

Deploy yaptıktan sonra altında size bir tx verecek bunu explorer üzerinden kontrol edelim.  <br> 

Bu adresin sonuna verdiği tx numarasını yazın işlemler doğruysa resimdeki gibi görünecek :  https://explorer.aleo.org/transaction/TX-ADRESİNİ-YAZ

![image](https://github.com/HerculesNode/Aleo-Token-Create/assets/101635385/c2ffe4f9-4c0f-49ee-ab91-f1edcaf73f38)


#### 3- Token oluşturma adımını yapalım

Bu adrese girelim yine bu sefer en üstteki alanı kullanacağız Execute Program : https://aleo.tools/develop

1- Load Program  : token isminiz ne ise onu yazıp aratın <br>
2- Private Key : Cüzdan Private key yazın <br>
3-Execute On-Chain : buton açık olacak <br>
4-Fee : 3 yazın olmazsa arttırın <br> <br>

> Mint bölümü <br>
1-r0 : Cüzdan adresinizi yazın <br>
2-r1 : 2000u64  yazın ne kadar istiyorsanız rakamı değiştirin <br><br>

Run tuşuna basın  <br>



![image](https://github.com/HerculesNode/Aleo-Token-Create/assets/101635385/8d5e743d-8fa5-4a27-aed6-8da9bacde915)


#### 4- İşlem tamamlanırsa aşağıdaki gibi onay gelecek


Explorer üzerinden kontrol edin verdiği tx çıktısını aşağıdaki adreslerin sonuna ekleyerek kontrol edebilirsiniz. <br> 

https://explorer.hamp.app/transaction?id= <br>
https://explorer.aleo.org/transaction/ <br>

![image](https://github.com/HerculesNode/Aleo-Token-Create/assets/101635385/b1b07be8-b8fa-4f2f-b18b-e496c1fd3b41)




