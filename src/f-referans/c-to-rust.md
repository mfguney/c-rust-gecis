# C → Rust kartları

Hızlı başvuru. Ayrıntı için ilgili bölümlere gidin.

| C | Rust | Not |
|---|------|-----|
| `malloc`/`free` | `Box`/`Vec` + Drop | sahiplik tipte |
| `NULL` | `Option` | null deref yok |
| `errno` / `int rc` | `Result` | `?` |
| `char buf[N]` | `[u8; N]` | uzunluk bilinen |
| `const char*` | `&str` / `&CStr` | UTF-8 / FFI |
| `void*` | generics / `*mut c_void` | tip silme son çare |
| `goto cleanup` | RAII Drop | erken return OK |
| `static` mutable | `OnceLock`/`Mutex` | yarışa dikkat |
| `#define MAX` | `Ord::max` / const | yan etkisiz |
| `_Generic` | generics + traits | monomorphize |
| `restrict` | `&mut` tekilliği | derleyici denetler |
| `pthread_mutex` | `Mutex` | poison modeli |
| `memcpy` punning | `from_ne_bytes` | aliasing güvenli |
| VLA | `Vec` / `arrayvec` | yığın patlamasın |
| `union` + tag | `enum` | idiomatik |

## Okuma

- A/bellek, B/türler-string, D/goto-drop
