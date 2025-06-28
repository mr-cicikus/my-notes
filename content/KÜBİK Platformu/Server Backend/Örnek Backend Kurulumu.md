
Örnek backend git ile yüklenebilir:

```
git clone https://github.com/Takim-Truva/backend_example.git
```

Backend'i yerel olarak test amaçlı çalıştırmak için ilk önce PiP'ten şu kütüphaneleri indirmek gerekir:

```pip
pip install uuid asyncpg pydantic datetime uvicorn asyncio 'python-jose\[cryptography]' 'pydantic\[email]' argon2-cffi binascii
```

> [!NOTE]
> Eğer error verilirse diğer kütüphanelerin yüklenmesi engel olunabilir, eksik kütüphaneler de olabilir. Tavsiyem teker teker denemek.

Daha sonra PostgreSQL'i yerel olarak çalıştırmak için onu ayrıca kurmak lazım:

- Windows Kurulumu: https://www.postgresql.org/download/windows/
- Kali Linux Kurulumu: https://labex.io/tutorials/kali-how-to-start-postgresql-in-kali-linux-417476

En sonunda, bir komut penceresi açıp şu komutları girmek gerek:

```
psql postgres
```

```
CREATE USER kubik_user WITH PASSWORD 'kubik_pass';
CREATE DATABASE kubik_main OWNER kubik_user;
CREATE DATABASE kubik_security OWNER kubik_user;
GRANT ALL PRIVILEGES ON DATABASE kubik_main TO kubik_user;
GRANT ALL PRIVILEGES ON DATABASE kubik_security TO kubik_user;
```

Ve ardından backend klasöründeki `initdb.py`'yi python ile çalıştırmak (bu tek bir sefer için gereklidir):
```
python initdb.py
```

Daha sonra, backend `python main.py` ile çalıştırılabilir. Veri tabanındaki tablolara manual giriş için şu komut bile kullanılabilir:

```
curl -X POST http://127.0.0.1:8000/register \
  -H "Content-Type: application/json" \
  -d '{
    "email": "cicikus@gmail.com",
    "user_name": "Cicikus",
    "user_surname": "Cici",
    "password": "birsifre123"
  }'

```
(bu, `/register` enpoint'ini kullanarak email, user_name, user_surname ve password verileriyle bir kullanıcı oluşturmaktadır)

```
curl -X POST http://127.0.0.1:8000/login \
  -H "Content-Type: application/json" \
  -d '{
    "email": "cicikus@gmail.com",
    "password": "birsifre123"
  }'
```
(bu, `/login` enpoint'ini kullanarak email ve password verileriyle kullanıcı girişini denemektedir)