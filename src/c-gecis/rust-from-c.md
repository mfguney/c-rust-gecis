# Rust’ı C’den çağırma

```toml
[lib]
crate-type = ["cdylib", "staticlib"]
```

```rust
#[no_mangle]
pub extern "C" fn rs_add(a: i32, b: i32) -> i32 {
    a + b
}
```

## Panic

`extern "C"` sınırında panic → UB. `catch_unwind` veya `panic=abort` +
dokümantasyon.

## cbindgen

Başlık üretimi; CI’da doğrula. Opaque `struct Type;` kalıbı.

## Kaynaklar

- Nomicon FFI
- cbindgen book

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
