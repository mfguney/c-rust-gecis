# Aliasing ve unsafe

C `restrict` yalanı ≈ Rust’ta yanlış `&mut` alias.
Strict aliasing ihlali ≈ Stacked/Tree Borrows ihlali.

Kurallar farklı formalize edilir; pratik ders aynı: çelişkili yazma yolları UB.

Çözümler: sınırları ayır, `UnsafeCell`, bayt+`memcpy`, safe API tasarımı.

## Kaynaklar

- Nomicon; CERT EXP39-C

## Somut senaryo

```c
void f(int *a, int *b) { *a = 1; *b = 2; }
// f(&x, &x) — alias; restrict varsa UB
```

```rust
fn f(a: &mut i32, b: &mut i32) { *a = 1; *b = 2; }
// f(&mut x, &mut x) — derlenmez
```

Rust sizi korur; C FFI’da aynı koruma yok — sarmalayıcıda `split` edin.

## Bayt yolu

Tür punning için `memcpy` / `u8` dilimleri her iki dilde de güvenli kalıptır.


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
