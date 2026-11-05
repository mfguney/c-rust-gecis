# Hata yayılımı

## C

```c
if ((rc = step1()) < 0) goto err;
if ((rc = step2()) < 0) goto err;
```

## Rust

```rust
fn pipeline() -> Result<(), Error> {
    step1()?;
    step2()?;
    Ok(())
}
```

Sınırda C’ye: `Result` → negatif kod + `thread_local` errno benzeri veya out-param.

`map_err` / `thiserror` ile bağlam ekleyin; `anyhow` uygulama tarafında.

## Kaynaklar

- Book ch.9

## Hata modeli seçimi

Tek politika seçin ve API genelinde uygulayın. Karışık `errno` + bool + sentinel
değer okunabilirliği öldürür. Rust’ta `?` + `map_err`; C sınırında kararlı
negatif kod tablosu.


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
