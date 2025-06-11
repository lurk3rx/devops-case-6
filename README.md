# Цифровая кафедра - Кейс 6


## 📌 О проекте
Проект демонстрирует настройку CI/CD для автоматического развертывания статического сайта (HTML+CSS) при каждом обновлении кода.

## 🌐 Живая демонстрация

[Открыть сайт на GitHub Pages](https://lurk3rx.github.io/devops-case-6/index.html)

## 🏗 Структура проекта
```
├── index.html # Главная страница
├── about.html # Страница "О нас"
├── contacts.html # Страница "Контакты"
├── styles/
│   └── main.css # Основные стили
├── img/
│   ├── ev5ia7rhrsm31.png
│   ├── ico.jpg
│   ├── ico.png
│   ├── IMG_8709.JPG
│   ├── IMG_8710.JPG
│   ├── IMG_8711.JPG
│   ├── IMG_8713.PNG
│   ├── IMG_8715.PNG
│   └── photo_2025-06-08_14-50-25.jpg
└── .github/
    └── workflows/
        └── deploy.yml # Конфигурация CI/CD
```

## ⚡ Как работает CI/CD
1. При push в ветку `main` запускается GitHub Actions
2. Workflow развертывает сайт на GitHub Pages
3. Обновления появляются на сайте в течение 1-2 минут

## 🚀 Инструкция по развертыванию

### 1. Клонирование репозитория
```bash
git clone https://github.com/lurk3rx/devops-case-6.git
cd devops-case-6
```
### 2. Настройка GitHub Pages
Перейдите в Settings → Pages

В разделе "Build and deployment":

Source: GitHub Actions

Static HTML → Confugre

Вставляем код из следующего пункта

Commit changes

Сохраните изменения

### 3. Настройка workflow
Файл .github/workflows/deploy.yml:

```yml
name: Deploy static content to Pages

on:
  push:
    branches: ["main"]

  workflow_dispatch:

permissions:
  contents: read
  pages: write
  id-token: write

concurrency:
  group: "pages"
  cancel-in-progress: false

jobs:
  deploy:
    environment:
      name: github-pages
      url: ${{ steps.deployment.outputs.page_url }}
    runs-on: ubuntu-latest
    steps:
      - name: Checkout
        uses: actions/checkout@v4
      - name: Setup Pages
        uses: actions/configure-pages@v5
      - name: Upload artifact
        uses: actions/upload-pages-artifact@v3
        with:
          path: '.'
      - name: Deploy to GitHub Pages
        id: deployment
        uses: actions/deploy-pages@v4
```

### 4. Проверка работы
Внесите изменения:

```bash
git add .
git commit -m "Обновление контента"
git push origin main
```

## 👑 Итог
Этот файл README содержит:
1. Полную инструкцию по настройке
2. Описание структуры проекта
3. Детали работы CI/CD
4. Актуальную конфигурацию workflow
