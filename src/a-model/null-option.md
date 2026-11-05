# Null vs Option, errno vs Result

## Null

C’de `NULL` her yerde; unutulmuş kontrol → UB.

```c
size_t n = strlen(p); /* p NULL ise UB */
```

Rust’ta `null` referans yoktur. Yokluk `Option`:

```rust
fn uzunluk(p: Option<&str>) -> usize {
    p.map(|s| s.len()).unwrap_or(0)
}
```

FFI’da nullable pointer → `Option<NonNull<T>>` veya `*mut T` + dokümantasyon.

## Hatalar

| C | Rust |
|---|------|
| `int rc` / `errno` | `Result<T, E>` |
| out-parametre `T *out` | `Result<T, E>` veya `(T, Warn)` |
| “0 başarı” karışık API | tek politika seçin |

```c
int parse(const char *s, int *out);
```

```rust
fn parse(s: &str) -> Result<i32, ParseError> { /* ... */ }
```

## unwrap gerçeği

`unwrap`/`expect` C’deki “assert non-null sonra kullan”a benzer — prototip OK,
kütüphane sınırında `?` tercih.

## Kaynaklar

- Book ch.6 / ch.9
- CERT EXP34-C

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
