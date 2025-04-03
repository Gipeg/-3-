import os

# 5.1 Вывод содержимого файла и выполнение .py
file_name = input("Введите имя файла: ")
if os.path.isfile(file_name):
    with open(file_name, 'r', encoding='utf-8') as file:
        content = file.read()
        print(content)
        
    if os.path.splitext(file_name)[1] == ".py":
        exec(content)
else:
    print("Файл не найден.")

# 5.2 Запись текста в файл
file_name = input("Введите имя файла для записи: ")
if os.path.exists(file_name):
    mode = input("Файл существует. Дописать (a) или перезаписать (w)? ")
    if mode not in ('a', 'w'):
        print("Неверный режим работы.")
        exit()
else:
    mode = 'w'

with open(file_name, mode, encoding='utf-8') as file:
    while True:
        line = input("Введите текст (или 'end' для завершения): ")
        if line == 'end':
            break
        file.write(line + '\n')

# 5.3 Операции с файлом
file_name = input("Введите имя файла: ")
if os.path.isfile(file_name):
    action = input("Выберите действие: (r) Чтение, (d) Удаление, (ren) Переименование: ")
    if action == 'r':
        with open(file_name, 'r', encoding='utf-8') as file:
            print(file.read())
    elif action == 'd':
        os.remove(file_name)
        print("Файл удалён.")
    elif action == 'ren':
        new_name = input("Введите новое имя файла: ")
        os.rename(file_name, new_name)
        print("Файл переименован.")
    else:
        print("Неверный выбор.")
else:
    print("Файл не найден.")

# 5.4 Удаление .txt файлов в каталоге и подкаталогах
directory = input("Введите путь к каталогу: ")
if os.path.isdir(directory):
    for root, _, files in os.walk(directory):
        for file in files:
            if file.endswith(".txt"):
                os.remove(os.path.join(root, file))
                print(f"Удалён файл: {file}")
else:
    print("Каталог не найден.")

# 5.5 Запись списка файлов и папок с их размерами в файл
output_file = "directory_contents.txt"
directory = input("Введите путь к каталогу: ")
if os.path.isdir(directory):
    with open(output_file, 'w', encoding='utf-8') as file:
        for root, dirs, files in os.walk(directory):
            for name in dirs + files:
                path = os.path.join(root, name)
                size_kb = os.path.getsize(path) // 1024
                file.write(f"{name} - {size_kb} KB\n")
    print(f"Информация записана в {output_file}")
else:
    print("Каталог не найден.")
