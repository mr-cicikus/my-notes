---

---
- [ ] Uygulama başlangıcında [[JWT (JSON Web Token)]] ile otomatik giriş denemesi
- [ ] Giriş Yap Düğmesi, text kutuları ve /login endpoint'e bağlanması
- [ ] Kayıt Ol Düğmesi, text kutuları ve /register endpoint'e bağlanması
- [ ] Ekranın genel tasarımı (logo, yazı, renk vb.)
---
# 0. Uygulama Başlangıcı

Öncelikle Flutter'ın yerel deposu olan `SharedPreferences`'ta bir [[JWT (JSON Web Token)]] olup olmadığı kontrol edilmeli. Eğer var ise, JWT'nin geçerliliği sunucu tarafından kontrol edilir ve eğer geçerli ise giriş işlemi otomatik olarak tamamlanır.

Eğer geçerli bir JWT yok ise, uygulama başlangıç ekranına yönelmeli.

---
# 1. Başlangıç Ekranı

İki fonksiyon içermeli: Giriş Yap ve Kayıt Ol.

Başlangıç ekranında direkt olarak "Giriş Yap" başlığı altında 2 tane text kutucuğu sunulabilir.  

![[Screenshot 2025-06-22 at 13.23.59.png]]

### Giriş Yap Düğmesi

Giriş Yap düğmesine basıldıktan sonra, şöyle bir işlem gerçekleşmelidir:

![[Giriş Yap.png]]

...

### Kayıt Ol Düğmesi


