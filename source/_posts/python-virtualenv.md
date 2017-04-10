---
title: Python 가상 환경 설치 (virtualenv)
date: 2017-04-10 23:08:23
tags: python, virtualenv
---

## virtualenv

Virtual Environment의 준말, 가상으로 Python 환경을 만드는 도구
한 시스템 내에서 각 각의 다른버젼으로 이루어진 환경을 분리하여 편하게 관리할 수 있다.

Python 패키지 뿐만 아니라 사용할 Python 버전도 가상 환경으로 분리 가능

Python 설치 후 자체 내장 된 기능으로 손쉽게 생성 가능하다.

* 설치 확인
    $ python3 -m venv
    (windows의 경우 그냥 python -m venv 로 입력)

* virtualenv 생성 명령어
    $ python3 -m venv 가상환경이름

* 활성화 및 비활성화 명령어
    Mac OS, Linux 계열
    $ source env_pystagram/bin/activate

    Windows
    $ env_pystagram\Scripts\activate.bat

    비활성화
    deactivate