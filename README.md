# Домашнее задание к занятию "`Хранение в K8s`"



 ## Скриншоты задания №1
![описание пода с контейнерами (kubectl describe pods data-exchange)](https://github.com/YuriKopshev/kubernetes1/blob/origin/homework-4/img/%D0%A1%D0%BA%D1%80%D0%B8%D0%BD%D1%88%D0%BE%D1%82-24-06-2026%2014_26_56.png);
![вывод команды чтения файла (tail -f <имя общего файла>)](https://github.com/YuriKopshev/kubernetes1/blob/origin/homework-4/img/Screenshot%202026-06-24%20at%2018.31.07.png);


 ## Скриншоты задания №2
![шаг2](https://github.com/YuriKopshev/kubernetes1/blob/origin/homework-4/img/Screenshot%202026-06-24%20at%2018.59.16.png);
![шаг3](https://github.com/YuriKopshev/kubernetes1/blob/origin/homework-4/img/Screenshot%202026-06-24%20at%2019.01.37.png);
![шаг 4 и шаг 5](https://github.com/YuriKopshev/kubernetes1/blob/origin/homework-4/img/Screenshot%202026-06-24%20at%2019.08.49.png);

### Объяснение для Шага 4:

Что произошло с PV:

В выводе команды kubectl describe pv local-pv мы видим, что статус изменился на Status: Released. При этом в поле Claim всё еще сохраняется ссылка на старый, уже удаленный запрос — default/local-pvc.Почему это произошло:Политика Reclaim Policy: Retain. В манифесте нашего PV была явно указана политика сохранения данных Retain. Это заставляет Kubernetes бережно относиться к ресурсу.Защита данных от перезаписи. Когда мы удалили PVC (local-pvc), кластер перевел PV в статус Released («Освобожден»). В этом состоянии PV считается занятым историческими данными. Kubernetes намеренно блокирует этот PV и не позволяет связывать его с новыми PVC, чтобы предотвратить случайную перезапись или утечку чужих данных.

### Объяснение для Шага 5:

Что произошло с файлом после удаления PV:

Файл pv-file.txt полностью сохранился на локальном диске ноды и остался доступен для чтения даже после того, как сам объект PersistentVolume был окончательно удален из кластера Kubernetes.Почему это произошло:Тип хранилища hostPath связывает PV с конкретной папкой на физическом диске хоста (в нашем случае — внутри контейнера ноды kind). Архитектура Kubernetes устроена так, что удаление логических абстракций внутри кластера (объектов PV и PVC) никогда автоматически не удаляет файлы на реальных физических дисках для типа hostPath. Это сделано для безопасности, чтобы предотвратить потерю важных данных. Администратор сервера должен очищать такие локальные директории на нодах вручную.


 ## Скриншоты задания №3
![шаг №2](https://github.com/YuriKopshev/kubernetes1/blob/origin/homework-4/img/Screenshot3.png);
![шаг №3](https://github.com/YuriKopshev/kubernetes1/blob/origin/homework-4/img/Screenshot3.1.png);




 


