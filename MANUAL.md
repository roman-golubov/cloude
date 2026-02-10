# 🚀 Руководство по командам агентов Claude Code

## ⚡ Quick Start - Самые частые команды

```bash
# Планирование новой задачи
/planner Реализовать фильтрацию в таблице пользователей по роли и статусу

# Запустить inspection-app
/nx-runner serve inspection-app-inspection

# Быстрый коммит
/git-helper commit

# Проверить и исправить код
/linter fix

# Review изменений
/pr-review
```

---

## 📝 PLANNER - Планировщик задач

### Базовое использование
```bash
# Создать план из Jira задачи
/planner STR-2303: Implement user import from CSV. Should validate emails, check duplicates, show progress

# С дополнительными указаниями
/planner STR-2303: Add export to Excel. Сделай как в админке для экспорта assets, используй тот же компонент ExcelExporter

# Продолжить выполнение существующего плана
/planner resume ticket-STR-2303.md

# Проверить статус выполнения плана
/planner check ticket-STR-2303.md
```

### Примеры реальных Jira задач
```bash
# Пример 1: Новая фича
/planner
Title: Add bulk operations for inspections
Description: Users should be able to select multiple inspections and perform bulk actions
AC:
- Checkbox selection in table
- Bulk delete with confirmation
- Bulk status change
- Show selected count
Подсказка: посмотри как сделано в workshop-app для work orders

# Пример 2: Баг фикс
/planner
STR-2234 BUG: Date picker shows wrong timezone
Steps to reproduce:
1. Open inspection form
2. Select date
3. Save and reload
Expected: Same date
Actual: Date shifted by timezone
Подсказка: проблема в компоненте DateSelector, нужно использовать dayjs с правильной timezone
```

---

## 🚀 NX-RUNNER - Управление проектами

### Запуск dev серверов
```bash
# Запустить конкретное приложение
/nx-runner serve inspection-app-inspection    # Port 4200
/nx-runner serve admin-panel                  # Port 4201
/nx-runner serve tenant-management            # Port 4202
/nx-runner serve freeway-app                  # Port 4203
/nx-runner serve workshop-app                  # Найдёт свободный порт

# Проверить запущенные серверы
/nx-runner status

# Остановить сервер
/nx-runner stop [shell_id]
```

### Сборка проектов
```bash
# Собрать один проект
/nx-runner build inspection-app-inspection

# Собрать все проекты
/nx-runner build all

# Собрать только изменённые (affected)
/nx-runner build affected

# Production сборка
/nx-runner build inspection-app-inspection --prod

# Сборка без кеша (force rebuild)
/nx-runner build admin-panel --skip-cache
```

### Тестирование
```bash
# Запустить тесты
/nx-runner test inspection-app-inspection

# Тесты с покрытием
/nx-runner test inspection-app-inspection --coverage

# Тесты в watch режиме
/nx-runner test inspection-app-inspection --watch

# Тесты для изменённых файлов
/nx-runner test affected
```

### Утилиты
```bash
# Очистить кеш Nx
/nx-runner reset

# Показать граф зависимостей
/nx-runner dep-graph

# Анализ бандла
/nx-runner analyze freeway-app

# Линтинг через Nx
/nx-runner lint inspection-app-inspection
```

---

## 🔧 GIT-HELPER - Git операции

### Работа с ветками
```bash
# Создать новую feature ветку
/git-helper создай ветку для новой фичи user-import

# Переключиться на ветку
/git-helper checkout task/STR-2303

# Показать все ветки
/git-helper branches

# Удалить ветку
/git-helper delete branch feature-old

# Обновить из master
/git-helper pull master
```

### Коммиты
```bash
# Умный коммит (анализирует изменения из контекста)
/git-helper commit

# Коммит с сообщением
/git-helper commit "Fix date picker timezone issue"

# Посмотреть что будет закоммичено
/git-helper status

# Добавить файлы и закоммитить
/git-helper add and commit

# Amend последний коммит
/git-helper amend
```

### Управление изменениями
```bash
# Спрятать изменения
/git-helper stash

# Вернуть изменения из stash
/git-helper stash pop

# Посмотреть diff
/git-helper diff

# Отменить изменения в файле
/git-helper restore file.ts

# Reset к предыдущему коммиту
/git-helper reset --soft HEAD~1
```

