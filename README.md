# Домашнее задание Пользователи и группы. Авторизация и аутентификация 
<ol> 
  <li>Создать сденд для выполнения домашнего задания
  <li> Настроить стенд для выполнения домашнего задания 
    <li> Вариант Модуль pam_time
      <li> Вариант с выполнением скрипта при подключении пользователя
        <li> Вариант Модуль pam_script
</ol>  

# 1. Создать сденд для выполнения домашнего задания
<ul>
  <p> Развернута VM на базе CentOS 7
</ul>  

# 2. Настроить стенд для выполнения домашнего задания
<ul>
  <li>Заведение пользователей</li>
  <p>sudo useradd day</p>
  <p>sudo useradd night</p>
  <p>sudo useradd friday</p>
  <li>Создание паролей для заведённых пользователей</li>
  <p>sudo passwd day</p>
  <p>sudo passwd night</p>
  <p>sudo passwd friday</p>
</ul>  

# 3. Вариант Модуль pam_time
<ul>
  <li>Отредактировал time.conf</li>
  <p>В конец файла /etc/security/time.conf добавил следующие строки</p>
  <p>*;*;day;Al0800-2000</p>
  <p>*;*;night;!Al0800-2000</p>
  <p>*;*;friday;Fr</p>
  <li>Подключил модуль PAM</li>
  <p>Отредактировал файл /etc/pam.d/sshd</p>
  <p>account required pam_nologin.so</p>
  <p>account required pam_time.so</p>
</ul>

# 4. Вариант с выполнением скрипта при подключении пользователя
<ul>
  <li>Отредактировал файл /etc/pam.d/sshd</li>
  <p>account required pam_nologin.so</p>
  <p>account required pam_exec.so /usr/local/bin/test_login.sh</p>
  <li>Создал скрипт /usr/local/bin/test_login.sh</li>
  <p>скрипт взял от сюда https://gist.github.com/dmitry-lyutenko/39bf8afe5d1f6fc2d48b09c325706495</p>
</ul>

# 5. Вариант Модуль pam_script
<ul>
  <li>Подключил репозиторий EPEL</li>
  <p>yum -y install epel-release</p>
  <li>Установил pam_script</li>
  <p>yum install $pkg</p>
  <li>Отредактировал файл /etc/pam.d/sshd</li>
  <p>account required pam_nologin.so</p>
  <p>account required pam_script.so /usr/local/bin/test_login.sh</p>
  <li>Установить пакет nmap-ncat</li>
  <p>yum install nmap-ncat</p>
  <p>Открыл новую сессию под пользователем day и выполнил команду ncat -l -p 80</p>
  ![image](https://user-images.githubusercontent.com/98658046/175825086-d14f8f35-cc37-4e1a-baa5-8c8fe86c53b0.png)
  <li>Модуль pam_cap</li>
  <p>Отредактировал файл /etc/pam.d/sshd</p>
  <p>auth include postlogin</p>
  <p>auth required pam_cap.so</p>
  <li>Права пользователя day</li>
  <p>Создал файл /etc/security/capability.conf и добавил в него строку cap_net_bind_service day</p>
  <p>Выдал права программе ncat</p>
  <p>sudo setcap cap_net_bind_service=ei/usr/bin/ncat</p>
</ul>
