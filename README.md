# Kendi Laravel Kütüphaneni Oluştur!

## BİLGİLENDİRME

Herkese merhaba. Bu projede kendinize ait laravel kütüphanesi nasıl oluşturabilirsiniz bundan bahsedeceğim. Uygulaması gayet basittir.

## ADIM 1: Kütüphane Dosyası Oluşturma

Öncelikle bir klasör oluşturuyoruz ve terminal kullanımı ile bu klasörün içerisine giriyoruz. Ve terminalde çalıştırmamız gereken kod

```bash
composer init
```
bu komutu çalıştırdıktan sonra bize bir takım ayarlar sunacaktır. Bunlardan bazılarını sizlerle paylaşıp önerilen ayarları göstereceğim.
**Package name(Projenizin ismi)** - isim/proje şeklinde isimlendirmenizi öneririm.
**Description(Açıklama)** - Kütüphanenin açıklamasını yapabilirsiniz.
**Author(Yazar)** - Kütüphaneyi yazan kişinin adı burada kendi adınızı veya geliştiricinin adını yazabilirsiniz.
**Minimum Stability(Proje Sürümü)** - bu kısımda kütüphanenin sürümle alakalı şekillendirmesini ayarlıyoruz "dev" değerini kullanabilirsiniz
**Package Type(Paket Türü)** - bu kısımda yazdığınız kod bir kütüphane mi yoksa daha çok projenin bir parçasını mı oluşturuyor bunu ayarlayabilirsiniz
**License(Lisans Türü)** - MIT kullanabilirsiniz 

Add PSR-4 autoload mapping? Maps namespace sorusuna geldiğinizde ise bu kısımda src/ ile yazmanızı önerir bu src adlı bir klasör oluşturur ve dosyalarınızı bu alanda yönetmenizi sağlar bunu kendinize göre düzenleyebilirsiniz.

Bu adımları izledikten sonra klasörünüzün içerisine dosyaları oluşturacaktır.

## ADIM 2: Örnek Dosya Oluşturma

Dosyalarımız oluştuktan sonra örnek olması amacıyla bu kütüphaneyi yükleyen birinin view dosyasına deneme.blade.php adlı bir dosya gelmesini istiyorum. "src/path/to"  adlı klasörümüzün içerisine oluşmasını istediğimiz dosyayı oluşturuyoruz örneğin **deneme.blade.php** dosyası oluşturup içerisini dolduruyorum.

```bash
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Deneme Sayfası</title>
</head>
<body>
    <h1>Bu bir deneme sayfasıdır!</h1>
</body>
</html>
```

## ADIM 3: Service Provider ile Dosyayı Yayınlama

"src" adlı klasörümüzün içerisine **ProjectServiceProvider.php** adlı dosyamızı oluşturuyoruz bu dosya kütüphanemizdeki dosyalarım kurulumunu tamamlayacak dosya oluyor. Akabinde içerisini şu şekilde dolduruyoruz.

```bash
namespace Ilimdeniztoprak\LaravelMyPackage;

use Illuminate\Support\ServiceProvider;

class ProjectServiceProvider extends ServiceProvider
{
    public function boot()
    {
        $this->publishes([
            __DIR__.'/path/to/deneme.blade.php' => resource_path('views/deneme.blade.php'),
        ]);
    }

    public function register()
    {
        //
    }
}
```
**Gerekli alanları kendinize göre düzenlemeyi unutmayın!!**

## ADIM 4: GitHub Üzerinde Yayınlama

Bu aşamada yaptığımız bu dosyaları github repository üzerinde yayınlamamız gerekiyor. **UNUTMAYIN!!** repository Public durumunda olması önemlidir yoksa sadece kendiniz ulaşabilirsiniz. Yayınladıktan sonra bir sonraki ve son adımımıza geçiyoruz.

## ADIM 5: Packagist Üzerinde Yayınlama

Bu adımda Packagist üzerinde GitHubda yayınladığımız Repo'nun linkini belirtmeliyiz. Üyelik oluşturduktan sonra Submit adlı alana, bu kütüphanenin GitHub linkini koyuyoruz ve yayına alıyoruz. Bu adımdan sonra laravel projenizde çalıştırmanız gereken komut;

```bash
composer require kutuphane/adi
```

buarada kutuphane/adi adlı alanda yazmanız gereken bilgiyi oluşan composer.json dosyasının en üstünde yer alan "name" alanında bulabilirsiniz. Küütphane kurulumu tamamlandıktan sonra blade dosyasını oluşturmak için 

```bash
vendor:publish --provider="Ilimdeniztoprak\LaravelMyPackage\ProjectServiceProvider"
```
şeklinde kullanabilirsiniz. Gerekli yerleri kendinize göre düzenlemeyi unutmayın. İyi çalışmalar.

