
## Docker Volumes for Java Devs: Hands-On

CONTAINERLAR DOGAR, BUYUR VE OLUR. E OLDUKLERINDE BEYINLERINDEKI BILGILERI BIR YERE YEDEKLEMEMIZ GEREKIYOR; BURADA DA DEVREYE VOLUMELER GIRIYOR.



    - Harici bir disk alanına sahip değilseniz veya harici tutulan bir veritabanına kayıt yapılmıyorsa veriler kaybolur. 
    - Container yaşam süresinden daha uzun saklanması gereken verileriniz varsa bunları container içinde tutmayız. Bunun için Volume ‘ler kullanılır.

* Volume ‘leri container dışında tutmamız ve her yeni container ile
ilintilendirmemiz(mount), paylaşılabilir ve erişilebilir yapmamız gerekir.

## Volume Yapısı

* Docker Volume ‘ler aynen container ve image gibi docker objeleridir.

* Aynen container oluşturur gibi oluşturulur.

* Varsayılan olarak docker deamon veya engine çalıştığı host makine üzerinde oluşturulurlar.

## Volume Nasıl Çalışır?

* `/app` klasörüne yazılmış herbir dosya abc volumüne yazılsın ama sen container içindeki app klasörüne yazılmış bir dosya olarak gör ve kullan, şeklindeki bir mantıkla çalışmaktadır.

## Volume Nasıl Oluşturulur?

* Yeni bir volume oluşturmak için;

```bash
$ docker volume create myfirstvolume

# Volume'leri gorebilmek icin
docker volume ls

```
* Özelliklerini ayrıntılı olarak görebilmek için;
```bash
$ docker volume inspect myfirstvolume


# Sonucu
[
    {
        "CreatedAt": "2022-04-07T00:49:06Z",
        "Driver": "local",
        "Labels": {},
        "Mountpoint": "/var/lib/docker/volumes/birincivolume/_data", # Burada mountpoint altında volume içeriğinin saklandığı görülür ancak Docker Desktop VM üzerinde koştuğundan bunu direkt görmek biraz farklıdır. Ama Linux makinede bunu direkt makinenin dosya sistemi üzerinde görebilirsiniz.(https://library.netapp.com/ecmdocs/ECMP1217281/html/GUID-C6537E25-1E71-40F8-A1AF-F0DEED4C865D.html#:~:text=A%20volume%20mount%20point%20is,26%2Ddrive%2Dletter%20limitation.)
        "Name": "birincivolume",
        "Options": {},
        "Scope": "local" # means Volumes are stored in a part of the host filesystem which is managed by Docker 
    }
]
```
* Burada;
```bash
{

“Driver” : “local”

“Mountpoint” : “/var/lib/docker…”

…

}

```

* Genel kullanımı => `docker run -v <volume_name>:<container-içindeki klasör-adı> image_name ...`
Şeklindedir.

#### Volume mount edilen ilk container ‘ı oluşturmak için

* Burada tam olarak napacagiz? Bir container'in icerisine directory(klasor), sonrasinda bir txt dosyasi olusturacagiz. Sonrasinda volume'leme yapacagiz. Son olarak container'i silince icinde olusturdugumuz dosya da silinmis mi silinmemis mi onu kontrol edecegiz.

```bash
$ docker run -it -v myfirstvolume:/containerVolume alpine sh
# app klasoru mock klasor; volume'lerde degil container'larda gorunur.
# Volume'un icerisindeyiz, devam..
pwd
ls
```

* Şimdi bir `/app` klasörü altında `abc.txt` isimli bir dosya oluşturalım. Bunun için;

```bash
# Volume'un icerisindeyiz, devam..
cd /app

touch abc.txt

ls

# Bu dosyaya bir veri girelim;
# Volume'un icerisindeyiz, devam..
echo “This line is added from the first container” >> abc.txt
cat abc.txt # Saglama yapmak icin
ls && exit
```
* Dolayısıyla container kapandı veya stop konumuna geçti. Bunu görebilmek için;

```bash
$ docker ps -a

# veya

$ docker container ls -a
```
* Bu container <ID> ile silmek için;

```bash
# Ben hepsini sileyim istiyorum
$ docker container prune
```
* Şimdi volumü bağladığımız bu container tamamen silindi! Böylece container yaşam süresi sona erdiği için içindeki dosyalarda silindi. 
* Bize gerekli olan oluşturduğumuz dosyaya erişmek için volume varlığını kontrol edelim.

* Bunun için;
```bash
$ docker volume ls
```
* **Dolayısıyla container silinince volume ‘de beraberinde silinmez. Volume ‘ler container‘lardan bağımsız ve ayrı objelerdir.**

* Volume'ler Container ‘larla bağımsız bir varlığa sahiptirler.

* Şimdi yeni bir container oluşturalım ve volume içindeki dosyamızın varlığını kontrol edelim. Bunun için;

```bash
$ docker run -it -v myfirstvolume:/containerVolume busybox sh
# bir ubuntu makina da çalıştırabiliz dilersek
# docker run -it -v firstvolume:/containerVolume ubuntu bash
# myVolume klasoru mock klasor
# Volume'un icerisindeyiz suan
```
* Volume bağladığımız klasörün varlığını kontrol edelim. Bunun için;
```bash
# Volume'un icerisindeyiz, devam..
pwd
ls

…

cd /myVolume

ls

…

cat abc.txt

The line is add from the first container

exit
```

* Böylece container yaşam süresinden fazla bir süre için dosylarımıza erişebiliyoruz. İşte volume bize tam da bunu sağlamaktadır.

* Yani gerekli verilerimizi ve dosyalarımızı container dışında tutmamızı sağlar.

--------------------------------------------------------------
