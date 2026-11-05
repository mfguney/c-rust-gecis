# Katkı Rehberi

Bu rehber C ve Rust kitaplarını köprüler. Karşılaştırmalar doğru ve idiomatik olsun;
“birebir sözdizimi eşlemesi” yerine zihinsel model farkını vurgulayın.

## Lisans

- Metin: CC BY-SA 4.0 (`LICENSE-CC-BY-SA`)
- Örnek kod: MIT (`LICENSE-CODE`)

## Bölüm yazma

1. Yan yana tablolarda C | Rust sütunlarını kullanın.
2. FFI örneklerinde ownership’in kimde kaldığını açık yazın.
3. Çapraz link: ilgili konular için `c-basvuru` / `rust-basvuru` bölümlerine işaret edin.
4. Bölüm sonunda **Kaynaklar** ekleyin.

## Yerel derleme

```bash
cargo install mdbook mdbook-mermaid
mdbook-mermaid install .
mdbook serve
```
