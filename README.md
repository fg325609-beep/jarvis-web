# 🤖 Jarvis Web — Siri kabi, hech qanday ilova ochmasdan

## 1. Vercel'ga joylash
1. Bu papkani GitHub'ga yuklang.
2. vercel.com → **Add New → Project** → repozitoriyni tanlang.
3. **Environment Variables** bo'limiga qo'shing:
   - `GEMINI_API_KEY` — aistudio.google.com dan bepul kalit
   - `JARVIS_TOKEN` — o'zingiz o'ylab topgan parol (boshqalar limitingizni ishlatmasligi uchun)
   - `USER_NAME` — ismingiz
4. **Deploy**. Kalit faqat serverda turadi, foydalanuvchiga ko'rinmaydi.

Lokal sinash: `.env.example` ni `.env.local` ga nusxalang → `npm install` → `npm run dev`.

## 2. iPhone: "Hey Siri, Jarvis" (ilova ochilmaydi)
**Shortcuts (Команды)** ilovasida yangi shortcut yarating va nomini **Jarvis** qo'ying:

1. **Dictate Text (Диктовать текст)** — tilni tanlang (o'zbek bo'lmasa, rus yoki ingliz — Jarvis baribir o'zbekcha javob beradi).
2. **Get Contents of URL (Получить содержимое URL)**
   - URL: `https://SIZNING-SAYT.vercel.app/api/siri?token=PAROLINGIZ`
   - Method: **POST**, Request Body: **JSON**, kalit `q` → qiymat: *Dictated Text*
3. **Speak Text (Произнести текст)** → *Contents of URL*. Ovozni sozlamada tanlang (o'zbekcha bo'lmasa, turkcha lotin matnni yaxshiroq o'qiydi).

Endi: **"Hey Siri, Jarvis"** → savol bering → javobni ovoz bilan eshitasiz.

**Sayt ham ochsin desangiz:** URL oxiriga `&format=json` qo'shing, keyin:
*Get Dictionary Value* `reply` → *Speak Text*; *Get Dictionary Value* `url` → *If has any value* → *Open URLs*.

## 3. Android
Saytni **Chrome**'da oching → ⋮ menyu → **"Ilovani o'rnatish"** (yoki "Bosh ekranga qo'shish").
Ekranda Jarvis ikonkasi paydo bo'ladi — oching, 🎙 bosing, gapiring. Javobni **Madina** o'zbekcha ovozida aytadi.
Birinchi marta mikrofonga ruxsat so'raydi — "Ruxsat berish" ni bosing.

## 4. Web ilova (iPhone va kompyuter)
Saytni Safari/Chrome'da oching → **Ulashish → Uy ekraniga qo'shish**. Jarvis ilova kabi to'liq ekranda ochiladi: 🎙 bosib gapirasiz, javobni ovoz bilan aytadi, saytlarni ochadi.

## API
| Endpoint | Vazifasi |
|---|---|
| `POST /api/jarvis` | `{message, history}` → `{reply, action, args, url}` (web ilova uchun) |
| `POST /api/tts` | `{text}` → MP3 (Madina ovozi) |
| `POST /api/voice` | `{audio: WAV base64, history}` → `{heard, reply, action, args, audio: MP3 base64}` (Android ilova uchun, bitta so'rov) |
| `GET/POST /api/siri` | Oddiy matn javob (Siri uchun); `?format=json` → `{reply, url}` |

Parol: `x-jarvis-token` header yoki `?token=`.

## Cheklovlar (ochiq)
- Vercel kompyuteringizni boshqara olmaydi (VS Code, terminal) — buning uchun lokal Python Jarvis bor.
- "Hey Jarvis" deb brauzerni fonda eshittirib bo'lmaydi — iPhone'da buning o'rniga "Hey Siri, Jarvis" ishlatiladi.
- Ovoz Microsoft Edge TTS orqali olinadi (bepul, rasmiy API emas). U ishlamay qolsa, ilova avtomatik brauzer ovoziga o'tadi.
# jarvis-web
