<warn>

Убедитесь, что вы [установили и сконфигурировали Terraform](../../../quick-start).

</warn>

Чтобы создать ключевую пару, создайте файл `keypair.tf`, где будет описана ее конфигурация. Добавьте текст из примера ниже и исправьте значения настроек для вашей инфраструктуры. В данном примере описывается создание ключевой пары с названием `test-keypair` и вывод на экран публичного и приватного ключа оператором `output`.

## Создание ключевой пары

<warn>

Приватный ключ, сгенерированный этим ресурсом, будет храниться в незашифрованном виде в вашем файле состояния Terraform. Использование этого ресурса для производственных развертываний не рекомендуется. Вместо этого создайте файл приватного ключа вне Terraform и безопасно распространите его в системе, где будет работать Terraform.

</warn>

Для создания ключевой пары вам потребуется ресурс (resource) `vkcs_compute_keypair`.

```hcl
resource "vkcs_compute_keypair" "keypair" {
  name = "test-keypair"
}

output "public_key" {
  value = vkcs_compute_keypair.keypair.public_key
}

output "private_key" {
  value = vkcs_compute_keypair.keypair.private_key
  sensitive = true
}
```

Здесь `name` — уникальное имя ключевой пары (обязательный аргумент). Изменение этого аргумента приведет к созданию новой ключевой пары.

## Применение изменений

Добавьте пример в файл `keypair.tf` и выполните следующие команды:

```bash
terraform init
```
```bash
terraform apply
```