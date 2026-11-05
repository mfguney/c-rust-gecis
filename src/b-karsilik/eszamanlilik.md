# Eşzamanlılık

| | C | Rust |
|---|----|------|
| Thread API | pthreads / C11 threads | `std::thread` |
| Yarış | data race = UB | safe’de yok |
| Paylaşım | dokümantasyon | `Send`/`Sync` |
| Kilit | mutex/rwlock | `Mutex`/`RwLock` |
| Atomik | `stdatomic.h` | `std::sync::atomic` |

Rust type system “bu değeri başka thread’e taşıyabilir misin?” sorusunu derleme
zamanında sorar. C’de TSan + disiplin.

## Kaynaklar

- Book ch.16; C atomics

## Yan yana örnek: sayaç

C atomik ve Rust atomik neredeyse aynı `memory_order` ailesini kullanır; fark
type system’in `Sync` dayatmasıdır.

```c
// C
atomic_fetch_add(&c, 1);
```

```rust
// Rust
c.fetch_add(1, Ordering::SeqCst);
```

## Kilit

C `pthread_mutex` ↔ Rust `Mutex`. Rust `lock().unwrap()` poison modelini bilin.
C’de `PTHREAD_MUTEX_ROBUST` ayrı konudur.

## Async notu

Rust `async` C’de eşdeğeri tek başına değildir; event loop / libuv / özel runtime
gerekir. Geçişte “her şeyi async yap” tuzağına düşmeyin.


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
