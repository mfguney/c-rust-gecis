# Enum modelleri

## C enum

Tamsayı sabitleri; veri taşımaz. Boyut/işaret IB olabilir.

## Rust enum

Etiketli birleşim — varyantlar veri taşır. C eşdeğeri:

```c
struct Deger {
    enum { INT, FLOAT } tag;
    union { int i; float f; } u;
};
```

## FFI

Düz C enum için:

```rust
#[repr(C)]
pub enum Color { Red = 1, Green = 2, Blue = 3 }
```

veya `#[repr(u32)]`. Veri taşıyan Rust enum’u C’ye “olduğu gibi” vermeyin —
düzleştirin veya opaque yapın.

## Kaynaklar

- Book ch.6; Nomicon

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
