VK Cloud предоставляет механизм для работы с объемными файлами, размер которых может оказаться слишком велик для единоразовой загрузки файла в бакет через графический интерфейс или CLI.

Многокомпонентная (составная) загрузка позволяет загружать один объект как набор частей. Каждая часть представляет собой непрерывную часть данных объекта. Можно загружать эти части объекта независимо и в любом порядке. Если передача какой-либо части не удалась, можно повторно передать эту часть, не затрагивая другие части. После того, как все части объекта загружены, VK Cloud собирает эти части и создает объект. Как правило, когда размер объекта достигает 100 МБ, рекомендуется рассмотреть возможность использования многокомпонентной загрузки вместо загрузки объекта за одну операцию.

Использование составной загрузки дает следующие преимущества:

- Повышенная производительность — можно загружать части параллельно, чтобы повысить производительность.
- Быстрое восстановление при любых сетевых проблемах — меньший размер части сводит к минимуму влияние перезапуска неудачной загрузки из-за сетевой ошибки.
- Приостановить и возобновить загрузку объекта — можно загружать части объекта с течением времени. После того, как инициируется многокомпонентная загрузка, нет срока действия; завершить или отменить составную загрузку необходимо в явном виде.
- Начать загрузку до того, как известен окончательный размер объекта — можно загружать объект по мере его создания.