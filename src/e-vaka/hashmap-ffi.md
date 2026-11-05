# Hash map FFI sarmalayıcı

C API: `map_create` / `map_insert` / `map_get` / `map_free`.
İçeride Rust `HashMap`; dışarıda opaque pointer.

```rust
pub struct Map(std::collections::HashMap<u32, u32>);

#[no_mangle]
pub extern "C" fn map_create() -> *mut Map {
    Box::into_raw(Box::new(Map(Default::default())))
}

#[no_mangle]
pub unsafe extern "C" fn map_insert(p: *mut Map, k: u32, v: u32) -> i32 {
    if p.is_null() { return -1; }
    (*p).0.insert(k, v);
    0
}

#[no_mangle]
pub unsafe extern "C" fn map_free(p: *mut Map) {
    if !p.is_null() { drop(Box::from_raw(p)); }
}
```

SAFETY: `p` ya null ya da `map_create` ürünü; double-free yok.

## Kaynaklar

- Nomicon ownership × FFI

## FFI kontrol listesi

- [ ] `extern "C"` / `#[no_mangle]`
- [ ] `#[repr(C)]` layout testi
- [ ] ownership (kim free eder?)
- [ ] nullability
- [ ] panic politikası
- [ ] thread safety (`Send`/`Sync`)


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
