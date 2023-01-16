Для подключения к виртуальной машине по SSH необходимо использовать ключевую пару: открытый ключ размещается на виртуальной машине, в то время как закрытый ключ хранится у пользователя.

Создать новую ключевую пару можно на этапе создания инстанса или в разделе «Ключевые пары».

Чтобы создать новую ключевую пару:

<tabs>
<tablist>
<tab>На платформе VK Cloud</tab>
<tab>Linux/Mac</tab>
<tab>Windows 10</tab>
</tablist>
<tabpanel>

1. Перейдите в раздел «Настройки аккаунта» → «Ключевые пары».
2. Нажмите «+ Создать ключ».
3. Введите название ключа.
4. Подтвердите создание.

Ключ автоматически будет сохранен на наш компьютер.

</tabpanel>
<tabpanel>

1. Откройте терминал.
2. Выполните команду `ssh-keygen`, чтобы создать новый ключ:

```bash
ssh-keygen -t rsa -b 2048 -m pem -f "путь до файла"
```

3. Укажите имя файла, в котором будут сохранены ключи и введите пароль.

Публичная часть ключа будет сохранена в файле `<имя_ключа>.pub`. Вставьте эту часть ключа в поле SSH-ключ при создании новой виртуальной машины.

</tabpanel>
<tabpanel>

1. Откройте терминал.
2. Создайте новый ключ, выполнив команду:

```bash
ssh-keygen -t rsa -b 2048 -m pem -f "путь до файла"
```

3. Когда вам будет предложено выбрать файл для сохранения ключа, нажмите Enter. Или укажите необходимый файл.
4. Введите пароль.

</tabpanel>
</tabs>