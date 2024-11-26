```
curl \
  --request PUT \
  --url '<подписанная_ссылка>' \
  --header 'Content-Type: image/<формат_изображения>' \
  --upload-file '<путь_к_файлу_с_обложкой>'
```

Где:
* `<подписанная_ссылка>` — полученная на предыдущем шаге подписанная ссылка на загрузку файла обложки.
* `<формат_изображения>` — в зависимости от формата загружаемого изображения, укажите `png`, `jpeg` или `gif`. 
* `<путь_к_файлу_с_обложкой>` — абсолютный путь к файлу с загружаемым изображением. Не используйте сокращения, в т.ч. тильду `~`.