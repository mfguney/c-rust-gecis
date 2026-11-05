# Rust → C / FFI kartları

| Rust | C / FFI | Not |
|------|---------|-----|
| `String` | `ptr`+`len` veya `CString` | kim free? |
| `&str` | `ptr`+`len` (UTF-8) | null-terminated değil |
| `&[u8]` | `uint8_t*` + `size_t` | |
| `Option<&T>` | nullable pointer | |
| `Result<T,E>` | out-param + hata kodu | panic yok |
| `Vec<T>` | ptr/len/cap + destroy | |
| `Box<T>` | opaque `T*` | `into_raw`/`from_raw` |
| `Arc<T>` | refcount API | clone/drop |
| `panic!` | abort / catch | sınırı geçirme |
| `#[repr(C)]` | eşleşen struct | test `size_of` |
| `enum` veri | tag+union veya opaque | |
| `&mut T` | `T*` exclusive | alias yok |

## Kontrol

Her export için: ownership, nullability, thread safety, panic.

## Okuma

- C/rust-from-c, E/hashmap-ffi, B/struct-layout
