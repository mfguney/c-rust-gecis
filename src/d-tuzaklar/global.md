# Global mutable state

## C’de neden yaygın?

Gizli bağlam: logger, config, errno benzeri thread-local… Küçük programlarda
kolay; büyük sistemlerde test edilemezlik ve yarış üretir.

```c
static int g_ready;
void set_ready(int v) { g_ready = v; } /* thread-safe değil */
```

## Rust alternatifleri

### OnceLock

```rust
use std::sync::OnceLock;
static CONFIG: OnceLock<String> = OnceLock::new();
fn config() -> &'static str {
    CONFIG.get_or_init(|| std::env::var("CFG").unwrap_or_default()).as_str()
}
```

### Mutex / Atomic

Paylaşılan sayaç veya durum için.

### Dependency injection

En idiomatik: durumu parametre olarak geçin; global’e ihtiyaç azalır.

## static mut

```rust
static mut COUNTER: i32 = 0; // kaçının
```

Her erişim `unsafe`; data race UB. Neredeyse her zaman daha iyi seçenek vardır.

## Alıştırmalar

1. Global config’i `OnceLock` ile yazın.
2. Aynı config’i fonksiyona parametre olarak taşıyıp testi kolaylaştırın.

## Kaynaklar

- `std::sync::OnceLock`
- Book — global variables tartışmaları
