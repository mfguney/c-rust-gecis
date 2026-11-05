# Sözlük (geçiş / ortak)

Üç kitapta senkron tutulur. Biçim: **Türkçe terim** — English (kısa açıklama).

| Türkçe | English | Not |
|--------|---------|-----|
| bellek yığını (yığın) | stack | Otomatik depolama; çerçeveler |
| öbek | heap | `malloc` / `Box` / `Vec` |
| işaretçi | pointer | C `T*` ≈ Rust `*mut T` / `&T` |
| tanımsız davranış | undefined behavior (UB) | C’de yaygın risk; safe Rust’ta yok |
| sahiplik | ownership | Rust modeli; C’de anlaşmalı |
| taşıma | move | Rust; C’de pointer hand-off |
| ödünç alma | borrowing | Rust `&`; C’de dokümantasyon |
| yaşam süresi | lifetime | Rust; C’de “kim free eder?” |
| yabancı işlev arayüzü | FFI | bindgen / cbindgen |
| temsil | repr(C) | FFI için layout anlaşması |
| sıkı aliasing | strict aliasing | C kuralı |
| null | null pointer | Rust’ta çoğu yerde `Option` |
| hata kodu | errno / return code | Rust’ta çoğu yerde `Result` |
| derleme birimi | translation unit | C; Rust’ta module/crate |
| iç değişkenlik | interior mutability | Rust; C’de `volatile`/atomik/kilit |

Kaynak kopyası: her depoda `GLOSSARY.md` ve `src/glossary.md` aynı tutulmalıdır.
