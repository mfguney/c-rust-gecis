# Derleme birimi vs crate

## C

- `.c` → çeviri birimi; başlıklar metin include
- Bağlayıcı sembolleri birleştirir
- `static` iç bağlama; `inline` kuralları incelikli
- Build: Make/CMake + pkg-config

## Rust

- Crate = derleme birimi + paket sınırı
- Modüller dilde; `pub` görünürlük
- Cargo bağımlılık grafiği + semver
- Features ile koşullu derleme

## Sonuçlar

1. C’de “başlıkta tanım” tuzağı; Rust’ta monomorphization / `inline` farklı
2. Versiyonlama: soname vs semver
3. Karışık projede iki graphe (CMake + Cargo) yönetilir

## Kaynaklar

- Cargo Book
- C translation phases (cppreference)

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
