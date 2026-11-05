# UB kültürü vs safe invariants

## C gerçeği

Birçok hata sınıfı **UB**dır ve “şimdilik çalışıyor” görünebilir. Optimizasyon,
farklı derleyici veya sanitizer altında patlar. Disiplin + araçlar şarttır.

## Safe Rust gerçeği

Derleyici/borrow checker invariants’ı korur. Data race, UAF, double-free safe
kodda yok sayılır. **UB kapısı:** `unsafe` ve FFI.

## Geçişte zihinsel tuzaklar

1. C alışkanlığıyla raw pointer’ı her yere yaymak
2. `unsafe` ile “hızlıca” borrow checker’ı susturmak
3. C API’nin null/alias sözleşmesini Rust tipine yansıtmamak

## Strateji

Önce idiomatik safe Rust; FFI sınırını ince tutun; her `unsafe` için SAFETY
yorumu ve test (Miri).

## Kaynaklar

- Nomicon
- CERT C

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
