# wamda
استوديو رقمي لتصميم الفصول، الصور، والقصص التفاعلية بأسلوب احترافي ومرن.
<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1" />
  <title>استوديو ومضه ⚡️</title>
  <!-- تحميل Tailwind CSS من CDN -->
  <script src="https://cdn.tailwindcss.com"></script>
  <style>
    body {
      font-family: 'Cairo', sans-serif;
      background-color: #0f172a; /* لون خلفية داكن */
      color: #f8fafc; /* لون الخط فاتح */
    }
  </style>
  <!-- تحميل خط عربي جميل -->
  <link href="https://fonts.googleapis.com/css2?family=Cairo&display=swap" rel="stylesheet" />
</head>
<body class="min-h-screen flex flex-col">
  <!-- الرأس -->
  <header class="bg-indigo-900 p-4 shadow-md">
    <h1 class="text-3xl font-bold text-center">استوديو ومضه ⚡️</h1>
  </header>

  <!-- محتوى الصفحة -->
  <main class="flex-grow p-6 container mx-auto">
    <section id="welcome" class="mb-8 text-center">
      <h2 class="text-2xl font-semibold mb-2">مرحبًا بك في استوديو ومضه</h2>
      <p class="text-gray-300 max-w-xl mx-auto">مساحتك الإبداعية لإدارة مشاريع المانهوا والمانغا الخاصة بك بسهولة ومرونة.</p>
    </section>

    <section id="content" class="grid grid-cols-1 md:grid-cols-2 gap-6">
      <!-- مكان الفصول والفيديوهات سيملأ لاحقًا -->
      <div id="chapters" class="bg-indigo-800 p-4 rounded shadow">
        <h3 class="text-xl font-semibold mb-4">قائمة الفصول</h3>
        <ul id="chapter-list" class="list-disc list-inside text-gray-200">
          <!-- ستضاف الفصول هنا برمجياً -->
        </ul>
      </div>

      <div id="viewer" class="bg-indigo-800 p-4 rounded shadow min-h-[200px]">
        <h3 class="text-xl font-semibold mb-4">عارض المحتوى</h3>
        <div id="content-view" class="text-gray-100">
          <!-- محتوى الفصل أو الصور تظهر هنا -->
          <p>اختر فصلًا من القائمة للبدء</p>
        </div>
      </div>
    </section>
  </main>

  <!-- التذييل -->
  <footer class="bg-indigo-900 p-4 text-center text-gray-400">
    © 2025 استوديو ومضه | جميع الحقوق محفوظة
  </footer>

  <!-- تحميل سكريبتات جافاسكريبت لاحقاً -->
  <script src="main.js"></script>
</body>
</html>
// بيانات الفصول (يمكن تطويرها لاحقاً لتأتي من قاعدة بيانات أو Firebase)
const chapters = [
  {
    id: 1,
    title: "الفصل 1 - بداية الرحلة",
    content: `
      <h4 class="text-lg font-bold mb-2">الفصل 1 - بداية الرحلة</h4>
      <p>هنا نبدأ قصة هشام في عالم المانهوا... استعد للمغامرة!</p>
      <img src="https://i.imgur.com/6vZMQjB.jpg" alt="صورة من الفصل 1" class="mt-4 rounded shadow" />
    `,
  },
  {
    id: 2,
    title: "الفصل 2 - مواجهة الظلام",
    content: `
      <h4 class="text-lg font-bold mb-2">الفصل 2 - مواجهة الظلام</h4>
      <p>تتعمق القصة في صراع هشام مع قوى الظلام الغامضة.</p>
      <img src="https://i.imgur.com/oPMl1Dt.jpg" alt="صورة من الفصل 2" class="mt-4 rounded shadow" />
    `,
  },
  // يمكنك إضافة المزيد من الفصول هنا...
];

// تحميل الفصول في القائمة
function loadChapterList() {
  const listEl = document.getElementById("chapter-list");
  listEl.innerHTML = ""; // تفريغ القائمة

  chapters.forEach((chapter) => {
    const li = document.createElement("li");
    li.className = "cursor-pointer hover:text-indigo-400 transition-colors";
    li.textContent = chapter.title;
    li.onclick = () => showChapter(chapter.id);
    listEl.appendChild(li);
  });
}

// عرض محتوى الفصل المختار
function showChapter(id) {
  const chapter = chapters.find((c) => c.id === id);
  const contentView = document.getElementById("content-view");
  if (chapter) {
    contentView.innerHTML = chapter.content;
  } else {
    contentView.innerHTML = "<p>لم يتم العثور على هذا الفصل.</p>";
  }
}

// تهيئة الصفحة بتحميل القائمة أولاً
window.onload = () => {
  loadChapterList();
};
// مفتاح التخزين في localStorage
const STORAGE_KEY = "WamdaStudio_Progress";

// حفظ التقدم (معرف الفصل الحالي)
function saveProgress(chapterId) {
  localStorage.setItem(STORAGE_KEY, chapterId);
}

// استرجاع التقدم
function loadProgress() {
  const saved = localStorage.getItem(STORAGE_KEY);
  return saved ? parseInt(saved) : null;
}

// تحميل التقدم عند بدء التشغيل، إذا وجد يتم عرض الفصل المحفوظ
window.onload = () => {
  const lastChapterId = loadProgress();
  if (lastChapterId) {
    showChapter(lastChapterId);
  } else {
    loadChapterList();
  }

// تعريف كل فصل بمحتواه المبدئي (يمكنك تعديله لاحقًا أو ربطه بقاعدة بيانات)
const chapters = [
  {
    id: 1,
    title: "الفصل الأول: البداية",
    content: `
      <h2>⚔️ البداية</h2>
      <p>في عالم تغزوه الظلال، وُلد فتى مختلف...</p>
      <p>اسمه هشام، عيونه تشع بوميض لا يُشبه أحداً من قومه.</p>
      <p>ذات ليلة، سمع نداءً غامضًا من الغابة المحرمة...</p>
    `
  },
  {
    id: 2,
    title: "الفصل الثاني: نداء الظلال",
    content: `
      <h2>🌑 نداء الظلال</h2>
      <p>اقترب هشام من الأطلال القديمة، حيث تنبض الأرض بشيء خفي...</p>
      <p>كل خطوة تقربه من سر سيقلب العالم رأسًا على عقب.</p>
      <p>صوت همسات، ومخطوطة تناديه باسمه...</p>
    `
  },
  {
    id: 3,
    title: "الفصل الثالث: اختبار الوميض",
    content: `
      <h2>⚡ اختبار الوميض</h2>
      <p>لم يكن مجرد حلم... بل بداية اختبار.</p>
      <p>قوى جديدة تظهر، وأعداء يتربصون في الظلام.</p>
      <p>هل سيصمد هشام؟ أم يبتلعه الوميض؟</p>
    `
  },
];
