.PHONY: dev test lint build migrate

dev:
	python3 -m uvicorn app.main:app --reload

test:
	python3 -m pytest tests/ --cov=app --cov-fail-under=80

lint:
	python3 -m ruff check . --fix
	python3 -m mypy .

build:
	echo "No build step — add one here if needed"

migrate:
	python3 pipeline/migrate.py  # replace with your migration script or alembic
