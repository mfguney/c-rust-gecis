# Özet

[Giriş](giris.md)

# A. Zihinsel model

- [Bellek: free vs Drop](a-model/bellek.md)
- [Null vs Option, errno vs Result](a-model/null-option.md)
- [Derleme birimi vs crate](a-model/derleme.md)
- [UB kültürü vs safe invariants](a-model/ub-vs-safe.md)

# B. Dil karşılıkları

- [Türler ve string’ler](b-karsilik/turler-string.md)
- [Dizi, slice, vektör](b-karsilik/dizi-slice.md)
- [Struct layout ve repr(C)](b-karsilik/struct-layout.md)
- [Enum modelleri](b-karsilik/enum.md)
- [Generics vs _Generic](b-karsilik/generics.md)
- [Eşzamanlılık](b-karsilik/eszamanlilik.md)

# C. Geçiş yolları

- [C → Rust yeniden yazım](c-gecis/rewrite.md)
- [C’yi Rust’tan çağırma](c-gecis/c-from-rust.md)
- [Rust’ı C’den çağırma](c-gecis/rust-from-c.md)
- [Karışık projeler](c-gecis/karisik.md)
- [Incremental migration checklist](c-gecis/checklist.md)

# D. Tuzaklar ve dönüşümler

- [goto cleanup → Drop](d-tuzaklar/goto-drop.md)
- [out-parametre → Result](d-tuzaklar/out-param.md)
- [Global mutable state](d-tuzaklar/global.md)
- [Callback + userdata](d-tuzaklar/callback.md)
- [Aliasing ve unsafe](d-tuzaklar/aliasing.md)

# E. Vaka çalışmaları

- [Dinamik dizi: realloc vs Vec](e-vaka/dinamik-dizi.md)
- [Hash map FFI sarmalayıcı](e-vaka/hashmap-ffi.md)
- [Hata yayılımı](e-vaka/hata.md)
- [Thread-safe sayaç](e-vaka/sayac.md)

# F. Hızlı referans

- [C → Rust kartları](f-referans/c-to-rust.md)
- [Rust → C / FFI kartları](f-referans/rust-to-c.md)
- [Okuma sırası](f-referans/okuma-sirasi.md)

---

[Sözlük](glossary.md)
[İlgili kitaplar](ilgili.md)