### Merge и Rebase
```bash
# Смержить ветку
/git-helper merge feature-branch

# Rebase на master
/git-helper rebase master

# Cherry-pick коммита
/git-helper cherry-pick abc123

# Разрешить конфликты
/git-helper resolve conflicts
```

---

## 🔍 PR-REVIEW - Проверка кода

### Базовые проверки
```bash
# Review текущих изменений (против master)
/pr-review

# Review конкретного PR (через gh cli)
/pr-review 123

# Review определённых файлов
/pr-review check components folder only

# Строгая проверка (более детальная)
/pr-review strict
```

### Специализированные проверки
```bash
# Проверка только TypeScript типов
/pr-review types only

# Проверка производительности
/pr-review performance focus

# Проверка безопасности
/pr-review security audit

# Проверка React best practices
/pr-review react patterns
```

---

## ✨ LINTER - Проверка качества кода

### Быстрые команды
```bash
# Проверить inspection-app (default)
/linter

# Проверить другое приложение
/linter workshop-app

# Автоматически исправить все проблемы
/linter fix

# Только проверка без исправлений
/linter check
```

### Режимы работы
```bash
# Строгая проверка (все правила)
/linter strict

# Проверка только TypeScript
/linter typescript

# Проверка форматирования
/linter format

# Проверка и исправление конкретной папки
/linter fix components/UserImport
```

---

## 🎯 Комбо - Типовые workflow

### Новая задача из Jira
```bash
# 1. Планирование
/planner [вставить текст из Jira]

# 2. Создать ветку
/git-helper создай ветку STR-2303

# 3. Запустить dev сервер
/nx-runner serve inspection-app-inspection

# 4-7. Разработка по плану...

# 8. Проверка качества
/linter fix

# 9. Тесты
/nx-runner test inspection-app-inspection

# 10. Коммит
/git-helper commit

# 11. Финальная проверка
/pr-review
```

### Быстрый багфикс
```bash
# 1. Переключиться на ветку
/git-helper checkout hotfix/date-bug

# 2. Быстрая проверка
/linter check

# 3. Исправить и проверить
/nx-runner test affected

# 4. Коммит
/git-helper commit "Fix date timezone issue"

# 5. Review
/pr-review
```

### Рефакторинг компонента
```bash
# 1. План рефакторинга
/planner Refactor UserTable component to use hooks instead of class

# 2. Запустить тесты в watch mode
/nx-runner test inspection-app-inspection --watch

# 3. После рефакторинга
/linter fix
/pr-review performance focus
/git-helper commit
```

### Параллельная работа
```bash
# Запустить несколько агентов одновременно
/nx-runner serve inspection-app-inspection & /nx-runner test inspection-app-inspection --watch

# Проверить всё перед коммитом
/linter fix & /pr-review & /nx-runner test affected
```

---

## 💡 Полезные советы

### Для Planner
- Вставляй полный текст из Jira, включая Acceptance Criteria
- Добавляй подсказки типа "сделай как в админке"
- Для больших задач план сохранится в файл автоматически

### Для Nx-Runner
- Используй `status` чтобы видеть запущенные процессы
- Dev серверы запускаются в фоне, не блокируют консоль
- При проблемах со сборкой используй `/nx-runner reset`

### Для Git-Helper
- Агент видит контекст твоей работы для умных коммитов
- Всегда делает `git pull` перед коммитом
- Автоматически исключает `routing.helper.ts`

### Для PR-Review
- Фокусируется только на Frontend коде
- Игнорирует Java/backend файлы
- Работает изолированно, не засоряет контекст

### Для Linter
- `fix` исправляет большинство проблем автоматически
- Запускает ESLint, Prettier и TypeScript проверки
- После `fix` могут остаться проблемы требующие ручного исправления

---

## 🔥 Горячие клавиши (псевдонимы)

Можешь создать короткие алиасы в `.claude/skills/` для частых команд:

```bash
# Быстрый старт дня
/start → /git-helper pull && /nx-runner serve inspection-app-inspection

# Быстрая проверка перед коммитом
/check → /linter fix && /nx-runner test affected && /pr-review

# Быстрый коммит и пуш
/ship → /git-helper commit && /git-helper push
```

---

## 📚 Дополнительно

- Все агенты работают в изоляции (кроме git-helper)
- Планы сохраняются в `.claude/plans/`
- Конфиги агентов в `.claude/skills/*/SKILL.md`
- Документация в `.claude/skills/README.md`

**Совет:** Начни с `/planner` для новой задачи - он создаст пошаговый план, который потом легко выполнить!