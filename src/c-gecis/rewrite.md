# C → Rust yeniden yazım

## Strateji: strangler

1. Test / golden output sabitle
2. Dış API’yi dondur
3. Modül modül Rust’a taşı (veya önce sarmala)
4. Ownership’i tipe göm
5. `unsafe` yüzeyini küçült
6. C kodunu sil

Big-bang rewrite risklidir.

## Önce sarmala, sonra değiştir

C kütüphanesini `bindgen` ile sar → güvenli idiomatik katman → içi yeniden yaz.

## Metrikler

- Satır / modül başına sanitizer temizliği
- `unsafe` blok sayısı ve satırı
- Test kapsamı

## Kaynaklar

- Industry notes (Firefox/servo yüksek seviye ilham)

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
