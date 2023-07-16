# Привет друг!
Если твоя нода ниже 16 то, сперва необходимо установить [NodeJS](https://nodejs.org/en/download/) 16 или выше.

**Обязательно** Для начала работы:

```sh
# установи зависимости
npm ci

# включить git hooks для проверки коммитов
npm prepare

```

## Проверка коммитов

Я настроила pre-commit hook. Чтобы его проверить, попробуй что либо закомитить не по conventional-commitlint.

## Workflow тестов

Workflow находиться тут [.github/workflows/testing.yml](https://github.com/Anakharsis9/ci-hw/actions/workflows/testing.yml)

Запускается на **pull request, и в других workflow**

Настроено ограничение на мерж изменений, если проверки не прошли на ветке *master*

Описание действий:

- Прогоняет unit тесты и статус выполнения записывает в env перменную unit_result
- создает ссылку на workflow и записывает в output
- Прогоняет e2e тесты и статус выполнения записывает в env перменную e2e_result
- Прогоняет проверку eslint и статус выполнения записывает в env перменную lint_result
- Все переменные записываются в output всего workflow, и будут доступны во время переиспользования.

## Workflow release

Workflow находиться тут [.github/workflows/release.yml](https://github.com/Anakharsis9/ci-hw/actions/workflows/release.yml)

Запускается на **при push релизного тега**

Закомить что нибудь и потом:
```sh
# добавь tag в релизном формате
git tag v28

# запушай tag
git push origin v28

```

Описание действий:

- запускает workflow тестов, получает статусы прогона тестов
- в любом случае (успешных/не успешных) тестов запускает создание issue
- issue создается по шаблону описанному в [.github/ISSUE_TEMPLATE.md](https://github.com/Anakharsis9/ci-hw/blob/master/.github/ISSUE_TEMPLATE.md)
- Будет создан issue RELEASE v28, c label **RELEASE**, в котором будет:
  
  - Автор
  - Версия
  - Дата и время создания
  - Changelog
  - Результаты автотестов

## Workflow deploy

Workflow находиться тут [.github/workflows/deploy.yml](https://github.com/Anakharsis9/ci-hw/actions/workflows/deploy.yml)

Запускается **вручную** (так Дима сам сказал делать). Чтобы запустить перейди в сам workflow по ссылке выше и нажми справа с боку на **Run workflow**

Описание действий:

- запускает билд
- с помощью action JamesIves/github-pages-deploy-action@v4 собирается билд для gh-pages
- получает последний актуальный релизный тег
- находит такой issue
- добавляет комментарий "Deployed to https://anakharsis9.github.io/ci-hw/"
- закрывает issue

На этом все, дорогой друг, если будут непонятки и комментарии, напиши мне в телеге [https://t.me/anakharsis19](https://t.me/anakharsis19)
