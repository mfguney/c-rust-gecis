# Vaka: dinamik dizi (realloc vs Vec)

## C

```c
int *data = NULL; size_t len = 0, cap = 0;
int push(int v) {
    if (len == cap) {
        size_t n = cap ? cap * 2 : 4;
        int *p = realloc(data, n * sizeof *p);
        if (!p) return -1;
        data = p; cap = n;
    }
    data[len++] = v; return 0;
}
```

## Rust

```rust
let mut data = Vec::new();
data.push(v);
```

## Animasyon

<div class="step-anim" data-step-anim>
  <p class="step-anim__title">realloc vs Vec</p>
  <div class="step-anim__viewport">
    <div class="step-anim__frame" data-caption="Büyüme adresleri geçersiz kılabilir; C eski pointer UB, Rust borrow checker engeller.">
      <img src="../animations/vec-vs-realloc/frame1.svg" alt="karşılaştırma" />
    </div>
  </div>
</div>

## Dönüşüm notları

| C | Rust |
|---|------|
| `realloc` kontrolü | `try_reserve` / OOM abort |
| eleman pointer sakla | indeks tut |
| `len/cap` elle | `len()`/`capacity()` |

## Kaynaklar

- `man 3 realloc`; `Vec` docs

## Amortize büyüme

Kapasiteyi ×2 artırmak amortize O(1) `push` sağlar. Eski işaretçileri saklamayın;
indeks veya büyümeden sonra yeniden alın. Rust’ta borrow checker; C’de dikkat.


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
