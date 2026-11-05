# Okuma sırası

1. Dil temeli: [c-basvuru](https://github.com/mfguney/c-basvuru) **veya**
   [rust-basvuru](https://github.com/mfguney/rust-basvuru)
2. Bu rehber **A** — zihinsel model
3. **B** — ihtiyacınız olan karşılık tabloları
4. **C** — rewrite / bindgen / cbindgen / karışık
5. **D–E** — tuzaklar ve vakalar
6. **F** — masabaşı kartlar

Animasyonlu sayfalar: A/bellek, C/c-from-rust, E/dinamik-dizi.

## Kaynaklar

- Kardeş README’ler

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
