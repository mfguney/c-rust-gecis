# goto cleanup → Drop

## C kalıbı

```c
int run(void) {
    A *a = NULL; B *b = NULL; int rc = -1;
    a = a_new(); if (!a) goto done;
    b = b_new(); if (!b) goto done;
    rc = work(a, b);
done:
    b_free(b);
    a_free(a);
    return rc;
}
```

Tek çıkış noktası kaynak sızıntısını azaltır; ama `goto` disiplini gerekir.

## Rust karşılığı

```rust
fn run() -> Result<(), Error> {
    let a = A::new()?;
    let b = B::new()?;
    work(&a, &b)?;
    Ok(())
} // a, b drop — sıra ters
```

Erken `?` dönüşlerinde bile `Drop` çalışır. Bu, C `goto cleanup`’ın dil düzeyinde
yerleşmiş hâlidir.

## İnce noktalar

- Drop sırasında panic → abort riski; `Drop` içinde paniklemeyin
- Kısmi init: alanları `Option` yapın veya builder kullanın
- FFI’dan alınan kaynak: `Drop`’ta `extern` free çağırın

## Alıştırmalar

1. Üç kaynaklı C cleanup’ı Rust’a çevirin.
2. Bilerek `Drop` içinde panic deneyip ne olduğunu görün (küçük örnek).

## Kaynaklar

- Book ownership / Drop
- C cleanup stili (Linux kernel tartışmaları)
