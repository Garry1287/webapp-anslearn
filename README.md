1. Проблема была в том, что не работает раздел

```
    - name: Ensure mysql is enabled to run on startup  
      service: name=mysql state=started enabled=true
```

Пришлось добавить в ручном режиме
```
    - name: Start Mysql Server
      shell: "service mysql start"
```
(https://itnan.ru/post.php?c=1&p=557838)[https://itnan.ru/post.php?c=1&p=557838]
(https://docs.ansible.com/ansible/latest/collections/community/mysql/mysql_user_module.html)[https://docs.ansible.com/ansible/latest/collections/community/mysql/mysql_user_module.html]

Борясь с этой проблемой пробывал руками всё ставить на образ, по-шагам
(https://github.com/mmumshad/simple-webapp)[https://github.com/mmumshad/simple-webapp]

Не заработало, flask не встал.


Получилось с этим образом 
[https://github.com/rastasheep/ubuntu-sshd/blob/mastermaster/18.04/Dockerfile] (https://github.com/rastasheep/ubuntu-sshd/blob/mastermaster/18.04/Dockerfile)

Но пришлось добавить в Dockerfile
```
ENV LC_ALL C
ENV LANG en_US.UTF-8
```

Собрал образ
```
garry@home-pc:~/devops_learn/ans_udemy/web_deployment$ docker build -t garry1287/ubuntu18-ssh .
```


Запустил два образа
`docker run -d garry1287/ubuntu18-ssh`


Запустил 
```
ansible-playbook playbook.yml -i inventory.txt
```
