# מכירת גראז' — אתר GitHub Pages

אתר סטטי בעברית להצגת פריטים למכירה.  
כתובת האתר: https://oren1210.github.io/garage/

## מבנה הפרויקט

```
garage/
├── index.html      # דפי האתר והלוגיקה
├── styles.css      # עיצוב
├── items.json      # כל הנתונים (פריטים, קטגוריות, יצירת קשר)
├── photos/         # תמונות הפריטים
└── README.md       # המדריך הזה
```

## תצוגה מקומית

האתר טוען את `items.json` דרך HTTP. הריצו מתוך תיקיית הפרויקט:

```bash
cd /path/to/garage
python3 -m http.server 8000
```

פתחו בדפדפן: http://localhost:8000

## הוספת פריט חדש

1. הוסיפו תמונות לתיקייה `photos/` (מומלץ: `{מזהה-פריט}-1.jpg`, `{מזהה-פריט}-2.jpg`).
2. ערכו את `items.json` והוסיפו אובייקט למערך `items`:

```json
{
  "id": "chair-01",
  "category": "furniture",
  "subsection": "chairs",
  "title": "כיסא עץ",
  "images": ["photos/chair-01-1.jpg", "photos/chair-01-2.jpg"],
  "hidden": false,
  "description": "כיסא נוח, מצב טוב",
  "brand": "IKEA",
  "condition": "טוב",
  "price": 120,
  "dimensions": "45×45×90 ס״מ",
  "notes": "איסוף עצמי"
}
```

| שדה | חובה | הסבר |
|-----|------|------|
| `id` | כן | מזהה ייחודי (אנגלית, ללא רווחים) |
| `category` | כן | מזהה קטגוריה מ-`categories` |
| `subsection` | לא | מזהה תת-קטגוריה תחת אותה קטגוריה |
| `title` | כן | כותרת בעברית |
| `images` | כן | מערך נתיבים; התמונה הראשונה = תמונת ממוזערת |
| `hidden` | לא | `true` = הפריט לא יוצג באתר (ברירת מחדל: `false`) |
| `description` | לא | תיאור |
| `brand` | לא | מותג |
| `condition` | לא | מצב הפריט |
| `price` | לא | מספר (מוצג כ-₪XX) או מחרוזת (למשל `"מחיר לפי הצעה"`) |
| `dimensions` | לא | מידות |
| `notes` | לא | הערות נוספות |

## עריכת פריט קיים

מצאו את הפריט במערך `items` לפי `id` ועדכנו את השדות. לשינוי תמונות — עדכנו את מערך `images` והחליפו קבצים ב-`photos/`.

## שיתוף קישור לפריט

לכל פריט יש קישור ישיר לפי המזהה `id`:

```
https://oren1210.github.io/garage/#item/shirt-01
```

- פתיחת הפריט בדפדפן → הקטלוג נפתח והפריט מוצג בחלון הפרטים.
- בתוך חלון הפרטים: לחצו **העתקת קישור לפריט** כדי להעתיק את הקישור ללוח.
- פריטים עם `"hidden": true` לא נפתחים בקישור ישיר.

## הסתרת פריט (בלי למחוק)

```json
"hidden": true
```

הפריט נשאר ב-JSON אך לא מופיע בדף הבית, בקטלוג או בחיפוש.

## קטגוריות ותת-קטגוריות

ערכו את מערך `categories` ב-`items.json`:

```json
{
  "id": "clothes",
  "label": "בגדים",
  "subsections": [
    { "id": "t-shirts", "label": "חולצות" }
  ]
}
```

- `id` — מזהה באנגלית (משמש בפריטים בשדה `category` / `subsection`).
- `label` — שם בעברית שמוצג באתר.

לאחר הוספת קטגוריה, ודאו שפריטים משתמשים ב-`category` (וב-`subsection` אם רלוונטי) תואמים.

## פרטי יצירת קשר

עדכנו ב-`items.json` תחת `site.contact`:

```json
"contact": {
  "email": "your@email.com",
  "whatsapp": "972501234567",
  "whatsappMessage": "שלום, אשמח לשאול על פריט מהאתר"
}
```

- `whatsapp` — מספר בלבד, עם קידומת מדינה, **בלי** `+` או מקפים.
- `whatsappMessage` — טקסט ברירת מחדל שנפתח בוואטסאפ.

## התחלת Git (פעם ראשונה)

```bash
cd /path/to/garage
git init -b main
git remote add origin https://github.com/oren1210/garage.git
git add .
git commit -m "הקמת אתר מכירת גראז'"
git push -u origin main
```

## פריסה ל-GitHub Pages

1. דחפו את הקוד ל-https://github.com/oren1210/garage (ענף `main`).
2. ב-GitHub: **Settings → Pages → Source**: Deploy from branch `main`, folder `/ (root)`.
3. האתר יהיה זמין ב: https://oren1210.github.io/garage/

```bash
git add .
git commit -m "עדכון אתר"
git push origin main
```

אין צורך בפקודת build — האתר סטטי.

## טיפים

- שמרו על `id` ייחודי לכל פריט.
- דחסו תמונות לפני העלאה (JPG, רוחב ~1200px מספיק).
- פריט לדוגמה עם `"hidden": true` ב-JSON (`lamp-hidden`) — לבדיקת הסתרה; אפשר למחוק אחרי הבדיקה.
