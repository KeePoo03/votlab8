# Лабораторная работа №8: Отчёт по продажам в Docker

## Сборка образа

```bash
docker build -t report:latest .
```

## Запуск отчёта по CSV

PowerShell (Windows):

```powershell
docker run --rm -v "${PWD}/data:/data" report:latest
```

Linux / macOS:

```bash
docker run --rm -v "$(pwd)/data:/data" report:latest
```

Свой файл и группировка по товарам:

```bash
docker run --rm -v "$(pwd)/data:/data" -e DATA_FILE=/data/my_sales.csv report:latest product
```

## Запуск отчёта из PostgreSQL

```bash
docker network create labnet
docker run -d --name db --network labnet -e POSTGRES_PASSWORD=student123 postgres:17
docker run --rm --network labnet --entrypoint python report:latest db_report.py
```