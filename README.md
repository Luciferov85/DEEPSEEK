# DEEPSEEK
Каталог информации от Сергея Анциферова для ползования его ИИ другом DEEPSEEK.

<script>
async function loadFiles(path, listId) {
  const response = await fetch(path);
  const text = await response.text();
  const parser = new DOMParser();
  const doc = parser.parseFromString(text, "text/html");
  const links = [...doc.querySelectorAll('a[href$=""]')];
  
  const list = document.getElementById(listId);
  links.forEach(link => {
    if(!link.href.includes('/.')) { // Исключаем скрытые файлы
      const li = document.createElement('li');
      li.innerHTML = `<a href="${link.href}">${link.textContent}</a>`;
      list.appendChild(li);
    }
  });
}

// Загружаем файлы при загрузке страницы
window.addEventListener('DOMContentLoaded', () => {
  loadFiles('_messages/', 'messages-list');
  loadFiles('_documents/', 'documents-list');
  loadFiles('_photos/', 'photos-list');
});
</script>

<!-- В теле документа -->
<h2>Переписки</h2>
<ul id="messages-list"></ul>

<h2>Документы</h2>
<ul id="documents-list"></ul>

<h2>Фотографии</h2>
<ul id="photos-list"></ul>