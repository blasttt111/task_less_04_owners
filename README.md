1. Создаем пользователя `vally` с домашним каталогом и оболочкой `/bin/bash`, задаем пароль
  - (`sudo useradd -m -s /bin/bash vally`)
  - (`sudo passwd vally`)
2. Создаем пользователя `eve` без домашнего каталога
  - (`sudo useradd eve`)
3. Создаем директорию `/home/eve` и даем пользователю `eve` права на него
  - (`sudo chown eve /home/eve`)
  - проверим (`ls -l /home`)
<img width="802" height="594" alt="image" src="https://github.com/user-attachments/assets/da3cb6a9-d5cc-4c7d-8262-19621e63a94f" />
  - поправил первоначальную ошибку в том что не изменил группу владельцев /home/eve, исправил при помощи `chown` добавив туда как владельца так и группу 
  
  - (`sudo chown eve:eve /home/eve`)
  
  <img width="537" height="186" alt="image" src="https://github.com/user-attachments/assets/3c83bfa5-5f39-42a8-b29b-5018533be4f7" />


4. Переименовываем пользователя `vally` в `robot` и смотрим на UID
  - (`sudo usermod -l robot vally`)
  - (`id robot`)
5. Создаем группу `tms` и добавляем в него `robot`
  - (`sudo groupadd tms`)
  - (`sudo usermod -aG tms robot`)
  - проверим (`groups robot`)
<img width="664" height="292" alt="image" src="https://github.com/user-attachments/assets/fe01b651-d995-4f2c-a218-60923d2d7c31" />

6. Переходим к созданию `/var/www/projects` и нужных в ней файлов и директорий (скриншот для этого и след. пунктов ниже)
7. Установим права на файл `secret` так, чтобы только владелец мог читать и изменять его
  - (`sudo chmod 600 secret`)
8. Установим права на файл `readme.md` так, чтобы группа могла читать и изменять его
  - (`sudo chmod g+rw readme.md`)
9. Уставновить права на `bot-hub` так, чтобы ни у одной категории пользователей не было бита `x`
  - (`sudo chmod 644 bot-hub`)
  
<img width="799" height="693" alt="image" src="https://github.com/user-attachments/assets/96ba79a8-19df-448a-ab5b-2a32aa1a86e2" />

10. У нас не выйдет зайти в директорию `bot-hub`
<img width="657" height="143" alt="image" src="https://github.com/user-attachments/assets/91f9860b-7dc2-4889-8efe-7359cdaef8f1" />

11. Вернем файлу `bot-hub/app.py` бит `x` для владельца и группы
  - (`sudo chmod ug+x bot-hub/app.py`)
  <img width="666" height="288" alt="image" src="https://github.com/user-attachments/assets/8d2286c2-bab3-4d52-94b4-eb0fb0bf0403" />

12. Назначим директоию `/var/www/projects` рекурсивно группой владельцев `tms`
  - (`sudo chgrp -R tms /var/www/projects`)
13. Назначим владельцем файла `secret` пользователя `robot`, а владельцем `readme.md` - `eve`
  - (`sudo chown robot secret`)
  - (`sudo chown eve readme.md`)
  <img width="739" height="241" alt="image" src="https://github.com/user-attachments/assets/bbcd6589-085f-4da9-9699-f63c6cbf0b66" />
