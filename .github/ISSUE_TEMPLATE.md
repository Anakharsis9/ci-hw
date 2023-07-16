---
title: RELEASE {{ env.version }}
labels: RELEASE
---
- Автор релиза: {{ env.author }}
- Версия: {{ env.version }}
- Дата и время создания: {{ env.creation_date }}
- Changelog:

{{ env.changelog }}

- Результаты автотестов:
  - Unit тесты: {{ env.unit_result }}
  - E2e тесты: {{ env.e2e_result }}
  - Eslint: {{ env.lint_result }}
