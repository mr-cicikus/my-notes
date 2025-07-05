
![[KÜBİK İşleyiş Şeması.png]]

Bu şemada görüldüğü gibi, frontend'te yer alacak `main.dart` dosyası, uygulamanın backend ile iletişime geçmesini sağlayan en önemli parçadır. Frontend kodunun çoğu da `main.dart`'ta yer alır.

Backend teorik olarak 4'ü Python, 2'si SQL olmak üzere 6 parçadan oluşmaktadır. Python tarafında FastAPI'yi başlatan, ve diğer her şeyi kontrol eden bir `main.py`, [[JWT (JSON Web Token)]]'i yöneten `jwt_utils.py`, ve PostgreSQL veri tabanlarını yöneten `initdb.py`. SQL tarafında ise sadece şifre hash'i ve hash sahibinde bağlayan `secure_key`'i saklayan bir "güvenlik veri tabanı" ile geri kalan her bilgiyi - kullanıcılar, kulüpler, etkinlikler vb. - içeren bir "ana veri tabanı".

Flutter frontend'imizdeki yapılacak her eylemin backend'ten geçmesini sağlamalıyız. Bunun için `main.py`'de FastAPI ile **API endpoint** kurmalıyız. 
Örnek olarak: http://127.0.0.1:8000/login, burada `/login` bir endpoint'tur. Bir kullanıcı [[Başlangıç Ekranı]]'nda giriş yapmak için **Giriş Yap** düğmesine bastığında Flutter (main.dart), `http` üzerinden `127.0.0.1:8000` adresinde çalışmakta olan main.py ile iletişime geçecek ve aynı şekilde yine `http` üzerinden yanıt alacaktır.

![[genel diagram.png]]