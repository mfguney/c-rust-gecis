# Giriş

Bu rehber **üçüncü kitap**tır: C ve Rust başvurularını köprüler. Amaç sözdizimi
eşlemesi değil; **zihinsel model**, **ownership sözleşmeleri** ve **idiomatik
dönüşümler**.

## Kardeş kitaplar

- [c-basvuru](https://github.com/mfguney/c-basvuru) — dil, bellek, UB, ABI
- [rust-basvuru](https://github.com/mfguney/rust-basvuru) — ownership, traits, unsafe

## Kim için hangi yol?

| Profil | Önerilen sıra |
|--------|----------------|
| C biliyor → Rust | A → B → C (rewrite veya FFI) → D |
| Rust biliyor → C/FFI | A (UB) → B (layout/string) → C (cbindgen) |
| Karışık kod tabanı | C (karışık) + E (vakalar) + F (kartlar) |

## Bu rehberin vaadi

1. Aynı problemi iki modelde göstermek (animasyonlar)
2. “Kim free eder?” sorusunu tip ve API’ye gömmek
3. Incremental migration için kontrol listeleri

## Kaynaklar

- [Nomicon — FFI](https://doc.rust-lang.org/nomicon/ffi.html)
- cppreference C
- bindgen / cbindgen kullanıcı kılavuzları

## Derinleşme: pratik notlar

Bu bölümün yüzeysel kalmaması için aşağıdaki kontrol listesini uygulayın:

1. Küçük, derlenebilir bir örnek yazın ve çalıştırın.
2. Bilerek kırık bir varyant üretip derleyici/sanitizer mesajını okuyun.
3. Kardeş kitaptaki ilgili bölüme çapraz referans ekleyin (C ↔ Rust).
4. “Sık tuzaklar” listesine kendi bulduğunuz bir vakayı ekleyin (PR).

## Sık tuzaklar

- Sözleşmeyi dokümante etmeden işaretçi/ödünç paylaşmak
- Hata yolunda kaynak sızıntısı veya kısmi init
- Platforma özel davranışı evrensel sanmak
- Optimizasyon açıkken kaybolan “şans eseri çalışan” kod

## Alıştırmalar

1. Bu bölümdeki ana örneği `examples/` altına tam proje olarak taşıyın.
2. Bir birim test veya sanitizer komutu ekleyin.
3. Bölüm sonu kaynakçasındaki en az bir belgeyi okuyup buraya bir cümlelik not düşün.

## Daha fazla okuma

Resmi belgeler (The Book, Reference, Nomicon, cppreference, man sayfaları) bu
konunun normatif kaynağıdır. Bu kitap özgün Türkçe derlemedir; çelişkide resmi
metne bakın.
