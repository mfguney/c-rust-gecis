# Callback + userdata

C:

```c
typedef void (*cb_t)(int ev, void *user);
void set_cb(cb_t cb, void *user);
```

Rust idiomatik: `FnMut`, trait object, channel.

FFI’da hâlâ `extern "C" fn` + `*mut c_void` gerekir:

```rust
unsafe extern "C" fn trampoline(ev: i32, user: *mut c_void) {
    let cb = &mut *(user as *mut Box<dyn FnMut(i32)>);
    cb(ev);
}
```

Lifetime/`Send` sınırlarını dokümante edin.

## Kaynaklar

- Nomicon FFI callbacks

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
