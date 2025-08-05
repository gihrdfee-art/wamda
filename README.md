# wamda
استوديو رقمي لتصميم الفصول، الصور، والقصص التفاعلية بأسلوب احترافي ومرن.
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>StudioMBA – Image Manager</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      background-color: #f2f2f2;
      padding: 20px;
      margin: 0;
      direction: rtl;
    }

    .container {
      max-width: 700px;
      margin: auto;
      background-color: #fff;
      padding: 25px;
      border-radius: 12px;
      box-shadow: 0 4px 12px rgba(0, 0, 0, 0.1);
    }

    h1, h2 {
      text-align: center;
      color: #333;
    }

    form {
      display: flex;
      flex-direction: column;
      gap: 12px;
    }

    input[type="file"],
    input[type="text"] {
      padding: 10px;
      border-radius: 6px;
      border: 1px solid #ccc;
    }

    button {
      padding: 10px;
      background-color: #4CAF50;
      color: white;
      border: none;
      border-radius: 6px;
      cursor: pointer;
      font-size: 16px;
    }

    button:hover {
      background-color: #45a049;
    }

    #gallery {
      margin-top: 30px;
    }

    .image-box {
      background-color: #fafafa;
      padding: 15px;
      border: 1px solid #ddd;
      border-radius: 10px;
      margin-bottom: 20px;
      text-align: center;
    }

    .image-box img {
      max-width: 100%;
      height: auto;
      border-radius: 6px;
      margin-bottom: 10px;
    }

    .download-btn {
      display: inline-block;
      margin-top: 8px;
      padding: 6px 12px;
      background-color: #2196F3;
      color: white;
      text-decoration: none;
      border-radius: 6px;
      font-size: 14px;
    }

    .download-btn:hover {
      background-color: #1976D2;
    }
  </style>
</head>
<body>
  <div class="container">
    <h1>📸 StudioMBA – مركز إدارة الصور</h1>

    <form id="uploadForm">
      <label for="imageInput">اختر صورة من جهازك:</label>
      <input type="file" id="imageInput" accept="image/*" required />

      <label for="imageName">اسم الصورة:</label>
      <input type="text" id="imageName" placeholder="أدخل اسم الصورة" required />

      <button type="submit">📤 رفع الصورة</button>
    </form>

    <hr />

    <div id="gallery">
      <h2>🖼️ المعرض</h2>
      <!-- سيتم عرض الصور هنا -->
    </div>
  </div>

  <script>
    const uploadForm = document.getElementById('uploadForm');
    const imageInput = document.getElementById('imageInput');
    const imageName = document.getElementById('imageName');
    const gallery = document.getElementById('gallery');

    function saveToLocalStorage(imageData) {
      const existing = JSON.parse(localStorage.getItem('images') || '[]');
      existing.push(imageData);
      localStorage.setItem('images', JSON.stringify(existing));
    }

    window.addEventListener('load', function () {
      const savedImages = JSON.parse(localStorage.getItem('images') || '[]');
      savedImages.forEach((data) => {
        const imageBox = document.createElement('div');
        imageBox.className = 'image-box';

        const img = document.createElement('img');
        img.src = data.url;
        img.alt = data.name;

        const caption = document.createElement('p');
        caption.textContent = `📌 ${data.name}`;

        const downloadBtn = document.createElement('a');
        downloadBtn.href = data.url;
        downloadBtn.download = data.name;
        downloadBtn.textContent = '⬇️ تحميل';
        downloadBtn.className = 'download-btn';

        imageBox.appendChild(img);
        imageBox.appendChild(caption);
        imageBox.appendChild(downloadBtn);

        gallery.appendChild(imageBox);
      });
    });

    uploadForm.addEventListener('submit', function (e) {
      e.preventDefault();

      const file = imageInput.files[0];
      const name = imageName.value.trim();

      if (!file || !name) {
        alert('يجب اختيار صورة وإدخال اسم.');
        return;
      }

      const reader = new FileReader();
      reader.onload = function (event) {
        const imageURL = event.target.result;

        const imageBox = document.createElement('div');
        imageBox.className = 'image-box';

        const img = document.createElement('img');
        img.src = imageURL;
        img.alt = name;

        const caption = document.createElement('p');
        caption.textContent = `📌 ${name}`;

        const downloadBtn = document.createElement('a');
        downloadBtn.href = imageURL;
        downloadBtn.download = name;
        downloadBtn.textContent = '⬇️ تحميل';
        downloadBtn.className = 'download-btn';

        imageBox.appendChild(img);
        imageBox.appendChild(caption);
        imageBox.appendChild(downloadBtn);

        gallery.appendChild(imageBox);

        saveToLocalStorage({ name: name, url: imageURL });

        uploadForm.reset();
      };

      reader.readAsDataURL(file);
    });
  </script>
</body>
</html>
