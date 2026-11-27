# Hello Sweetie USA · Find Your Store + Sweetie Claw

Instagram bio linkine konacak sayfa. Mağaza bulucu ve Sweetie Claw oyunu aynı sayfada.

Adres: **https://hellosweetieusa.navynightcreative.com**

## Dosyalar
- `index.html`: sayfanın kendisi. Mağaza bilgileri de bunun içinde.
- `fonts/`: yazı tipleri. Sayfa dışarıdan hiçbir şey yüklemiyor (GA4 açılırsa sadece o).
- `og-image.png`: link paylaşılınca görünen önizleme görseli.
- `favicon.svg`, `favicon-32.png`, `apple-touch-icon.png`: sekme ve ana ekran ikonları.
- `404.html`: yanlış adrese gelenleri ana sayfaya yönlendiren sayfa.
- `CNAME`: GitHub'a alt alan adını söyleyen dosya. İçinde sadece adres yazıyor, silinmemeli.
- `.nojekyll`, `robots.txt`: GitHub Pages ve arama motorları için.

## Yayına alma (bir kere yapılır)
1. GitHub'da `hellosweetieusa` adında public bir repo aç.
2. Bu klasördeki her şeyi reponun ana dizinine yükle. `.nojekyll` ve `CNAME` dahil.
3. Repo → **Settings → Pages** → Source: **Deploy from a branch** → Branch: **main**, klasör **/(root)** → Save.
4. navynightcreative.com'un DNS paneline gir. DNS'in nerede yönetildiği kontrol edilecek; Bobby Dixon alt alan adı da aynı panelden eklenmiş olmalı. Şu kaydı ekle:

   | Tür | Ad (Host) | Değer |
   |---|---|---|
   | CNAME | `hellosweetieusa` | `yavasemirhan.github.io` |

5. Repo → Settings → Pages → **Custom domain** alanında `hellosweetieusa.navynightcreative.com` yazıyor olmalı (CNAME dosyasından gelir). DNS oturunca (birkaç dakika, bazen birkaç saat) **Enforce HTTPS** kutusunu işaretle.
6. Adresi telefondan aç, kontrol et. Sonra Instagram bio linkini değiştir:

```
https://hellosweetieusa.navynightcreative.com/?utm_source=instagram&utm_medium=bio
```

Sondaki etiket, GA4'te ziyaretin bio'dan geldiğini ayırmak için.

## Mağaza bilgisi güncelleme
`index.html` içinde `STORES_DATA` listesini bul. Her mağaza bir blok.

| İşletme onayladığında | Ne yapılır |
|---|---|
| Saatler | `hours: 'Mon–Sat 10 AM – 8 PM · Sun 11 AM – 6 PM'` gibi yaz, `hoursConfirmed: true` yap |
| Dükkan numarası | `unit: 'F11'` yaz, `unitConfirmed: true` yap |
| Telefon | `phone: '(708) 000-0000'` yaz. "Call" butonu kendiliğinden çıkar |
| AVM içindeki yer | `wayfinding: 'Upper level, next to the food court'` gibi yaz |
| Yeni mağaza | Listeye yeni bir blok ekle (adres, `lat` / `lng`, bölge). Henüz müşteriye gösterilmeyecekse `hidden: true` ekle |
| Onaylanan bilgi | O bilgiyle ilgili `notes` satırını sil |

Onaylanmamış bilgi müşteriye hiç görünmez. Adresin sonuna `#review` eklenince tüm "To confirm" notları görünür; işletmeye bilgi onaylatırken bu link gönderilir.

## Ölçüm (GA4)
`index.html` içinde `HS_CONFIG = { ga4Id: "" }` satırına ölçüm kimliği yazılınca açılır (ör. `"G-XXXXXXXXXX"`). Sayılan olaylar:
- `directions_click`, `details_click`, `copy_address`, `call_click`: mağaza bazında
- `map_pin_click`, `state_filter`, `use_location`
- `claw_nav_click`, `claw_first_grab`, `claw_series_complete`
- `instagram_click`, `tiktok_click`

Raporda yol tarifi tıklaması "mağaza ziyareti" diye yazılmaz, ziyaret niyeti olarak yazılır.

## Sweetie Claw
- Sadece eğlence için. Ödül, kupon veya sıralama yok.
- Her gün 20 ücretsiz jeton. Aynı ürün 3 kez yakalanırsa (double) 1 jetonla takas edilebilir.
- İlerleme sadece oyuncunun kendi telefonunda saklanır. Kayıt yok, kişisel veri toplanmıyor.
- Ödül sistemi onaylanırsa kayıt, yaş kontrolü ve kurallar sayfası eklenmeden açılmayacak (bkz. kepçe oyunu çalışması).

## Tasarımda değişiklik yaparken
Sayfadaki stiller derlenmiş Tailwind CSS. Yeni bir Tailwind sınıfı eklenirse (ör. yeni renk veya boşluk) CSS'in yeniden derlenmesi gerekir. Metin, link ve mağaza bilgisi değişiklikleri için derlemeye gerek yok.
