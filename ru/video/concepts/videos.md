# Видео в сервисе {{ video-name }}

С помощью {{ video-name }} вы можете загружать на [канал](index.md#channels) _видео_ для дальнейшей публикации на внешних ресурсах.

{% include [video-characteristic](../../_includes/video/video-characteristic-multiple.md) %}

В сервисе действуют [ограничения](limits.md) на разрешение публикуемых видео.

Для видео доступна загрузка пользовательских обложек. Обложка будет отображаться в интерфейсе {{ video-name }}, а также в [плеере](./player.md) на сайте, где размещено видео.

{% include [image-characteristic](../../_includes/video/image-characteristic.md) %}

Вы можете [опубликовать](../operations/video/get-link.md) по прямой ссылке или разместить на сайте как одиночные видео, так и видео, сгруппированные в [плейлисты](playlists.md) в определенной последовательности. Подробнее о публикации плейлистов см. в разделе [{#T}](../operations/playlists/get-link.md).

## Статусы {#statuses}

### Статусы видео {#video-statuses}

* `{{ ui-key.yacloud_video.videos.status_wait-uploading }}` — исходный файл с видео загружается в хранилище {{ yandex-cloud }}.
* `{{ ui-key.yacloud_video.videos.status_processing }}` — исходный файл с видео транскодируется в несколько вариантов видео с различным битрейтом и разрешением. При дальнейшем просмотре видео на клиентских устройствах видеоплеер подбирает оптимальный вариант для плавного воспроизведения при текущей скорости интернет-соединения.
* `{{ ui-key.yacloud_video.videos.status_ready }}` — транскодирование выполнено, видео готово к просмотру.
* `{{ ui-key.yacloud_video.videos.status_error }}` — ошибка при загрузке файла или транскодировании видео. Проверьте стабильность интернет-соединения, целостность файла, его формат и повторите попытку.

### Статусы публикации {#publication-statuses}

* `{{ ui-key.yacloud_video.videos.status_published }}` — видео [опубликовано](../operations/video/publish.md).
* `{{ ui-key.yacloud_video.videos.status_unpublished }}` — видео не опубликовано.

## Параметры публикации видео {#video-parameters}

Вы можете изменять следующие базовые настройки воспроизведения видео при [генерации](../operations/video/get-link.md) прямой ссылки или кода для вставки видео на сайт:

* установка по умолчанию для воспроизведения звука при проигрывании;
* автоматический запуск воспроизведения при открытии;
* отображение элементов управления видео в плеере.

{% include [iframe-settings](../../_includes/video/iframe-settings.md) %}

## Статистика просмотров видео {#video-statistics}

Для каждого видео вы можете [посмотреть статистику](../operations/video/get-statistics.md) просмотров с возможностью гибко настроить период расчета статистики.

В настоящее время доступны следующие статистические показатели просмотров:

* количество просмотров — целое число;
* доля просмотренного контента — процентное соотношение средней длительности просмотра к длительности видео;
* общее время просмотра — суммарная длительность просмотров в часах и минутах;
* средняя длительность просмотра — средняя длительность просмотра в часах и минутах;
* линейная диаграмма с распределением количества просмотров на единицу времени со следующими уровнями дискретизации:

    * `5 минут`
    * `1 час`
    * `1 день`
* круговая диаграмма с распределением просмотров по типам операционных систем устройств;
* круговая диаграмма с распределением просмотров по типам устройств.
* [тепловая карта](https://ru.wikipedia.org/wiki/Тепловая_карта) с данными о просмотрах фрагментов видео.

    Каждая точка на тепловой карте соответствует 30-секундному фрагменту видео.

    Просмотром на тепловой карте считается факт воспроизведения фрагмента видео, независимо от продолжительности воспроизведения. Например, если вы запустили видео и сразу же остановили его, то для первого фрагмента видео будет засчитан просмотр.