# devops-netology
First Line

## Описание файла .gitignore в каталоге terraform

#### Комментарии на 1-й строке:
Исключает субдиректории .terraform

#### Комментарии на 4-й строке:
Исключает файлы .tfstate

#### Комментарии на 8-й строке:
Исключает лог-файл crash.log

#### Комментарии на 11-й строке:
Исключает все файлы .tfvars, которые могут содержать конфиденциальные данные, такие как
пароль, закрытые ключи и другие секреты. Они не должны быть частью системы
управления версиями, поскольку они являются точками данных, которые потенциально чувствительны и
могут быть изменены в зависимости от среды.

#### Комментарии на 18-й строке:
Исключает файлы:
override.tf
override.tf.json
Исключает файлы с именем, завершающиеся на _override и расширением .tf и .tf.json:
*_override.tf
*_override.tf.json

#### Комментарии на 25-й строке:
Включает файл example_override.tf

#### Комментарии на 29-й строке:
Включает файлы tfplan, чтобы игнорировать вывод плана командой: terraform plan -out=tfplan
Пример вывода: *tfplan*

#### Комментарии на 32-й строке:
Исключает файлы конфигурации командной строки:
.terraformrc
terraform.rc
