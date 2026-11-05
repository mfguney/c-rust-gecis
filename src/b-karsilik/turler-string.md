# Türler ve string’ler

## Skaler kabaca eşleme

| C | Rust |
|---|------|
| `int32_t` | `i32` |
| `size_t` | `usize` |
| `bool` / `_Bool` | `bool` |
| `void *` | `*mut ()` / `*mut c_void` |
| `T *` | `*mut T` / `*const T` / `&T` / `Option<&T>` |

İşaretli taşma: C UB (klasik); Rust debug panic / release wrapping — bilinçli API.

## String modelleri

| C | Rust |
|---|------|
| `char *` + null | `CStr` / `CString` |
| uzunluk + ptr | `&[u8]` / `&str` |
| sahip tampon | `String` / `Vec<u8>` |

```rust
use std::ffi::{CStr, CString};
let c = CString::new("merhaba").unwrap();
let p = c.as_ptr(); // *const c_char — c yaşarken
```

UTF-8: Rust `String` geçerli Unicode varsayar; C’den gelen baytları
`String::from_utf8` / `from_utf8_lossy` ile doğrulayın.

## Kaynaklar

- `std::ffi`
- cppreference string.h

## Metin ve sınırlar

Her zaman uzunluk taşıyın. C’de `snprintf`; Rust’ta `&str` / `String`.
FFI’da UTF-8 doğrulaması (`from_utf8`) unutulursa güven/doğruluk kırılır.


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
