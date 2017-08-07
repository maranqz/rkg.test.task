# Тестовое задание, часть 1#

Для инициализации стандартных пользователей команду yii init-users/up

admin:123456, email: admin@admin.com, role: admin
manager:123456, email: manager@manager.com, role: manager
user:123456, email: user@user.com, role: user

1. Регистрация и авторизация пользователей (можно использовать готовые модули/расширения) с подтверждением почтового ящика.

    Использовался готовый модуль yii2-user, для подтверждения была задан параметр enableConfirm


2. CRUD управление пользователями
- Добавление/редактирование пользователей сделать в модальном окне.

    Модальное окно сделано по средствам Model Widget с загрузкой содержания страницы редактирования. Само редактирование и изменение по средствам pjax, чтобы это корректно работало статично задаются id для pjax и при закрытее модального окна обновляется выше лежащий pjax блок.

- Возможность фильтрации списка: по ид, логину, email, дате регистрации, дате  последней авторизации.

    Стандартными средствами GridView filter с использованием yii2-date-range

права доступа: - Доступно только роли администратор
  
    Задана роль для параметр adminPermission как admin

3. CRUD управление новостями с разграничением прав.
- Добавление/редактирование новости сделать в модальном окне (картинка, краткий текст, полный текст).

    Выполнено аналогично пункту два.

- Возможность фильтрации списка: по дате добавления (от – до), названию, описанию,
статусу

    Стандартными средствами GridView filter с использованием yii2-date-range

- Возможность изменения статуса новости (активен, неактивен) прямо в списке без
перезагрузки страницы.

    по средствам pjax

права доступа (реализовать с использованием RBAC):
- Анонимный пользователь может просматривать только превью
- Авторизованный пользователь может просматривать полные новости
- Менеджер может добавлять новости и редактировать/удалять только свои новости
- Администратор - все выше описанное.

    Используется yii\rbac\PhpManager со стандартной ролью guest,  хранение данных выбрано в файле, т.к. предполагается небольшое количество пользователей (это ошибочно, для реального применение данного тестового задания)

    Задание всех параметров происходит в классе app\models\user\User\RbacController    


4. Постраничный вывод превью новостей на главной странице с дальнейшим полным просмотром. У пользователя должна быть возможность изменять количество превью на странице

    Используется activeDropDownList, который привязан к фильтру PostSearch модели

5. При добавлении новости на сайт, оповещать зарегистрированных пользователей по email и всплывающим уведомлением (например bootstrap-alert) с возможностью отметить уведомление как прочитанное.

    Используется longpolling по средствам yii2-longpolling. При добавлении нового уведомления происходит отправка

6. Сделать в настройках профиля настройку уведомлений (получать уведомления о новых новостях только на email, в браузер или и то и другое)

    Добавлены в профайл пользователя yii2-user

7. Оповещать пользователя по email при изменении пароля или создания нового пользователя администратором (выслать новому пользователю на email ссылку для активации профиля и ввода нового пароля для дальнейшей авторизации)

    Добавлен обработчик события на изменение пароля, с дальнейшей его посылкой.
