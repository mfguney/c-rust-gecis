# Thread-safe sayaç

## C

```c
#include <stdatomic.h>
atomic_long c = 0;
atomic_fetch_add_explicit(&c, 1, memory_order_relaxed);
```

## Rust

```rust
use std::sync::atomic::{AtomicI64, Ordering};
static C: AtomicI64 = AtomicI64::new(0);
C.fetch_add(1, Ordering::Relaxed);
```

Anlamlar benzer; Rust’ta `AtomicI64: Sync` paylaşımı türe gömülüdür.
Yanlış `Ordering` her iki dilde de ince bug üretir.

## Kaynaklar

- C `<stdatomic.h>`; `std::sync::atomic`

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
