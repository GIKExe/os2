[Сайт симуляции](https://copy.sh/v86/), [Опкоды процессора](http://sparksandflames.com/files/x86InstructionChart.html), [Bios 0x10](https://biosprog.narod.ru/real/ints/int10.htm)
<br>
Программы: [HxD](https://mh-nexus.de/en/) (для изменения файлов по байтам), [UltraISO](https://www.ezbsystems.com/) (для создания загрузочного образа)
<br><br>
![image](https://github.com/GIKExe/os2/assets/72767917/81d5189e-79d5-4f66-91cb-d4949b337e3d)

```
### установка экрана (очистка тоже так работает)
B0 mov AL, 0x03
03 (80x25 символов, 16 цветов, 0xB8000 адрес страниц)
CD int 0x10
10 (функции экрана)

### отображение символа ? зелёным цветом
B4 mov AH, 0x09
09 (функция записи символа с цветом)
B0 mov AL, 0x3F
3F (символ ?)
B3 mov BL, 0x02
02 (зелёный символ на чёрном фоне)
B1 mov CL, 0x01
01 (количестов символов)
CD int 0x10
10 (функции экрана)

### получаем позицию курсора в x: DL, y: DH
B4 mov AH, 0x03
03
CD int 0x10
10

### x += 1, y = 0
42 inc DX
B6 mov DH, 0x00
00

### устанавливаем позицию курсора
B4 mov AH, 0x02
02
CD int 0x10
10

### зацикливание на отображение символа
EB jmp -23
E9
```
