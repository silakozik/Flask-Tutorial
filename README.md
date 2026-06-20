# Task Master

Flask ve SQLAlchemy kullanılarak geliştirilmiş basit bir görev (to-do) yönetim uygulaması. Görev ekleyebilir, listeleyebilir, güncelleyebilir ve silebilirsiniz.

## Özellikler

- Yeni görev ekleme
- Tüm görevleri eklenme tarihine göre listeleme
- Mevcut görevi güncelleme
- Görev silme
- SQLite veritabanı ile kalıcı veri saklama

## Kullanılan Teknolojiler

- **Python 3**
- **Flask** – web çatısı (framework)
- **Flask-SQLAlchemy** – veritabanı (ORM) yönetimi
- **SQLite** – veritabanı
- **Jinja2** – HTML şablonları 

## Proje Yapısı

```
Flask-Tutorial/
├── app.py                  # Ana uygulama ve rotalar (routes)
├── instance/
│   └── test.db             # SQLite veritabanı dosyası
├── static/
│   └── css/
│       └── main.css        # Stil dosyası
├── templates/
│   ├── base.html           # Ana şablon (diğerleri bunu genişletir)
│   ├── index.html          # Görev listesi ve ekleme formu
│   └── update.html         # Görev güncelleme sayfası
└── venv/                   # Sanal ortam (virtual environment)
```

## Kurulum

### 1. Projeyi edinin

Projeyi indirin veya klonlayın ve klasöre girin:

```bash
cd c:\projects\Flask-Tutorial
```

### 2. Sanal ortamı oluşturun (henüz yoksa)

```bash
python -m venv venv
```

### 3. Sanal ortamı etkinleştirin

Windows için:

```bash
venv\Scripts\activate
```

Etkinleştiğinde satırın başında `(venv)` ifadesini görürsünüz.

### 4. Gerekli paketleri yükleyin

```bash
pip install flask flask-sqlalchemy
```

### 5. Veritabanını oluşturun

Veritabanı dosyası (`instance/test.db`) yoksa, Python yorumlayıcısını açıp tabloları oluşturun:

```bash
python
```

```python
>>> from app import app, db
>>> app.app_context().push()
>>> db.create_all()
>>> exit()
```

## Çalıştırma

```bash
python app.py
```

Ardından tarayıcıda şu adresi açın:

```
http://127.0.0.1:5000
```

Sunucuyu durdurmak için terminalde `CTRL + C` tuşlarına basın.

> Not: `debug=True` açık olduğu için kodda yaptığınız değişikliklerde sunucu otomatik olarak yeniden başlar.

## Rotalar (Routes)

| Yöntem      | Adres            | Açıklama                              |
| ----------- | ---------------- | ------------------------------------- |
| GET / POST  | `/`              | Görevleri listeler ve yeni görev ekler |
| GET         | `/delete/<id>`   | Belirtilen görevi siler               |
| GET / POST  | `/update/<id>`   | Belirtilen görevi günceller           |

## Veritabanı Modeli

`Todo` tablosu aşağıdaki alanlardan oluşur:

| Alan           | Tür      | Açıklama                          |
| -------------- | -------- | --------------------------------- |
| `id`           | Integer  | Birincil anahtar (otomatik artar) |
| `content`      | String   | Görev metni (zorunlu)             |
| `completed`    | Integer  | Tamamlanma durumu (varsayılan: 0) |
| `date_created` | DateTime | Oluşturulma tarihi (otomatik)     |
