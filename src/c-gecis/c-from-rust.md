# C’yi Rust’tan çağırma

## Araçlar

| Araç | Rol |
|------|-----|
| `cc` | C kaynaklarını Cargo ile derle |
| `bindgen` | başlık → Rust FFI |
| `pkg-config` | sistem lib |

## Ownership animasyonu

<div class="step-anim" data-step-anim>
  <p class="step-anim__title">FFI sahipliği</p>
  <div class="step-anim__viewport">
    <div class="step-anim__frame" data-caption="C owner: Rust yalnızca ödünç alır. Rust free etmez.">
      <img src="../animations/ffi-ownership/frame1.svg" alt="C owner" />
    </div>
    <div class="step-anim__frame" data-caption="Ownership Rust’a geçtiyse Box::from_raw ile Drop bağlayın.">
      <img src="../animations/ffi-ownership/frame2.svg" alt="Rust owner" />
    </div>
  </div>
</div>

## İskelet

```rust
unsafe extern "C" {
    fn mylib_add(a: i32, b: i32) -> i32;
}
pub fn add(a: i32, b: i32) -> i32 {
    unsafe { mylib_add(a, b) }
}
```

`unsafe` yalnızca FFI çağrısında; dış API safe.

## Kaynaklar

- Nomicon FFI
- bindgen guide

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
