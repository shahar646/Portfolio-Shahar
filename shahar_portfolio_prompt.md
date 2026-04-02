# פרומפט לבניית פורטפוליו — שחר פריד
## להעתיק ולהדביק ב־Claude Code

---

## משימה

בני אתר פורטפוליו אישי מסוג **one-pager** בעברית (RTL) עבור שחר פריד, סטודנטית לטכנולוגיות למידה.
האתר יהיה **קובץ HTML יחיד עצמאי** (HTML + CSS + JS הכל inline), ללא תלות בספריות חיצוניות מלבד Google Fonts.

---

## טכני — חובה

- `<html dir="rtl" lang="he">`
- כל הטקסט בעברית
- Smooth scroll בין מקטעים
- קובץ אחד: `index.html`

---

## פונט

```css
@import url('https://fonts.googleapis.com/css2?family=Assistant:wght@300;400;600;700&display=swap');
font-family: 'Assistant', sans-serif;
```

- כותרות ראשיות (h1): `font-weight: 700`, `font-size: 2.8rem`
- כותרות מקטעים (h2): `font-weight: 700`, `font-size: 2rem`
- שמות פרויקטים (h3): `font-weight: 600`, `font-size: 1.3rem`
- טקסט רץ: `font-weight: 400`, `font-size: 1rem`

---

## פלטת צבעים

```css
:root {
  --cream:      #F7F4EF;   /* רקע בסיס */
  --grid-line:  #E2D9CA;   /* קווי משבצות */
  --purple:     #8783D1;   /* סגול */
  --purple-light: #B8B5E8; /* סגול בהיר לגוונים */
  --yellow:     #FFD95D;   /* צהוב/חרדל */
  --yellow-light: #FFF0A0; /* צהוב בהיר */
  --linen:      #F0EADC;   /* שמנת כהה יותר */
  --text-dark:  #2D2A22;   /* טקסט ראשי */
  --text-mid:   #5A5347;   /* טקסט משני */
}
```

---

## רקע האתר

רקע אחיד לכל ה־body — גוון שמנת `#F7F4EF` עם תבנית SVG של משבצות:

```css
body {
  background-color: #F7F4EF;
  background-image: url("data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' width='28' height='28'%3E%3Cpath d='M 28 0 L 0 0 0 28' fill='none' stroke='%23E2D9CA' stroke-width='0.5'/%3E%3C/svg%3E");
  background-repeat: repeat;
  background-attachment: fixed;
}
```

---

## סרגל ניווט — Floating Navbar

- תמיד צמוד לחלק העליון של המסך גם בגלילה (`position: fixed; top: 0`)
- **שקוף** עם `backdrop-filter: blur(12px)` ו־`background: rgba(247,244,239,0.75)`
- `border-radius: 0 0 20px 20px`
- `box-shadow: 0 2px 16px rgba(135,131,209,0.10)`
- סדר הקישורים מימין לשמאל: **בית | פרויקטים | אודות**
- קישורים: צבע `var(--text-dark)`, ללא underline, `font-weight: 600`
- hover: צבע `var(--purple)`, transition חלק
- padding: `12px 40px`

---

## מקטע 1 — Hero Section (`id="home"`)

**מבנה:**
- מרכז המסך אנכית ואופקית
- padding-top: גובה הנאבבר + 60px

**תוכן (מימין לשמאל — layout):**

**צד שמאל:** תמונת פרופיל
- מקום placeholder לתמונה: עיגול `200px × 200px`, רקע `var(--purple-light)`, border `3px solid var(--purple)`, טקסט קטן "תמונה תוכנס כאן"

**צד ימין:** טקסטים
- כותרת: `היי, שמי שחר` — `font-size: 2.8rem`, `font-weight: 700`
- תת־כותרת: `סטודנטית שנה ב' לתואר ראשון בטכנולוגיות למידה במכון הטכנולוגי חולון HIT.` — טקסט רץ רגיל

