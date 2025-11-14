# Sigortacılık CRM SaaS Uygulaması

Modern ve güçlü bir Sigortacılık Müşteri İlişkileri Yönetimi (CRM) uygulaması. Laravel 12.38.1 framework'ü kullanılarak geliştirilmiştir.

## 📋 İçindekiler

- [Sistem Gereksinimleri](#sistem-gereksinimleri)
- [Yerel Kurulum](#yerel-kurulum)
- [Veritabanı Yapılandırması](#veritabanı-yapılandırması)
- [Hosting'e Kurulum](#hostinge-kurulum)
- [Yapılandırma](#yapılandırma)
- [Lisans](#lisans)

## 🖥️ Sistem Gereksinimleri

Uygulamayı çalıştırabilmek için aşağıdaki gereksinimlerin karşılanması gerekmektedir:

- **PHP:** 8.2 veya üzeri
- **Composer:** 2.0 veya üzeri
- **MySQL:** 5.7 veya üzeri / MariaDB 10.3 veya üzeri
- **Web Sunucusu:** Apache / Nginx
- **PHP Eklentileri:**
  - OpenSSL
  - PDO
  - Mbstring
  - Tokenizer
  - XML
  - Ctype
  - JSON
  - BCMath
  - Fileinfo

## 🚀 Yerel Kurulum

### Adım 1: Projeyi İndirin

```bash
git clone https://github.com/insurance-crm/Insurance_CRM_With_Laravel.git
cd Insurance_CRM_With_Laravel
```

### Adım 2: Composer Bağımlılıklarını Yükleyin

```bash
composer install
```

### Adım 3: Ortam Dosyasını Oluşturun

```bash
cp .env.example .env
```

### Adım 4: Uygulama Anahtarını Oluşturun

```bash
php artisan key:generate
```

### Adım 5: Veritabanı Ayarlarını Yapın

`.env` dosyasını açın ve aşağıdaki değerleri kendi veritabanı bilgilerinizle güncelleyin:

```env
DB_CONNECTION=mysql
DB_HOST=127.0.0.1
DB_PORT=3306
DB_DATABASE=insurance_crm
DB_USERNAME=root
DB_PASSWORD=your_password
```

### Adım 6: Veritabanını Oluşturun

MySQL veya phpMyAdmin üzerinden yeni bir veritabanı oluşturun:

```sql
CREATE DATABASE insurance_crm CHARACTER SET utf8mb4 COLLATE utf8mb4_unicode_ci;
```

### Adım 7: Migrasyonları Çalıştırın

```bash
php artisan migrate
```

### Adım 8: Depolama Bağlantısını Oluşturun

```bash
php artisan storage:link
```

### Adım 9: Uygulamayı Başlatın

```bash
php artisan serve
```

Tarayıcınızda `http://localhost:8000` adresine giderek uygulamayı görebilirsiniz.

## 🗄️ Veritabanı Yapılandırması

### MySQL Veritabanı Oluşturma (Detaylı)

#### Yöntem 1: Komut Satırı ile

```bash
# MySQL'e bağlanın
mysql -u root -p

# Veritabanını oluşturun
CREATE DATABASE insurance_crm CHARACTER SET utf8mb4 COLLATE utf8mb4_unicode_ci;

# Kullanıcı oluşturun (opsiyonel ama önerilir)
CREATE USER 'insurance_user'@'localhost' IDENTIFIED BY 'güçlü_şifreniz';

# Yetkileri verin
GRANT ALL PRIVILEGES ON insurance_crm.* TO 'insurance_user'@'localhost';

# Yetkileri uygulayın
FLUSH PRIVILEGES;

# Çıkış yapın
EXIT;
```

#### Yöntem 2: phpMyAdmin ile

1. phpMyAdmin'e giriş yapın
2. "Veritabanları" sekmesine tıklayın
3. "Veritabanı oluştur" bölümüne `insurance_crm` yazın
4. Karakter seti: `utf8mb4_unicode_ci` seçin
5. "Oluştur" butonuna tıklayın

### .env Dosyası Veritabanı Ayarları

`.env` dosyanızı açın ve aşağıdaki ayarları yapın:

```env
# Uygulama Ayarları
APP_NAME="Sigortacılık CRM"
APP_ENV=production
APP_DEBUG=false
APP_URL=https://yourdomain.com

# Veritabanı Ayarları
DB_CONNECTION=mysql
DB_HOST=127.0.0.1
DB_PORT=3306
DB_DATABASE=insurance_crm
DB_USERNAME=insurance_user
DB_PASSWORD=güçlü_şifreniz
```

## 🌐 Hosting'e Kurulum

### Shared Hosting için Kurulum (cPanel)

#### Adım 1: Dosyaları Yükleyin

1. **FileZilla veya cPanel File Manager kullanarak:**
   - Tüm proje dosyalarını sunucuya yükleyin
   - Dosyaları `public_html` veya `www` dizininin **dışına** yükleyin
   - Örnek: `/home/kullaniciadi/laravel-app/`

#### Adım 2: Public Klasörünü Ayarlayın

İki seçeneğiniz var:

**Seçenek A: Subdomain Kullanımı (Önerilir)**
1. cPanel'de yeni bir subdomain oluşturun (örn: `app.yourdomain.com`)
2. Document Root'u `/home/kullaniciadi/laravel-app/public` olarak ayarlayın

**Seçenek B: Ana Domain'de Kullanım**
1. `public` klasörünün içeriğini `public_html`'e kopyalayın
2. `index.php` dosyasını düzenleyin ve yolları güncelleyin:

```php
// Eski
require __DIR__.'/../vendor/autoload.php';
$app = require_once __DIR__.'/../bootstrap/app.php';

// Yeni
require __DIR__.'/../laravel-app/vendor/autoload.php';
$app = require_once __DIR__.'/../laravel-app/bootstrap/app.php';
```

#### Adım 3: Veritabanı Oluşturun

1. cPanel'de **MySQL Databases** bölümüne gidin
2. Yeni veritabanı oluşturun (örn: `cpanel_insurance_crm`)
3. Yeni kullanıcı oluşturun
4. Kullanıcıyı veritabanına ekleyin ve tüm yetkileri verin
5. Veritabanı bilgilerini not edin

#### Adım 4: .env Dosyasını Yapılandırın

SSH veya File Manager ile `.env` dosyasını düzenleyin:

```bash
# .env.example dosyasını kopyalayın
cp .env.example .env
```

`.env` dosyasını açın ve düzenleyin:

```env
APP_NAME="Sigortacılık CRM"
APP_ENV=production
APP_DEBUG=false
APP_URL=https://yourdomain.com

DB_CONNECTION=mysql
DB_HOST=localhost
DB_PORT=3306
DB_DATABASE=cpanel_insurance_crm
DB_USERNAME=cpanel_dbuser
DB_PASSWORD=database_password
```

#### Adım 5: Composer ve Artisan Komutlarını Çalıştırın

SSH erişiminiz varsa:

```bash
# Proje dizinine gidin
cd /home/kullaniciadi/laravel-app

# Composer bağımlılıklarını yükleyin
composer install --optimize-autoloader --no-dev

# Uygulama anahtarını oluşturun
php artisan key:generate

# Cache'leri temizleyin
php artisan config:clear
php artisan cache:clear
php artisan view:clear
php artisan route:clear

# Yapılandırmaları cache'leyin (production için)
php artisan config:cache
php artisan route:cache
php artisan view:cache

# Migrasyonları çalıştırın
php artisan migrate --force

# Storage linkini oluşturun
php artisan storage:link
```

SSH erişiminiz yoksa, hosting sağlayıcınızın terminal veya PHP Artisan aracını kullanın.

#### Adım 6: Dosya İzinlerini Ayarlayın

```bash
# Storage ve bootstrap/cache klasörleri yazılabilir olmalı
chmod -R 775 storage
chmod -R 775 bootstrap/cache
chown -R kullaniciadi:kullaniciadi storage bootstrap/cache
```

#### Adım 7: .htaccess Dosyasını Kontrol Edin

`public/.htaccess` dosyasının mevcut olduğundan emin olun. Laravel ile birlikte gelir, ancak kontrol edin.

### VPS/Dedicated Server için Kurulum (Ubuntu/Debian)

#### Adım 1: Sunucu Hazırlığı

```bash
# Sistem güncellemesi
sudo apt update && sudo apt upgrade -y

# Gerekli paketleri yükleyin
sudo apt install -y nginx mysql-server php8.2-fpm php8.2-mysql php8.2-mbstring \
php8.2-xml php8.2-bcmath php8.2-curl php8.2-zip unzip git
```

#### Adım 2: Composer Kurulumu

```bash
curl -sS https://getcomposer.org/installer | php
sudo mv composer.phar /usr/local/bin/composer
```

#### Adım 3: MySQL Yapılandırması

```bash
# MySQL'i güvenli hale getirin
sudo mysql_secure_installation

# MySQL'e giriş yapın
sudo mysql

# Veritabanı ve kullanıcı oluşturun
CREATE DATABASE insurance_crm CHARACTER SET utf8mb4 COLLATE utf8mb4_unicode_ci;
CREATE USER 'insurance_user'@'localhost' IDENTIFIED BY 'güçlü_şifre';
GRANT ALL PRIVILEGES ON insurance_crm.* TO 'insurance_user'@'localhost';
FLUSH PRIVILEGES;
EXIT;
```

#### Adım 4: Projeyi Klonlayın

```bash
cd /var/www
sudo git clone https://github.com/insurance-crm/Insurance_CRM_With_Laravel.git
sudo mv Insurance_CRM_With_Laravel insurance-crm
cd insurance-crm
```

#### Adım 5: Bağımlılıkları Yükleyin ve Yapılandırın

```bash
sudo composer install --optimize-autoloader --no-dev
sudo cp .env.example .env
sudo php artisan key:generate

# .env dosyasını düzenleyin
sudo nano .env
```

#### Adım 6: İzinleri Ayarlayın

```bash
sudo chown -R www-data:www-data /var/www/insurance-crm
sudo chmod -R 775 /var/www/insurance-crm/storage
sudo chmod -R 775 /var/www/insurance-crm/bootstrap/cache
```

#### Adım 7: Nginx Yapılandırması

```bash
sudo nano /etc/nginx/sites-available/insurance-crm
```

Aşağıdaki yapılandırmayı ekleyin:

```nginx
server {
    listen 80;
    server_name yourdomain.com www.yourdomain.com;
    root /var/www/insurance-crm/public;

    add_header X-Frame-Options "SAMEORIGIN";
    add_header X-Content-Type-Options "nosniff";

    index index.php;

    charset utf-8;

    location / {
        try_files $uri $uri/ /index.php?$query_string;
    }

    location = /favicon.ico { access_log off; log_not_found off; }
    location = /robots.txt  { access_log off; log_not_found off; }

    error_page 404 /index.php;

    location ~ \.php$ {
        fastcgi_pass unix:/var/run/php/php8.2-fpm.sock;
        fastcgi_param SCRIPT_FILENAME $realpath_root$fastcgi_script_name;
        include fastcgi_params;
    }

    location ~ /\.(?!well-known).* {
        deny all;
    }
}
```

Site yapılandırmasını etkinleştirin:

```bash
sudo ln -s /etc/nginx/sites-available/insurance-crm /etc/nginx/sites-enabled/
sudo nginx -t
sudo systemctl restart nginx
```

#### Adım 8: SSL Sertifikası (Let's Encrypt)

```bash
sudo apt install certbot python3-certbot-nginx -y
sudo certbot --nginx -d yourdomain.com -d www.yourdomain.com
```

#### Adım 9: Migrasyonları Çalıştırın

```bash
cd /var/www/insurance-crm
sudo php artisan migrate --force
sudo php artisan storage:link
sudo php artisan config:cache
sudo php artisan route:cache
```

## ⚙️ Yapılandırma

### Ortam Değişkenleri

`.env` dosyasında yapılandırılması gereken önemli ayarlar:

```env
# Uygulama
APP_NAME="Sigortacılık CRM"
APP_ENV=production
APP_DEBUG=false
APP_URL=https://yourdomain.com

# Veritabanı
DB_CONNECTION=mysql
DB_HOST=127.0.0.1
DB_PORT=3306
DB_DATABASE=insurance_crm
DB_USERNAME=insurance_user
DB_PASSWORD=your_secure_password

# Mail Ayarları (isteğe bağlı)
MAIL_MAILER=smtp
MAIL_HOST=smtp.gmail.com
MAIL_PORT=587
MAIL_USERNAME=your_email@gmail.com
MAIL_PASSWORD=your_email_password
MAIL_ENCRYPTION=tls
MAIL_FROM_ADDRESS=noreply@yourdomain.com
MAIL_FROM_NAME="${APP_NAME}"
```

### Önbellek ve Optimizasyon

Production ortamında performansı artırmak için:

```bash
php artisan config:cache
php artisan route:cache
php artisan view:cache
php artisan optimize
```

Geliştirme sırasında önbellekleri temizlemek için:

```bash
php artisan config:clear
php artisan route:clear
php artisan view:clear
php artisan cache:clear
```

## 🔒 Güvenlik

- `.env` dosyasının asla versiyon kontrolüne eklenmediğinden emin olun
- Production ortamında `APP_DEBUG=false` olmalıdır
- Güçlü veritabanı şifreleri kullanın
- Düzenli olarak `composer update` yapın
- SSL sertifikası kullanın (HTTPS)
- Dosya izinlerini doğru ayarlayın (storage ve cache klasörleri 775)

## 📝 Lisans

Bu proje MIT lisansı altında lisanslanmıştır.

## 🆘 Destek

Herhangi bir sorun yaşarsanız, lütfen [GitHub Issues](https://github.com/insurance-crm/Insurance_CRM_With_Laravel/issues) üzerinden bildiriniz.
