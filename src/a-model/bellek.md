# Bellek: free vs Drop

## C modeli

Dinamik bellek **açık sözleşme**dir. `malloc`/`free` çiftini siz kurarsınız;
unutmak sızıntı, erken/`çift` free UB.

```c
char *buf = malloc(64);
if (!buf) return -1;
/* ... */
free(buf);
buf = NULL;
```

Birden fazla işaretçi aynı bloğu gösteriyorsa “sahip kim?” dokümantasyondadır —
derleyici bilmez.

## Rust modeli

Sahiplik bitince `Drop` çalışır. Sızıntı için bilinçli `mem::forget` /
`Box::leak` gerekir.

```rust
let mut buf = vec![0u8; 64];
/* ... */
// drop otomatik
```

## Animasyon

<div class="step-anim" data-step-anim>
  <p class="step-anim__title">C free vs Rust Drop</p>
  <div class="step-anim__viewport">
    <div class="step-anim__frame" data-caption="C: tahsis ve free sizin sorumluluğunuz; unutmak sızıntı, erken free UAF.">
      <img src="../animations/memory-models/frame1.svg" alt="C modeli" />
    </div>
    <div class="step-anim__frame" data-caption="Rust: kapsam sonu Drop; double-free safe kodda yok.">
      <img src="../animations/memory-models/frame2.svg" alt="Rust modeli" />
    </div>
  </div>
</div>

## Geçiş ipuçları

| C sözleşmesi | Rust’a taşıma |
|--------------|----------------|
| çağıran free eder | `Box`/`Vec` döndür veya `Drop` sarmalayıcı |
| callee free eder | içeri alınca `from_raw` |
| ödünç, free yok | `&` / `*const`; asla `from_raw` |
| ortak sahiplik | `Arc` (+ kilit) veya arena |

## Kaynaklar

- Rust Book ch.4; Nomicon ownership
- CERT MEM*

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