**כישורים מרחפים — Floating Skills:**
מתחת לטקסט, פסקת כישורים עם אנימציית floating:
כישורים: `AI` | `UX/UI` | `Figma` | `Illustrator` | `Unity 2D` | `Storyline`

כל chip:
```css
.skill-chip {
  background: white;
  border: 1.5px solid var(--purple);
  border-radius: 20px;
  padding: 6px 16px;
  font-size: 0.9rem;
  font-weight: 600;
  color: var(--purple);
  display: inline-block;
}
```

אנימציית float — כל chip עם `animation-delay` שונה (0, 0.3s, 0.6s וכו'):
```css
@keyframes float {
  0%, 100% { transform: translateY(0px); }
  50% { transform: translateY(-6px); }
}
.skill-chip { animation: float 3s ease-in-out infinite; }
```

---

## מעבר בין Hero לפרויקטים

**אלמנט מעבר** — מלבן מעוגל בצבע `var(--yellow)` עם `opacity: 0.35`, `height: 80px`, `border-radius: 40px`, `margin: 40px auto`, `width: 80%`.  
זה נותן תחושה של מעבר בין אזורים — כמו ריבוע צבעוני שמחלק את הדף.

---

## מקטע 2 — פרויקטים נבחרים (`id="projects"`)

### כותרת המקטע
```
פרויקטים נבחרים
```
- מיושרת **לימין** עם `padding-right: 60px`
- אפקט מרקר: pseudo-element `::after` (או `::before`) שמדמה הדגשה בצהוב מתחת לטקסט:
```css
.section-title {
  position: relative;
  display: inline-block;
}
.section-title::after {
  content: '';
  position: absolute;
  bottom: 2px;
  right: 0;
  left: 0;
  height: 12px;
  background: var(--yellow);
  opacity: 0.55;
  border-radius: 3px;
  z-index: -1;
}
```

### טקסט הסבר מעל המסגרות
```
בלחיצה על תמונת הפרויקט הוא יפתח בכרטיסיה חדשה.
לקריאה נוספת אודות תהליך העבודה על הפרויקט אפשר ללחוץ על הכפתור +
```
- טקסט קטן, `color: var(--text-mid)`, מיושר לימין מתחת לכותרת

### כרטיסי פרויקטים — 2 כרטיסים זה לצד זה

**חשוב: מסגרת בסגנון ציור קווי / כתב יד**

כל כרטיס:
- `width: ~45%`
- גובה: `auto`
- border בסגנון sketch — **לא** `border` רגיל אלא SVG filter או border עם אפקט ידני:

```css
.project-card {
  border: 2.5px solid var(--text-dark);
  border-radius: 12px;
  /* אפקט ציור ידני — קצת לא ישר */
  box-shadow: 3px 3px 0px var(--text-dark);
  position: relative;
  background: white;
  overflow: visible;
}
```

**מבנה הכרטיס מלמעלה למטה:**

1. **שם הפרויקט** — מעל המסגרת (מחוץ לה, מעליה):
   - `font-weight: 600`, `font-size: 1.3rem`, מיושר לכרטיס

2. **תוך הכרטיס:**
   - **תמונה מייצגת** — לוחצים עליה → פותח קישור בכרטיסייה חדשה (`target="_blank"`)
   - לתמונה: `cursor: pointer`, `transition: opacity 0.2s`, hover `opacity: 0.85`
   - **תיאור טקסט** מתחת לתמונה — padding בצדדים

3. **כפתור `+` בתחתית הכרטיס** — ממורכז בצלע התחתונה:
   ```css
   .plus-btn {
     position: absolute;
     bottom: -20px;
     left: 50%;
     transform: translateX(-50%);
     width: 40px;
     height: 40px;
     border-radius: 50%;
     background: var(--purple);
     color: white;
     font-size: 1.5rem;
     border: none;
     cursor: pointer;
     display: flex;
     align-items: center;
     justify-content: center;
     box-shadow: 2px 2px 8px rgba(135,131,209,0.4);
     transition: transform 0.2s, background 0.2s;
   }
   .plus-btn:hover {
     background: var(--yellow);
     color: var(--text-dark);
     transform: translateX(-50%) scale(1.1);
   }
   ```
   - בלחיצה על `+`: **accordion** — נפתח פאנל מתחת לכרטיס עם placeholder:
     ```
     [כאן יופיע תיאור שלבי העבודה על הפרויקט — יתווסף בהמשך]
     ```
     פאנל ה־accordion: `background: var(--linen)`, `border-radius: 0 0 12px 12px`, `padding: 20px`

---

### פרטי הפרויקטים

**פרויקט 1 — על השולחן**
- שם: `על השולחן`
- תמונה: `project1.jpg` (תמונה שסופקה — אתר הדרכה לעיצוב שולחן)
- קישור בלחיצה על תמונה: `https://www.figma.com/proto/R5cmikVUbnmKYxLE1KKueM/%D7%A2%D7%9C-%D7%94%D7%A9%D7%95%D7%9C%D7%97%D7%9F?node-id=293-24490&t=hJI7ZYm0Q96Higu2-1`
- תיאור: `אפיון ועיצוב אתר הדרכתי ב-Figma. מטרתו להעניק למשתמש ידע בסיסי וכלים פשוטים לעצב שולחן למצבי אירוח שונים.`

**פרויקט 2 — Rapid e-Learning**
- שם: `Rapid e-Learning`
- תמונה: `project2.jpg` (תמונה שסופקה — לומדה על Jailbreak)
- קישור בלחיצה על תמונה: `https://edu.sliceapp.net/share/6954e58d4591ca0832600c0b`
- תיאור: `לומדה יישומית לזיהוי ומניעת Jailbreak במודלי שפה. פותח ב-Slice.`

> **הערה לגבי התמונות:** התמונות מסופקות כ-`project1.jpg` ו-`project2.jpg` בתיקיית הפרויקט. טמיע אותן עם `<img src="project1.jpg">` וכו'. אם אין גישה לקבצים, השתמש ב-placeholder בצבע `var(--purple-light)` עם טקסט "תמונת הפרויקט".

---

### טקסט מתחת לכרטיסים (מעל הכפתור)

```
ואם ברצונך לראות פרויקטים נוספים, לחיצה על הכפתור תיקח אותך לשם.
```
- טקסט קטן, מיושר למרכז, `color: var(--text-mid)`

### כפתור — "אני רוצה לראות!"

```css
.cta-btn {
  display: block;
  margin: 24px auto;
  padding: 14px 36px;
  background: var(--yellow);
  color: var(--text-dark);
  border: 2px solid var(--text-dark);
  border-radius: 30px;
  font-family: 'Assistant', sans-serif;
  font-weight: 700;
  font-size: 1.05rem;
  cursor: pointer;
  box-shadow: 3px 3px 0 var(--text-dark);
  transition: transform 0.15s, box-shadow 0.15s;
}
.cta-btn:hover {
  transform: translate(-2px, -2px);
  box-shadow: 5px 5px 0 var(--text-dark);
}
```

הכפתור ב־scroll ליעד `id="more-projects"` (placeholder — מקטע ריק עם טקסט "פרויקטים נוספים יתווספו בהמשך")

---

## מעבר בין פרויקטים לאודות

אותו אפקט מעבר כמו קודם אבל בצבע `var(--purple)` עם `opacity: 0.25`

---

## מקטע 3 — קצת עליי (`id="about"`)

### כותרת
```
קצת עליי
```
- אותו עיצוב כותרת כמו "פרויקטים נבחרים" — מיושרת לימין, אפקט מרקר
- צבע המרקר: `var(--purple)` (לגיוון)

### תוכן

טקסט:
```
שלום, שמי שחר פריד, סטודנטית שנה ב' לתואר ראשון בטכנולוגיות למידה במכון הטכנולוגי חולון HIT.
אני משלבת בין עיצוב, טכנולוגיה ואנשים, ומתמקדת באפיון ופיתוח חוויות למידה דיגיטליות ואינטראקטיביות. במהלך לימודיי אני יוצרת תוצרים המשלבים חשיבה פדגוגית, חוויית משתמש וכלים טכנולוגיים, במטרה לייצר למידה משמעותית, ברורה ומעוררת מעורבות.
```
- `max-width: 600px`, מיושר לימין

### אייקונים ליצירת קשר

שני אייקונים זה לצד זה, מיושרים לימין:

**LinkedIn:**
```html
<a href="https://www.linkedin.com/in/shahar-frid" target="_blank" title="LinkedIn">
  <!-- SVG אייקון LinkedIn -->
</a>
```
- SVG inline של אייקון LinkedIn (official square icon)
- hover: `color: var(--purple)`, scale 1.1

**Email — Copy to Clipboard:**
```html
<button onclick="copyEmail()" title="העתק כתובת מייל" id="email-btn">
  <!-- SVG אייקון מעטפה -->
</button>
```
- בלחיצה: מעתיק `shahar.frid1@gmail.com` לקליפבורד
- אחרי העתקה: הכפתור משנה צבע ל-`var(--purple)` ומציג tooltip קטן: ✓ הועתק!
- JavaScript:
```javascript
function copyEmail() {
  navigator.clipboard.writeText('shahar.frid1@gmail.com').then(() => {
    const btn = document.getElementById('email-btn');
    btn.style.color = '#8783D1';
    const tip = document.createElement('span');
    tip.textContent = '✓ הועתק!';
    tip.style.cssText = 'position:absolute;background:#8783D1;color:white;padding:4px 10px;border-radius:8px;font-size:0.8rem;right:0;top:-30px;';
    btn.style.position = 'relative';
    btn.appendChild(tip);
    setTimeout(() => tip.remove(), 2000);
  });
}
```

---

## Footer

פשוט ומינימלי:
```
© 2025 שחר פריד
```
- `font-size: 0.85rem`, `color: var(--text-mid)`, מרכז, padding: 30px

---

## מקטע נוסף — פרויקטים נוספים (`id="more-projects"`)

מיקום: **בין מקטע הפרויקטים למקטע אודות**

תוכן:
```
עוד פרויקטים יתווספו כאן בקרוב ✨
```
- כרטיס placeholder מרכזי בסגנון כרטיסי הפרויקטים — מסגרת ציור קווי, `width: 80%`, `margin: auto`
- `background: var(--linen)`, טקסט מרכז, `color: var(--text-mid)`

---

## אנימציות כלליות

**Fade-in בטעינה:**
```css
@keyframes fadeInUp {
  from { opacity: 0; transform: translateY(20px); }
  to   { opacity: 1; transform: translateY(0); }
}
section { animation: fadeInUp 0.6s ease both; }
```

**Scroll smooth:**
```css
html { scroll-behavior: smooth; }
```

---

## סיכום מבנה הקוד

```
index.html
  ├── <head> — meta, fonts, CSS inline
  ├── <nav> — floating navbar
  ├── <section id="home"> — Hero
  ├── [divider element — yellow]
  ├── <section id="projects"> — פרויקטים נבחרים
  ├── <section id="more-projects"> — פרויקטים נוספים (placeholder)
  ├── [divider element — purple]
  ├── <section id="about"> — קצת עליי
  ├── <footer>
  └── <script> — JS inline (clipboard, accordion)
```

---

## הערות חשובות

1. **תמונות הפרויקטים** — אם אתה מריץ ב־Claude Code, שים את `project1.jpg` ו-`project2.jpg` באותה תיקייה כמו `index.html`. אחרת, השתמש ב-placeholder.
2. **RTL** — ודא שכל flexbox layout מתחשב בכיוון RTL (`flex-direction: row-reverse` היכן שצריך).
3. **Responsive** — הכרטיסים ייסדרו ב-column במובייל (`@media (max-width: 768px)`).
4. **Accordion** — כפתור ה-`+` מסובב ל-`×` כשפתוח (CSS transform: rotate(45deg)).
