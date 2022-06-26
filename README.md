# Домашнее задание Пользователи и группы. Авторизация и аутентификация 
<ol> 
  <li>Создать сденд для выполнения домашнего задания
  <li> Настроить стенд для выполнения домашнего задания 
    <li> PAM
      <li>
        <li>
          <li>
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

# 3. PAM
<ul>
  <li>pam_time</li>
  <p>В конец файла /etc/security/time.conf добавил следующие строки</p>
  <p>*;*;day;Al0800-2000
  <p>*;*;night;!Al0800-2000
  <p>*;*;friday;Fr
</ul>
