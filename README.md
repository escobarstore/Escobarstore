# SMARTSZOP — Telegram Mini App / Vercel

Gotowy szkielet sklepu jako Telegram Mini App. Interfejs jest inspirowany przesłanymi ekranami: ciemne tło, zielono-cyjanowy akcent, zaokrąglone karty i dolna nawigacja.

## Co już działa

- 23 produkty w `app/page.tsx`
- 6 kategorii + „Wszystkie”
- 3 języki: PL / EN / RU
- koszyk z ilościami
- rabat 20% od 5 sztuk **tego samego produktu**
- darmowa dostawa od 70 zł — komunikat UI
- osobna informacja o gratisach
- formularz dostawy
- przycisk „Sprawdź” zawsze pokazuje „Dostawa dostępna / do 30 min”
- BLIK / Crypto / Paysafecard jako wybór metody
- zakładki: Menu / Koszyk / Regulamin / Opinie
- 5 opinii
- Telegram WebApp SDK
- API `/api/order` do przesyłania zamówień do administratora Telegrama
- API `/api/set-menu` do ustawienia przycisku Web App w menu bota

## Ważne: prawdziwe zdjęcia produktów

Przesłane przez Ciebie materiały są ekranami aplikacji, a nie 23 osobnymi zdjęciami produktów. Dlatego w projekcie są bezpieczne placeholdery SVG.

Podmień:
`public/products/product-01.svg` ... `product-23.svg`

na własne JPG/PNG/WebP i zmień ścieżkę `image` przy danym produkcie w `app/page.tsx`.

Nazwy, ceny, opisy i przypisanie do 6 kategorii również zmienisz w tablicy `PRODUCTS`.

## Vercel

1. Wrzuć projekt do GitHub.
2. W Vercel wybierz „Add New Project” i repozytorium.
3. Framework: Next.js (Vercel wykryje go automatycznie).
4. Dodaj zmienne środowiskowe:
   - `TELEGRAM_BOT_TOKEN`
   - `TELEGRAM_ADMIN_CHAT_ID`
5. Deploy.

Vercel ma natywne wsparcie dla Next.js.

## Telegram / BotFather

1. W @BotFather utwórz bota i skopiuj token.
2. Ustaw avatar bota w @BotFather.
3. Po wdrożeniu uzyskaj adres Vercel, np. `https://twoj-sklep.vercel.app`.
4. W BotFather skonfiguruj Mini App / Main Mini App z tym adresem.
5. Ustaw menu button na „Otwórz sklep”.

### Link otwierający Mini App

Dla Main Mini App użyj formatu:

`https://t.me/TWOJ_BOT?startapp`

Telegram dokumentuje również bezpośrednie linki do nazwanych Mini Apps:

`https://t.me/TWOJ_BOT/TWOJ_SHORT_NAME`

Samo `https://t.me/TWOJ_BOT` otwiera chat z botem; automatyczne wejście do Mini App zależy od konfiguracji Main Mini App / menu button.

## Automatyczne ustawienie menu button

Po wdrożeniu możesz wywołać:

`POST https://twoj-domenowy-adres.vercel.app/api/set-menu`

z JSON:

```json
{
  "url": "https://twoj-domenowy-adres.vercel.app",
  "text": "Otwórz sklep"
}
```

Endpoint korzysta z `TELEGRAM_BOT_TOKEN`.

## Zamówienia

Po ustawieniu `TELEGRAM_BOT_TOKEN` i `TELEGRAM_ADMIN_CHAT_ID` każde zamówienie jest wysyłane do wskazanego czatu Telegram.

Jeśli zmienne nie są ustawione, aplikacja działa w trybie demonstracyjnym i zapisuje zamówienie w logu funkcji Vercel.

### Jak znaleźć chat ID administratora

Najprościej napisz do swojego bota, a następnie użyj własnego mechanizmu botowego/webhooka do odczytania `chat.id`. Nie wpisuj tokena do kodu źródłowego.

## Płatności

BLIK, Crypto i Paysafecard są obecnie metodami wyboru przy składaniu zamówienia. Nie są to jeszcze prawdziwe bramki płatnicze. Integrację z konkretnym operatorem płatności należy dodać osobno.

## Dostosowanie wyglądu

Najważniejsze style są w:
`app/globals.css`

Avatar:
`public/avatar.svg`

Produkty:
`public/products/`

Teksty:
`T` w `app/page.tsx`

Produkty/kategorie:
`PRODUCTS` i `CATS` w `app/page.tsx`

## Najważniejsze: edycja sklepu w jednym pliku

Dane sklepu przeniesione są do:

`app/store-data.ts`

W tym pliku zmienisz m.in.:
- nazwę sklepu i operatora,
- próg darmowej dostawy,
- próg gratisów,
- liczbę sztuk od której działa rabat i procent rabatu,
- 6 kategorii w PL/EN/RU,
- nazwy, ceny, opisy, kategorię i zdjęcie wszystkich 23 produktów,
- 5 opinii w PL/EN/RU.

Zdjęcia produktów znajdują się w `public/products/`.

### Kategorie ustawione w tej wersji
- ENERGIA / ENERGY / ЭНЕРГИЯ
- EMPATIA / EMPATHY / ЭМПАТИЯ
- SOLE / SALTS / СОЛИ
- PRZYGODA / ADVENTURE / ПРИКЛЮЧЕНИЯ
- NATURA / NATURE / ПРИРОДА
- APTEKA / PHARMACY / АПТЕКА
