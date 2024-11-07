# Лабораторная работа №3

## Задание

Необходимо настроить виртуальную машину А с Ubuntu (желательно, но можно и другую Linux подобную ОС) в VirtualBox.
Обеспечить доступ в сеть Интернет. Осуществить проверку этого доступа и приложить скриншот из терминала.
Следующим шагом настроить ещё одну виртуальную машину Б.
После чего обеспечить сетевой доступ от машины А к машину Б. Приложить скриншот из терминала.
Поднять ещё одну виртуальную машину В. Организовать сетевой доступ:

1. из машины А в машину Б,
2. из машины А в машину В,
3. но запретить доступ из машины Б в машину В,
4. приложить скриншот, на котором видно терминалы всех трёх машин и видно что между машинами есть (или нет) доступа.

## Ход работы

Для создания виртуальных машин я буду использовать Parallels для Mac. В ней с помощью [iso-образца Ubuntu Server](https://ubuntu.com/download/server/arm) я создаю три виртуальные машины. Каждой машине я определил свой IP-адрес в сети: `192.168.0.101` (А), `192.168.0.102` (Б), `192.168.0.103` (В).

![Screenshot 2024-11-07 at 04 49@2x](https://github.com/user-attachments/assets/0f35672e-0ba9-40bb-87c6-7a8dc9fa35c6)

На каждой машине так же настроен доступ в Интернет. Проверить мы можем это с помощью команды `ping -c 4 google.com`.

![Screenshot 2024-11-07 at 04 56@2x](https://github.com/user-attachments/assets/dc0645af-a9a4-4a4b-8bb5-2ae4ad477d53)

Так же из машины А мы можем получить доступ к машинам Б и В:

![Screenshot 2024-11-07 at 04 57@2x](https://github.com/user-attachments/assets/617fd088-a4a9-49b5-a3d9-60c5cd9bc544)

Далее по заданию требуется запретить доступ машине Б к машине В. Для этого на машине В я воспользовался командой iptables, которая блокирует доступ машине Б по IP-адресу: `iptables -A INPUT -i eth0 -p icmp --icmp-type echo-request -s 192.168.0.102 -j DROP`. Проверить наличия доступа у машины Б к машине В, мы можем с помощью команды `ping -c 4 192.168.0.103` на машине Б.

![Screenshot 2024-11-07 at 04 59@2x](https://github.com/user-attachments/assets/2102eeb5-1555-4468-a0c7-c230a9bf0e41)

## Доступы

Скриншот с информацией о доступах к разным точкам для каждой машины:

![Screenshot 2024-11-07 at 05 39@2x](https://github.com/user-attachments/assets/4733b45f-d20a-4f15-b6fa-643a1178cb6f)

## Вывод

Таким образом, у меня получилось поставить 3 виртуальных машины на Ubuntu, установить между ними связь, а так же настроить определенные доступы между ними.
