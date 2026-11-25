# Keepsake — Digital Agency Landing

**Live Demo:** https://tarasosypchuk.github.io/landing-keepsake-9lab/

---

## Про проєкт

Лендінг для цифрового брендингового агентства Keepsake. Зібраний на Vite + Pug + SCSS із автоматичною оптимізацією зображень, PostCSS-обробкою та CI/CD через GitHub Actions.

---

## Вимоги

- **Node.js** `20.x` LTS або новіша
- **npm** `10.x` або новіша

---

## Команди

| Команда | Що робить |
|---|---|
| `npm install` | Встановлює залежності та ініціалізує husky-хуки |
| `npm run dev` | Dev-сервер на `localhost:5173` з HMR |
| `npm run build` | Збірка в `dist/` |
| `npm run preview` | Перегляд збірки на `localhost:4173` |
| `npm run images` | Конвертація зображень у AVIF / WebP / JPEG через sharp |
| `npm run format` | Форматування всіх файлів через Prettier |
| `npm run lint` | Перевірка SCSS (stylelint) + форматування (prettier --check) |

> ⚠️ Перед `npm run lint` запусти `npx stylelint "src/**/*.scss" --fix`

**Швидка перевірка після клонування:**
```bash
npm run format && npm run lint && npm run build && npm run preview
```

---

## Структура

```text
landing-keepsake-9lab/
├── .github/workflows/deploy.yml   # CI/CD → GitHub Pages
├── .husky/pre-commit              # Запуск лінтерів перед комітом
├── scripts/optimize-images.js     # Конвертація зображень (sharp)
├── src/
│   ├── assets/images/             # AVIF, WebP, JPEG у двох розмірах
│   ├── components/
│   │   ├── sections/              # hero, works, cta, services, stats, clients, journal
│   │   ├── header.pug
│   │   └── footer.pug
│   ├── data/                      # Дані відокремлені від розмітки
│   ├── includes/sprite.svg        # SVG-спрайт
│   ├── layouts/main.pug           # Базовий макет
│   ├── mixins/                    # +btn, +icon, +picture, +work-card
│   ├── pages/index.pug            # Головна сторінка
│   └── styles/
│       ├── abstracts/             # Токени, rem(), mq()
│       ├── base/                  # :root, reset
│       ├── layout/                # header, footer, containers
│       ├── components/            # Стилі блоків
│       └── main.scss              # Точка входу
├── .browserslistrc
├── .prettierrc
├── .stylelintrc.json
├── postcss.config.js
└── vite.config.js
```

---

## Технічні рішення

### Pug
Базовий макет через `extends` / `block`, секції підключені через `include`, контент винесений у `src/data/*.pug` і рендериться циклами `each`. Повторювані UI-елементи — міксини.

### SCSS (7-1)
`@use` / `@forward` замість `@import`. Кольори зберігаються в SASS-мапі `$colors` і автоматично генеруються в CSS-змінні `--color-*`. Адаптивність — mobile-first через `mq()`, БЕМ з вкладеністю до 3 рівнів.

### Зображення
Кожне зображення конвертується у AVIF + WebP + JPEG у розмірах `400w` і `800w`. У Pug підставляється через мікст `+picture()` із `<picture>`, `srcset` і `loading="lazy"`.

---

## Інструменти

| Інструмент | Роль |
|---|---|
| Vite | Збірка, dev-сервер, мініфікація |
| Vituum + vite-plugin-pug | Pug у Vite |
| Dart Sass | Компіляція SCSS |
| PostCSS + Autoprefixer | Вендорні префікси |
| sharp | Оптимізація зображень |
| Prettier + plugin-pug | Форматування |
| Stylelint | Аналіз SCSS, БЕМ |
| Husky + lint-staged | Pre-commit хуки |
| GitHub Actions | Автодеплой на Pages |
