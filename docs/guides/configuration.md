# Оптимизированная конфигурация `mkdocs.yml`

Ниже приведены ключевые настройки с комментариями, ориентированные на удобство чтения, поиск и поддержку. Все параметры совместимы с актуальной версией MkDocs Material.

## Основные блоки конфигурации

```yaml
site_name: "База знаний компании"
site_description: "Внутренний портал с инструкциями, стандартами и практиками"
site_url: "https://knowledge.example.com"  # заполните после выбора домена

theme:
  name: material
  language: ru
  features:
    - navigation.tabs         # верхний бар с разделами
    - navigation.sections     # группировка страниц в секции в сайдбаре
    - navigation.instant      # мгновенная загрузка страниц без перезагрузки
    - navigation.top          # кнопка «вверх» в правом нижнем углу
    - toc.integrate           # оглавление встроено в левое меню
    - search.suggest          # подсказки в поиске
    - search.highlight        # подсветка совпадений
    - content.code.copy       # кнопка «скопировать» в блоках кода
    - content.tabs.link       # синхронизация вкладок по якорям
  palette:
    - scheme: default
      primary: blue
      accent: indigo
      toggle:
        icon: material/weather-night
        name: Переключиться на тёмную тему
    - scheme: slate
      primary: blue
      accent: indigo
      toggle:
        icon: material/weather-sunny
        name: Переключиться на светлую тему

plugins:
  - search:
      lang: [ru, en]          # русско-английский индекс
  - tags                      # облако и страницы тегов
  - git-revision-date-localized:
      enable_creation_date: true
      type: datetime          # отображать дату и время
      fallback_to_build_date: true
  - section-index             # файлы index.md для разделов

markdown_extensions:
  - admonition
  - pymdownx.details
  - pymdownx.superfences:
      custom_fences:
        - name: mermaid       # поддержка диаграмм
          class: mermaid
          format: !!python/name:pymdownx.superfences.fence_code_format
  - pymdownx.tabbed:
      alternate_style: true
  - pymdownx.highlight:
      anchor_linenums: true
      linenums: true
  - pymdownx.inlinehilite
  - pymdownx.emoji:
      emoji_generator: !!python/name:material.extensions.emoji.to_svg
      emoji_index: !!python/name:material.extensions.emoji.twemoji

extra_css:
  - assets/stylesheets/extra.css
```

## Назначение и преимущества

- **Темы и палитры:** светлая/тёмная схемы улучшают доступность и дают пользователям выбор. Настраиваемые primary/accent цвета сохраняют фирменный стиль.
- **Навигационные фичи:** быстрый переход к разделам, встроенное оглавление и кнопка «наверх» ускоряют скролл длинных страниц.
- **Поиск:** двуязычный индекс упрощает нахождение терминов на русском и английском. Подсветка совпадений экономит время чтения.
- **Метаданные Git:** дата изменения помогает отслеживать актуальность материалов и облегчает аудит.
- **Расширения Markdown:** вкладки, подробности (details) и диаграммы делают документацию более выразительной и компактной.

## Производительность и поддерживаемость

- Используйте `navigation.instant` и `search.suggest` для ускорения работы на клиенте; при большом количестве страниц регулярно прогоняйте `mkdocs build` для контроля размера итогового бандла.
- Следите, чтобы указанные плагины были установлены в окружении (`pip install mkdocs-material mkdocs-section-index mkdocs-git-revision-date-localized-plugin`).
- При доработке цветовых схем меняйте только `primary`/`accent`, чтобы сохранить единообразие UI.
