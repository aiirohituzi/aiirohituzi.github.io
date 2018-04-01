---
title: xlsxwriter 기본 사용법 메모
date: 2018-04-01 21:47:27
tags: xlsxwriter
---

xlsxwriter : python에서 excel을 다룰 수 있게 하는 모듈 중의 하나
[(docs 링크)](http://xlsxwriter.readthedocs.io/)


### 사용 예시
```py
import xlsxwriter

workbook = xlsxwriter.Workbook('skill.xlsx')
worksheet = workbook.add_worksheet()

# 직접 셀 위치를 입력
worksheet.write('A1', 'aaa')
worksheet.write('B1', 'bbb')
worksheet.write('C1', 'ccc')
worksheet.write('D1', 'ddd')


# 반복문을 통한 자동 입력
row = 1
col = 0

for a in (data):
    worksheet.write(row, col, a.get('...'))
    worksheet.write(row, col + 1, a.get('...'))
    worksheet.write(row, col + 2, a.get('...'))
    worksheet.write(row, col + 3, a.get('...'))
    ...

    row += 1

workbook.close()
```