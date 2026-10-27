---
name: workflow-check
description: Проверь workflow GitHub Actions перед коммитом — права токена, секреты в журнале и версии действий. Вызывай, когда просят «проверь workflow», перед коммитом файла из .github/workflows/.
---

# Проверка workflow

Проверь каждый файл `.github/workflows/*.yml`, который назвал пользователь.

## Правила

1. В файле есть строка `permissions:` — на уровне всего workflow или у каждого задания.
2. Нигде нет `write-all` и `read-all`.
3. Права `write` (`contents: write`, `pages: write`, `issues: write`, `id-token: write`) заданы у задания, которому нужна запись, а не у всего workflow.
4. Нет шага, который печатает секрет: `echo` со `${{ secrets.… }}` или с `GH_TOKEN`.
5. Мажоры действий после `@` — как в курсе: `actions/checkout@v7`, `actions/setup-node@v7`, `actions/upload-pages-artifact@v5`, `actions/deploy-pages@v5`.

## Ответ

Одна строка на файл:
- `принято: <файл>` — если все правила выполнены;
- `отказ: <файл> — <номер правила>: <что не так, строка>` — если хотя бы одно нарушено.

Файлы не правь: решение о правке принимает пользователь.
