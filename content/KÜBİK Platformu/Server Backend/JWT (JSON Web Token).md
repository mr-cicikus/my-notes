
## JWT Nedir ve Ne İşe Yarar?

JWT (JSON Web Token), kullanıcının kimliğini kanıtlayan **dijital bir imzalı token**’dır. Kimlik doğrulama sonrasında istemciye verilir ve her istekte bu token ile kimlik sunulur. Bu sayede kullanıcı giriş yaptıktan sonra tekrar şifre girmez.


## `main.py` Dosyasında JWT'nin Rolü

- `/login` endpoint’i başarılı girişten sonra `create_access_token()` fonksiyonunu çağırarak bir JWT oluşturur.
    
- Bu token, içinde `user_id` gibi bilgilerle birlikte istemciye döner.
    
- FastAPI, korumalı rotalarda gelen `Authorization: Bearer <token>` başlığındaki JWT’yi kontrol eder.
  
  
## `jwt_utils.py` Dosyasında JWT'nin Rolü

Bu dosya JWT üretimi ve doğrulamasıyla ilgili iki temel işlevi barındırır:

### 1. `create_access_token(data: dict)`

- Gelen kullanıcı bilgilerini (örneğin `user_id`) alır.
    
- Bunları bir `exp` (expiration) süresiyle birleştirir.
    
- `HS256` algoritması ile imzalanmış bir JWT döner.
    

### 2. `decode_access_token(token: str)`

- Gelen JWT’yi çözümler.
    
- İmza geçerliyse payload verilerini döner (`user_id`, `exp`, vs.).
    
- Token hatalıysa `None` döner.
  


## `main.dart` Dosyasında JWT'nin Rolü

### Giriş Anında (`login()` içinde):

- Backend’den dönen JWT, `SharedPreferences` ile cihazda yerel olarak saklanır:
  
```dart
  await prefs.setString('jwt_token', token);
```

### Korunan Rotalara Erişim:

- Uygulama `SharedPreferences`’tan token'ı çeker.
    
- HTTP isteklerinde `Authorization` başlığına eklenerek gönderilir:

```dart
	headers: { "Authorization": "Bearer $token" }
```

Bu sayede kullanıcı yeniden giriş yapmadan sunucuya doğrulanmış istekler yapabilir.
