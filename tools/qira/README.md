# qira

## Сборка
### 1. Сборка докер образа
```bash
sudo docker build -t qira .
```
### 2. Запуск
```bash
sudo docker run -it -p 4000:4000 -p 3002:3002 -p 8080:8080 -v ${PWD}:/tmp qira:latest
```
## Использование
1. Скопировать исполняемый файл в папку с Dockerfile
2. Запустить исполняемый файл под qira (`qira *binary_file_name*`)
3. Перейти в браузере на [127.0.0.1:3002](http://127.0.0.1:3002/)