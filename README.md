<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>AI Bio Generator - مولد السير الذاتية الذكي</title>
  <style>
    body {
      font-family: 'Arial', sans-serif;
      background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
      margin: 0;
      padding: 20px;
      color: #333;
      text-align: center;
    }
    .container {
      max-width: 800px;
      margin: 0 auto;
      background: white;
      padding: 40px;
      border-radius: 15px;
      box-shadow: 0 10px 30px rgba(0,0,0,0.2);
    }
    h1 {
      color: #764ba2;
      margin-bottom: 30px;
    }
    form {
      display: flex;
      flex-direction: column;
      gap: 15px;
      margin-bottom: 30px;
    }
    input, select {
      padding: 10px;
      border: 1px solid #ddd;
      border-radius: 5px;
      font-size: 16px;
    }
    button {
      background: #667eea;
      color: white;
      padding: 12px;
      border: none;
      border-radius: 5px;
      cursor: pointer;
      font-size: 18px;
      transition: background 0.3s;
    }
    button:hover {
      background: #764ba2;
    }
    .results {
      display: none;
      text-align: right;
    }
    .bio-option {
      background: #f9f9f9;
      padding: 20px;
      margin: 20px 0;
      border-radius: 10px;
      border-left: 5px solid #667eea;
    }
    .bio-option h3 {
      color: #667eea;
      margin-top: 0;
    }
    .char-count {
      font-size: 12px;
      color: #888;
    }
    @media (max-width: 600px) {
      .container {
        padding: 20px;
      }
    }
  </style>
</head>
<body>
  <div class="container">
    <h1>🤖 AI Bio Generator</h1>
    <p>أدخل معلوماتك لإنشاء سيرة ذاتية قصيرة احترافية مخصصة لمنصتك المفضلة. سنولد لك 3 خيارات مختلفة في ثوانٍ!</p>
    
    <form id="bioForm">
      <input type="text" id="name" placeholder="اسمك (مثال: أحمد محمد)" required>
      <input type="text" id="field" placeholder="تخصصك أو وظيفتك (مثال: مطور برمجيات)" required>
      <select id="tone" required>
        <option value="">اختر نبرة الأسلوب</option>
        <option value="احترافي">احترافي</option>
        <option value="مرح">مرح</option>
        <option value="ملهم">ملهم</option>
        <option value="إبداعي">إبداعي</option>
      </select>
      <select id="platform" required>
        <option value="">اختر المنصة</option>
        <option value="Twitter">Twitter (≤150 حرف)</option>
        <option value="Instagram">Instagram (≤150 حرف)</option>
        <option value="LinkedIn">LinkedIn (≤300 حرف)</option>
        <option value="TikTok">TikTok (≤150 حرف)</option>
        <option value="Personal Website">موقع شخصي (≤400 حرف)</option>
      </select>
      <button type="submit">ولّد السيرة الذاتية الآن!</button>
    </form>
    
    <div id="results" class="results">
      <h2>إليك 3 خيارات مخصصة:</h2>
      <div id="bio1" class="bio-option"></div>
      <div id="bio2" class="bio-option"></div>
      <div id="bio3" class="bio-option"></div>
    </div>
  </div>

  <script>
    document.getElementById('bioForm').addEventListener('submit', function(e) {
      e.preventDefault();

      const name = document.getElementById('name').value;
      const field = document.getElementById('field').value;
      const tone = document.getElementById('tone').value;
      const platform = document.getElementById('platform').value;

      if (!name || !field || !tone || !platform) {
        alert('يرجى ملء جميع الحقول!');
        return;
      }

      const templates = {
        "احترافي": {
          short: `${name} | ${field} متميز بخبرة واسعة. أسعى للابتكار والكفاءة.`,
          medium: `${name} | خبير في ${field}. أبني حلولاً رقمية مستدامة وأربط الأفكار بالنتائج.`,
          long: `في مجال ${field}، ${name} هو الشريك المثالي للمشاريع الرقمية. أركز على الجودة والابتكار لنصنع الفرق معًا.`
        },
        "مرح": {
          short: `هلا! أنا ${name}، ${field} يحب القهوة والتحديات 😎.`,
          medium: `مرحباً! ${name} هنا، ${field} بأسلوب مرح يحول الأفكار إلى واقع ممتع 😉.`,
          long: `أنا ${name}، ${field} اللي بيضيف لمسة مرح على كل مشروع ☕🎉.`
        },
        "ملهم": {
          short: `${name} | ${field} يلهم التغيير. كل فكرة تبدأ بخطوة!`,
          medium: `${name} في عالم ${field} هو الشرارة. أبني جسورًا للمستقبل ✨.`,
          long: `${name}، ${field} شغوف بالإلهام. أؤمن أن كل تحدي فرصة للنمو.`
        },
        "إبداعي": {
          short: `${name} | ${field} إبداعي يرسم المستقبل 🎨.`,
          medium: `أنا ${name}، ${field} يمزج الخيال بالواقع. أفكاري تتدفق كالنهر.`,
          long: `مع ${name}، ${field} يصبح فنًا. أستخدم الإبداع لأحول الأحلام إلى واقع.`
        }
      };

      const template = templates[tone];
      const maxLength =
        platform.includes('Twitter') || platform.includes('Instagram') || platform.includes('TikTok')
          ? 150
          : platform.includes('LinkedIn')
          ? 300
          : 400;

      const bio1 = template.short.slice(0, maxLength);
      const bio2 = template.medium.slice(0, maxLength);
      const bio3 = template.long.slice(0, maxLength);

      document.getElementById('bio1').innerHTML = `<h3>خيار 1: ${tone} قصير</h3><p>${bio1}</p><div class="char-count">مناسب لـ ${platform}</div>`;
      document.getElementById('bio2').innerHTML = `<h3>خيار 2: ${tone} متوسط</h3><p>${bio2}</p><div class="char-count">مناسب لـ ${platform}</div>`;
      document.getElementById('bio3').innerHTML = `<h3>خيار 3: ${tone} مفصل</h3><p>${bio3}</p><div class="char-count">مناسب لـ ${platform}</div>`;

      document.getElementById('results').style.display = 'block';
      document.getElementById('results').scrollIntoView({ behavior: 'smooth' });
    });
  </script>
</body>
</html>
