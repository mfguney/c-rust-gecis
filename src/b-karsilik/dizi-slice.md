# Dizi, slice, vektör

| C | Rust |
|---|------|
| `T a[N]` | `[T; N]` |
| `T *` + `n` | `&[T]` / `&mut [T]` |
| elle buffer | `Vec<T>` |
| `realloc` büyümesi | `Vec::push` / `reserve` |

## Sınır denetimi

Rust indeksi debug/release’de panik üretebilir; `get` → `Option`.
C’de sessiz taşma UB/zafiyet.

## Büyüme sırasında referanslar

Her iki dilde de buffer taşınınca eski işaretçiler/dilimler geçersiz.
Rust borrow checker çoğu bug’ı derlemede yakalar; C’de sanitizer.

## Kaynaklar

- Book ch.8; `man 3 realloc`

## Amortize büyüme

Kapasiteyi ×2 artırmak amortize O(1) `push` sağlar. Eski işaretçileri saklamayın;
indeks veya büyümeden sonra yeniden alın. Rust’ta borrow checker; C’de dikkat.


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
