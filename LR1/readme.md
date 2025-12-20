# Отчет по лабораторной работе №1 "Реализация удаленного импорта"

1. Запустил файл myremotemodule.py, находясь в каталоге этого файла командой 
    ```python3 -m http.server```

![alt text](https://github.com/21question/Programming-5-semester/blob/main/LR1/pictures/Photo_3.png)

2. После запуска сервера открываем второй терминал, переходим в нашу папку и запускаем команду 
```python3 -i activation_script.py```

![alt text](https://github.com/21question/Programming-5-semester/blob/main/LR1/pictures/Photo_1.png)

После запуска команды прописываем уже в редакторе Python команду ```sys.path.append("http://localhost:8000")```
И команду ```import название_файла```, в моем случае было myremotemodule.
После этого если нет ошибок, вводим команду myremotemodule.myfoo() (название_файла.название_функции) и получаем вывод:

![alt text](https://github.com/21question/Programming-5-semester/blob/main/LR1/pictures/Photo_2.png)

Переписал содержимое функции url_hook, класса URLLoader с помощью модуля requests

![alt text](https://github.com/21question/Programming-5-semester/blob/main/LR1/pictures/Photo_4.png)

