# Flaskr CI/CD with DevSecOps Practices

## Описание
Учебный проект для дипломной работы: реализация CI/CD пайплайна с практиками DevSecOps.  
Приложение: **Flaskr (Flask-based blog app)**.  
Основная цель — показать интеграцию инструментов безопасности в процесс разработки.

---

## Технологии

| Компонент | Технология |
|-----------|------------|
| **Приложение** | Flask (Python 3.11) |
| **CI/CD** | GitHub Actions |
| **SAST** | Bandit |
| **DAST** | OWASP ZAP |
| **Security Checks** | Gitleaks (секреты), Trivy (зависимости) |
| **Security Gateway** | Автоматическая проверка перед релизом |

---

## Статус пайплайна

![CI/CD Pipeline](https://github.com/Ana7SteiSha/Diplomnaya-rabota-flaskr-ci-cd/actions/workflows/ci.yml/badge.svg)

---

## Архитектура пайплайна
[Код] 
   ├── SAST: Bandit ────────────────┐
   ├── Security Checks: Gitleaks + Trivy ──┤
   └── Приложение ── DAST: OWASP ZAP ────┘
                                          │
                                          ▼
                                  [Security Gateway]
                                          │
                                          ▼
                                   { Релиз? }
                                   /         \
                                  /           \
                                 ▼             ▼
                            [Деплой]    [Уведомление в PR]
---

## Локальный запуск

```bash
# Клонировать репозиторий
git clone https://github.com/Ana7SteiSha/Diplomnaya-rabota-flaskr-ci-cd.git
cd Diplomnaya-rabota-flaskr-ci-cd

# Создать и активировать виртуальное окружение
python -m venv venv
source venv/bin/activate   # Для Linux/Mac
# venv\Scripts\activate    # Для Windows

# Установить зависимости
pip install -r requirements.txt

# Запустить приложение
flask --app flaskr run --host=0.0.0.0 --port=5000
После запуска приложение доступно по адресу: http://localhost:5000/hello
Результаты проверок безопасности
Этап	Инструмент	Статус	Артефакт
SAST	Bandit	✅ Успешно	bandit-report.json
DAST	OWASP ZAP	✅ Успешно	dast-report.html
Security Checks	Gitleaks + Trivy	✅ Успешно	trivy-results.sarif
Security Gateway	Автоматический	✅ Готов	security-recommendations.md
Все отчеты доступны для скачивания в GitHub Actions → Artifacts.

Зоны роста
Интеграция с DefectDojo — централизованное хранение отчетов об уязвимостях

Полноценное DAST — активное сканирование с авторизацией и покрытием всех API

Kubernetes Security — добавление проверки манифестов (checkov)

Автоматическое обновление зависимостей — настройка Renovate

Внедрение IAST — интерактивный анализ безопасности в рантайме

Документация
Подробное описание пайплайна, аналитика выбора инструментов и описание процесса в DEVSECOPS.md

## Результаты работы пайплайна

![Результаты CI/CD](https://raw.githubusercontent.com/Ana7SteiSha/Diplomnaya-rabota-flaskr-ci-cd/main/images/actions_result.png)
