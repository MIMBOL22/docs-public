VK Cloud поддерживает подключение к Cloud Storage с использованием файловых менеджеров. Такие менеджеры позволяют работать с объектами хранилища, как с папками и файлами вашего устройства. Это удобно для работы с большим количеством файлов или с разными хранилищами одновременно.

## CyberDuck

CyberDuck позволяет подключаться к различным хранилищам одновременно. Каждое подключение открывается в отдельном окне. Вы можете копировать файлы как между устройством и хранилищем, так и между разными хранилищами или бакетами одного хранилища. Доступен для macOS и Windows.

1. [Создайте аккаунт и ключ доступа](../../instructions/account-management/) к Cloud Storage в личном кабинете VK Cloud. Сохраните **Secret Key**.
1. [Установите](https://cyberduck.io/download) CyberDuck.
1. Настройте подключение к объектному хранилищу:
    1. Нажмите кнопку **Новое подключение**.
    1. Укажите параметры подключения:

        - Тип подключения: `Amazon S3`.
        - **Сервер** — должен соответствовать [региону](../../../account/concepts/regions/) аккаунта:
            - `hb.ru-msk.vkcs.cloud` — для региона Москва;
            - `hb.kz-ast.vkcs.cloud` — для региона Казахстан.
        - **Порт**: `443`.
        - **Access Key ID**: идентификатор ключа доступа к Cloud Storage.
        - **Secret Access Key**: секретный ключ доступа к Cloud Storage. Секретный ключ должен соответствовать тому идентификатору ключа, который вы указали в **Access Key ID**.
    1. Нажмите кнопку **Подключиться**

В результате успешного подключения доступные для аккаунта бакеты отобразятся в CyberDuck.

<info>

Бакеты и объекты, которые создаются через Cyberduck, имеют [класс хранения](../../references#klass_hraneniya) `Hotbox` и [тип доступа](../../references#acl) `private`.

</info>

## WinSCP

WinSCP позволяет подключаться к различным хранилищам одновременно. Каждое подключение или локальная директория открывается на отдельной вкладке. Вы можете копировать файлы как между устройством и хранилищем, так и между разными хранилищами или бакетами одного хранилища. Доступен для Windows.

1. [Создайте аккаунт и ключ доступа](../../instructions/account-management/) к Cloud Storage в личном кабинете VK Cloud. Сохраните **Secret Key**.
1. [Установите](https://winscp.net/eng/download.php) WinSCP.
1. Настройте подключение к объектному хранилищу:
    1. Выберите в главном меню **Вкладки** → **Подключение** → **Управление подключениями**.
    1. Укажите настройки подключения:

        - **Протокол передачи**: `Amazon S3`;
        - **Имя хоста** — должно соответствовать [региону](../../../account/concepts/regions/) аккаунта:
            - `hb.ru-msk.vkcs.cloud` — для региона Москва;
            - `hb.kz-ast.vkcs.cloud` — для региона Казахстан.
        - **Порт**: `443`.
        - **Идентификатор ключа доступа**: идентификатор ключа, полученный при создании аккаунта Cloud Storage.
        - **Секретный ключ доступа**: секретный ключ доступа к Cloud Storage. Секретный ключ должен соответствовать тому идентификатору ключа, который вы указали в поле **Идентификатор ключа доступа**.
    1. Нажмите кнопку **Войти**.

В результате успешного подключения доступные для аккаунта бакеты отобразятся на вклакде WinSCP.

<info>

Бакеты, которые создаются через WinSCP, имеют [класс хранения](../../references#klass_hraneniya) `Hotbox`. Объекты, которые создаются через WinSCP, имеют класс хранения и [тип доступа](../../references#acl), наследуемые от бакета.

</info>

## Диск-О:

Диск-О: позволяет подключаться к различным хранилищам одновременно. Каждое подключение открывается как отдельный диск в локальной файловой системе. Диск-O: подключает не ко всему  Cloud Storage, а к бакету. Для работы с несколькими бакетами нужно создавать отдельные подключения. Вы можете копировать файлы как между устройством и хранилищем, так и между разными хранилищами или бакетами одного хранилища. Доступен для macOS и Windows.

1. [Создайте аккаунт и ключ доступа](../../instructions/account-management/) к Cloud Storage в личном кабинете VK Cloud. Сохраните **Secret Key**.
1. Выберите нужный бакет или [создайте новый](../../instructions/buckets/create-bucket).
1. [Установите](https://disk-o.cloud/ru/) Диск-О:.
1. Настройте подключение к бакету объектного хранилища:
    1. Нажмите кнопку **Подключить**.
    1. Выберите **MSC S3**.
    1. Укажите настройки подключения:

        - **Выберите хранилище**: `Горячие данные` — для бакета с [классом хранения](../../references#klass_hraneniya) Hotbox, `Холодные данные` — для бакета с [классом хранения](../../references#klass_hraneniya) Icebox;
        - **Введите бакет**: название имеющегося бакета.
        - **Access Key**: идентификатор ключа, полученный при создании аккаунта Cloud Storage.
        - **Secret Key**: секретный ключ доступа к Cloud Storage. Секретный ключ должен соответствовать тому идентификатору ключа, который вы указали в **Access Key**.
    1. Нажмите кнопку **Подключить**.

В результате успешного подключения объекты бакета будут доступны в локальной файловой системе и в окне быстрого доступа Диск-О:. Если в бакете нет объектов, подключенный диск будет пустым. Добавьте файл до 1 ГБ в директорию диска и через личный кабинет VK Cloud убедитесь, что в бакете появился объект.

<info>

Объекты, которые создаются через Диск-О:, имеют класс хранения и [тип доступа](../../references#acl), наследуемые от бакета.

</info>

## s3fs

Файловый менеджер s3fs позволяет монтировать бакет через FUSE и работать с объектами Cloud Storage в вашей локальной файловой системе или через CLI. Доступен для Linux, macOS, Windows и FreeBSD.

1. [Создайте аккаунт и ключ доступа](../../instructions/account-management/) к Cloud Storage в личном кабинете VK Cloud. Сохраните **Secret Key**.
1. Выберите нужный бакет или [создайте новый](../../instructions/buckets/create-bucket).
1. Установите s3fs.

    <tabs>
    <tablist>
    <tab>Debian 9 или новее</tab>
    <tab>Ubuntu 16.04 или новее</tab>
    <tab>CentOS 7 или новее</tab>
    <tab>SUSE 12 и openSUSE 42.1</tab>
    <tab>macOS</tab>
    </tablist>
    <tabpanel>

    Выполните команду:

    ```bash
    sudo apt install s3fs
    ```

    </tabpanel>
    <tabpanel>

    Выполните команду:

    ```bash
    sudo apt install s3fs
    ```

    </tabpanel>
    <tabpanel>

    В EPEL выполните команду:

    ```bash
    sudo yum install epel-release
    sudo yum install s3fs-fuse
    ```

    </tabpanel>
    <tabpanel>

    Выполните команду:

    ```bash
    sudo zypper install s3fs
    ```

    </tabpanel>
    <tabpanel>

    В Homebrew выполните команду:

    ```bash
    brew cask install osxfuse
    brew install s3fs
    ```

    </tabpanel>
    </tabs>

1. Настройте подключение к объектному хранилищу:

    1. Сохраните идентификатор ключа и секретный ключ в файл `~/.passwd-s3fs` в формате `<идентификатор ключа>:<секретный ключ>`:

        ```bash
        echo <идентификатор_ключа>:<секретный_ключ> >  ~/.passwd-s3fs
        ```
    1. Ограничьте доступ к файлу `~/.passwd-s3fs`:

        ```bash
        chmod 600  ~/.passwd-s3fs
        ```
    1.  Выберите каталог, в который будет монтироваться бакет, и убедитесь в наличии прав на чтение и запись к этому каталогу.
    1.  Выполните команду:

        ```bash
        s3fs <имя_бакета> <путь_к_папке> -o passwd_file=~/.passwd-s3fs -o url=<домен проекта> -o use_path_request_style
        ```
        Здесь:

        - `<имя_бакета>` — название бакета в Cloude Storage;
        - `<путь_к_папке>` — путь в локальной файловой системе до папки, в которой будет отображаться содержимое бакета;
        - `<домен проекта>` — должен соответствовать [региону](../../../account/concepts/regions/) аккаунта:
            - `https://hb.ru-msk.vkcs.cloud` — для региона Москва;
            - `https://hb.kz-ast.vkcs.cloud` — для региона Казахстан.

Если подключение успешно, в директории `<путь_к_папке>` должны отображаться все объекты подключенного бакета. Если в бакете нет объектов, директория будет пустой. Добавьте файл до 1 ГБ в директорию и через личный кабинет VK Cloud убедитесь, что в бакете появился объект.

<info>

Объекты, которые создаются через s3fs, имеют [класс хранения](../../references#klass_hraneniya) и [тип доступа](../../references#acl), наследуемые от бакета.

</info>