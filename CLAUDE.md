# Основные настройки проекта

## Модели и агенты
- **Планирование задач**: `/planner` - превращает Jira в детальные планы
- **Сборка и запуск**: `/nx-runner` - управление Nx командами
- **Git операции**: `/git-helper` - коммиты, ветки, merge
- **Code review**: `/pr-review` - проверка качества кода
- **Linting**: `/linter` - автоматические проверки

## Основные правила
- Общение на русском, комментарии в коде только на английском
- Фокус только на Frontend (TypeScript/React), игнорировать Java/backend
- Использовать TodoWrite для планирования сложных задач
- Не добавлять emoji в console.logs

## Tech Stack
- **Frontend**: React 18, TypeScript, Nx (monorepo), Material-UI, Ant Design, SCSS
- **State**: Redux Toolkit, Context API
- **Mobile**: Capacitor для Android/iOS
- **Auth**: AWS Amplify Auth, Azure MSAL
- **Testing**: Jest, React Testing Library, Cypress
- **Build**: Nx, Webpack

## Структура проекта
```
webapps/
├── apps/
│   ├── inspection-app/        # Основное приложение (DWA)
│   ├── workshop-app/          # Приложение для мастерских
│   ├── freeway-app/           # Freeway приложение
│   ├── admin-panel/           # Админ панель
│   └── fleet-management/      # Управление флотом
├── libs/
│   ├── common/                # Общие компоненты и утилиты
│   ├── auth-amplify/          # AWS Amplify авторизация
│   ├── auth-nfc/              # NFC логин
│   └── auth-offline/          # Offline авторизация
└── [конфиги: nx.json, tsconfig.json, jest.config.ts]
```

## Рекомендации по коду
- Functional components с TypeScript
- async/await вместо promise chains
- Ant Design компоненты для UI
- Cleanup в useEffect где необходимо

## Workflow с агентами

### Новая задача из Jira:
1. `/planner [текст из Jira]` - создаст детальный план
2. `/git-helper` - создаст ветку
3. `/nx-runner serve [app]` - запустит dev сервер
4. Выполняй план пошагово
5. `/linter` - проверит качество
6. `/nx-runner test` - прогонит тесты
7. `/git-helper commit` - создаст коммит
8. `/pr-review` - финальная проверка

### Быстрые команды:
- `/nx-runner` - для любых Nx операций (serve, build, test)
- `/planner` - для планирования сложных задач

Детальные инструкции в `.claude/skills/README.md`