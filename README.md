# -<!DOCTYPE html>
<html lang="he">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>הברמן הדיגיטלי שלך</title>
  <style>
    @import url('https://fonts.googleapis.com/css2?family=Assistant:wght@400;700&display=swap');

    body {
      font-family: 'Assistant', sans-serif;
      background: linear-gradient(135deg, #0f044c, #5c1e87, #3c8dbc);
      background-size: 400% 400%;
      animation: galaxyBG 20s ease infinite;
      text-align: center;
      direction: rtl;
      padding: 20px;
      color: #f0f0f0;
    }

    @keyframes galaxyBG {
      0% {background-position: 0% 50%;}
      50% {background-position: 100% 50%;}
      100% {background-position: 0% 50%;}
    }

    h1 {
      color: #d1c4e9;
      font-size: 36px;
      margin-bottom: 30px;
    }

    .question {
      margin: 20px auto;
      max-width: 500px;
      background-color: rgba(0, 0, 0, 0.3);
      padding: 20px;
      border-radius: 10px;
      box-shadow: 0 0 10px rgba(255, 255, 255, 0.1);
    }

    .btn-group {
      display: flex;
      flex-wrap: wrap;
      justify-content: center;
    }

    .btn {
      background-color: #673ab7;
      color: white;
      border: none;
      padding: 10px 16px;
      margin: 5px;
      border-radius: 5px;
      cursor: pointer;
      transition: background-color 0.3s ease;
    }

    .btn:hover {
      background-color: #9575cd;
    }

    .result {
      font-size: 24px;
      color: #b3e5fc;
      margin-top: 30px;
      background-color: rgba(255, 255, 255, 0.1);
      padding: 15px;
      border-radius: 8px;
    }

    .footer {
      margin-top: 40px;
      font-size: 14px;
      color: #cccccc;
    }
  </style>
</head>
<body>
  <h1>הברמן הדיגיטלי שלך</h1>

  <div id="question-container">
    <div class="question" id="question1">
      <p>מה טווח הגילאים שלך?</p>
      <div class="btn-group">
        <button class="btn" onclick="next('age', '18-25')">18-25</button>
        <button class="btn" onclick="next('age', '26-35')">26-35</button>
        <button class="btn" onclick="next('age', '36+')">36+</button>
      </div>
    </div>
  </div>

  <div class="question" id="question2" style="display:none;">
    <p>מה המזל שלך?</p>
    <div class="btn-group">
      <button class="btn" onclick="next('sign', 'טלה')">טלה</button>
      <button class="btn" onclick="next('sign', 'שור')">שור</button>
      <button class="btn" onclick="next('sign', 'תאומים')">תאומים</button>
      <button class="btn" onclick="next('sign', 'סרטן')">סרטן</button>
      <button class="btn" onclick="next('sign', 'אריה')">אריה</button>
      <button class="btn" onclick="next('sign', 'בתולה')">בתולה</button>
      <button class="btn" onclick="next('sign', 'מאזניים')">מאזניים</button>
      <button class="btn" onclick="next('sign', 'עקרב')">עקרב</button>
      <button class="btn" onclick="next('sign', 'קשת')">קשת</button>
      <button class="btn" onclick="next('sign', 'גדי')">גדי</button>
      <button class="btn" onclick="next('sign', 'דלי')">דלי</button>
      <button class="btn" onclick="next('sign', 'דגים')">דגים</button>
    </div>
  </div>

  <div class="question" id="question3" style="display:none;">
    <p>מה העונה שאתה הכי אוהב?</p>
    <div class="btn-group">
      <button class="btn" onclick="next('season', 'אביב')">אביב</button>
      <button class="btn" onclick="next('season', 'קיץ')">קיץ</button>
      <button class="btn" onclick="next('season', 'סתיו')">סתיו</button>
      <button class="btn" onclick="next('season', 'חורף')">חורף</button>
    </div>
  </div>

  <div class="question" id="question4" style="display:none;">
    <p>איפה אתה מעדיף לטייל?</p>
    <div class="btn-group">
      <button class="btn" onclick="next('travel', 'עירוני')">עירוני</button>
      <button class="btn" onclick="next('travel', 'טבע')">טבע</button>
      <button class="btn" onclick="next('travel', 'חוף')">חוף</button>
    </div>
  </div>

  <div class="question" id="question5" style="display:none;">
    <p>איזה מוזיקה אתה שומע?</p>
    <div class="btn-group">
      <button class="btn" onclick="next('music', 'פופ')">פופ</button>
      <button class="btn" onclick="next('music', 'רוק')">רוק</button>
      <button class="btn" onclick="next('music', 'אלקטרוני')">אלקטרוני</button>
      <button class="btn" onclick="next('music', 'מזרחית')">מזרחית</button>
      <button class="btn" onclick="next('music', 'ג׳אז')">ג׳אז</button>
    </div>
  </div>

  <div class="question" id="question6" style="display:none;">
    <p>מה הטעם האהוב עליך בקוקטייל?</p>
    <div class="btn-group">
      <button class="btn" onclick="finish('מתוק')">מתוק</button>
      <button class="btn" onclick="finish('מריר')">מריר</button>
      <button class="btn" onclick="finish('חמוץ')">חמוץ</button>
      <button class="btn" onclick="finish('מרענן')">מרענן</button>
      <button class="btn" onclick="finish('חזק')">חזק</button>
    </div>
  </div>

  <div class="result" id="result" style="display:none;"></div>
  <div class="footer">כל הזכויות שמורות לדני</div>

  <script>
    const answers = {};

    const cocktails = {
      אביב: {
        מתוק: "פלומה",
        מריר: "נגרוני",
        חמוץ: "מרגריטה (אשכוליות)",
        מרענן: "מוחיטו",
        חזק: "וודקה מרטיני"
      },
      קיץ: {
        מתוק: "אורגזמה",
        מריר: "ג׳זמין",
        חמוץ: "דקירי",
        מרענן: "אפרול שפריץ",
        חזק: "קובה ליברה"
      },
      סתיו: {
        מתוק: "קלובר קלאב",
        מריר: "בול ורדיאר",
        חמוץ: "אמרטו סוואר",
        מרענן: "דקירי 2",
        חזק: "ראסטי נייל"
      },
      חורף: {
        מתוק: "וויט ראשן",
        מריר: "סייד קאר (גרסה נוספת)",
        חמוץ: "סייד קאר",
        מרענן: "גפאניס",
        חזק: "אולד פאשן"
      }
    };

    function next(key, value) {
      answers[key] = value;
      const current = document.querySelector(`#question${Object.keys(answers).length}`);
      const next = document.querySelector(`#question${Object.keys(answers).length + 1}`);
      if (current) current.style.display = 'none';
      if (next) next.style.display = 'block';
    }

    function finish(taste) {
      answers['taste'] = taste;
      document.querySelector('#question6').style.display = 'none';
      const season = answers['season'];
      const result = cocktails[season]?.[taste] || "מוסקו מיול";
      document.querySelector('#result').style.display = 'block';
      document.querySelector('#result').innerHTML = `הקוקטייל שלך הוא: <strong>${result}</strong>`;
    }
  </script>
</body>
</html>
