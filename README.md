<фрагмент_вставки_значка>
<фрагмент_вставки_значка>

# Лаба 2. Отчет
## 1. Настройка окружения и GitHub.

```bash
$ export GITHUB_USERNAME=<имя_пользователя>
$ export GITHUB_EMAIL=<адрес_почтового_ящика>
$ export GITHUB_TOKEN=<сгенирированный_токен>
$ alias edit=<nano|vi|vim|sub1>

$ cd $(GITHUB_USERNAME)/workspace
$ source scripts/activate

$ mkdir ~/.config
$ cat > ~/.config/hub <<EOF
github.com:
- user: $(GITHUB_USERNAME)
  oauth_token: $(GITHUB_TOKEN)
  protocol: https
EOF
$ git config --global hub.protocol https
```
## 2. Инициализация Git-репозитория.

```bash
$ mkdir projects/lab02 && cd projects/lab02
$ git init
$ git config --global user.name $(GITHUB_USERNAME)
$ git config --global user.email $(GITHUB_EMAIL)

$ git config -e --global
$ git remote add origin https://github.com/${GITHUB_USERNAME}/lab02.git
$ git pull origin master
$ touch README.md
$ git status
$ git add README.md
$ git commit --m"added README.md"
$ git push origin master
```
## 3. Добавление .gitignore в репозиторий.

```bash
*build*/
*install*/
*.swp
.idea/

$ git pull origin master
$ git log
```

## 4. Создание структуры проекта и файлов.

```bash
$ mkdir sources
$ mkdir include
$ mkdir examples
$ cat > sources/print.cpp <<EOF
#include <print.hpp>

void print(const std::string& text, std::ostream& out)
{
    out << text;
}

void print(const std::string& text, std::ofstream& out)
{
    out << text;
}
EOF

$ cat > include/print.hpp <<EOF
#include <fstream>
#include <iostream>
#include <string>

void print(const std::string& text, std::ofstream& out);
void print(const std::string& text, std::ostream& out = std::cout);
EOF
```
## 5. Создание примеров использования.

```bash
$ cat > examples/exampled.cpp <<EOF
#include <print.hpp>

int main(int argc, char** argv) { print("hello"); }
EOF

$ cat > examples/exampled.cpp <<EOF
#include <print.hpp>

#include <fstream>

int main(int argc, char** argv) { std::ofstream file("log.txt"); print(std::string("hello"), file); }
EOF
```
## 6. Работа с Git: коммит и отправка изменений.

```bash
$ git status
$ git add .
$ git commit -m"added sources"
$ git push origin master
```
## 7. Клонирование задач и создание отчетов.

```bash
$ cd ~/workspace/
$ export LAB_NUMBER=02
$ git clone https://github.com/tp-labs/lab$(LAB_NUMBER).git tasks/lab$(LAB_NUMBER)
$ mkdir reports/lab$(LAB_NUMBER)
$ cp tasks/lab$(LAB_NUMBER)/README.md reports/lab$(LAB_NUMBER)/REPORT.md
$ cd reports/lab$(LAB_NUMBER)
$ edit REPORT.md
$ gist REPORT.md
```

