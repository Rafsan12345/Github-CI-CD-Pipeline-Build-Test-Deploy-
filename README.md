# Github-CI-CD-Pipeline-Build-Test-Deploy-

#🟢 Step 1: লোকাল প্রজেক্ট সেটআপ
mkdir python-ci-demo
cd python-ci-demo
git init

#🟢 Step 2: Python কোড লিখুন

calculator.py

def add(a, b):
    return a + b

def sub(a, b):
    return a - b

def mul(a, b):
    return a * b

def div(a, b):
    if b == 0:
        raise ValueError("Cannot divide by zero")
    return a / b

#🟢 Step 3: Unit Test লিখুন

test_calculator.py

import pytest
import calculator

def test_add():
    assert calculator.add(2, 3) == 5

def test_sub():
    assert calculator.sub(5, 3) == 2

def test_mul():
    assert calculator.mul(4, 5) == 20

def test_div():
    assert calculator.div(10, 2) == 5

def test_div_zero():
    try:
        calculator.div(10, 0)
    except ValueError as e:
        assert str(e) == "Cannot divide by zero"

#🟢 Step 4: Requirements ফাইল বানান

requirements.txt

pytest

#🟢 Step 5: লোকালি টেস্ট চালান
pip install -r requirements.txt
pytest -v


সব test pass হলে ✅ GitHub এ push করার জন্য রেডি।

#🟢 Step 6: GitHub Repo তে push
git add .
git commit -m "Initial Python project with unit tests"
git branch -M main
git remote add origin https://github.com/YourUsername/python-ci-demo.git
git push -u origin main

#🟢 Step 7: GitHub Actions Workflow তৈরি

.github/workflows/python-ci.yml

name: Python CI

on:
  push:
    branches: [ main ]
  pull_request:
    branches: [ main ]

jobs:
  build-and-test:
    runs-on: ubuntu-latest

    steps:
      - name: Checkout repo
        uses: actions/checkout@v3

      - name: Set up Python
        uses: actions/setup-python@v4
        with:
          python-version: '3.10'

      - name: Install dependencies
        run: |
          python -m pip install --upgrade pip
          pip install -r requirements.txt

      - name: Run Unit Tests
        run: pytest -v

#🟢 Step 8: Workflow push করুন
git add .github/workflows/python-ci.yml
git commit -m "Add Python CI workflow"
git push

#🟢 Step 9: GitHub এ ফলাফল দেখুন

Repo → Actions ট্যাব এ workflow দেখাবে

প্রতিটি push/PR এ টেস্ট রান হবে

যদি কোন টেস্ট fail করে → লাল cross ❌

সব pass হলে → সবুজ চেক ✅
