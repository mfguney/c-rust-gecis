# Generics vs _Generic

## C tarafı

C’de aşırı yükleme yoktur. Yaklaşımlar:

1. **Makrolar** — metin; yan etki ve tür güvenliği zayıf
2. **`_Generic` (C11)** — derleme zamanı tür seçimi
3. **`void *` + boyut** — tip silme; hata çalışma zamanına kaçar
4. **Kod üretimi** (X-macro) — tekrarlayan fonksiyonlar

```c
#define MAX(a,b) _Generic((a), \
    int: max_int, \
    double: max_double \
)(a,b)
```

Sınır: açık tür listesi; trait bound yok; coherence yok.

## Rust tarafı

```rust
fn max<T: PartialOrd>(a: T, b: T) -> T {
    if a > b { a } else { b }
}
```

Monomorphization veya `dyn`. Orphan rule, associated types, GAT — C’de karşılığı
zayıf olan kavramlar.

## Geçiş stratejisi

C makro/`_Generic` ormanını birebir çevirmeyin. Önce:

1. Ortak davranışı trait olarak adlandırın
2. Somut türleri `impl` edin
3. Gerekirse `dyn` ile heterojen koleksiyon

## Alıştırmalar

1. C `_Generic` max’ını Rust generics’e çevirin.
2. Aynı API’yi `dyn` ile yazıp farkı ölçün.

## Kaynaklar

- Book ch.10
- cppreference `_Generic`
