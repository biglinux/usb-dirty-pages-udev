# EN - Use udev to specify dirty pages for usb devices i.e. cache in ram before writing files to usb devices

Dirty pages is the name used to define how much cache in RAM memory must be used before recording data on storage devices.

A problem known for many years in Desktop Linux is the default configuration that stipulates the configuration of dirty pages for the entire system and it is very difficult to find information on how to configure dirty pages in isolation for each storage device.

Low values slow down the system, but high values are bad for using removable devices connected to USB, because when copying large files, the user is informed that the copy was completed when he finished moving the file to the cache in RAM and not the actual writing of the file to the storage device.

To perform the change manually, just use 2 commands, see the example considering that the USB device is /dev/sdb, first we will stipulate the use of 16 MB of max_bytes, which is equivalent to dirty pages, in the second command we activate this limit:

echo 16777216 > /sys/block/sdb/bdi/max_bytes
echo 1 > /sys/block/sdb/bdi/strict_limit

This repository includes a configuration file for udev that automates the task and always uses 16 MB of dirty pages for storage devices plugged into USB ports.


# PT - Use o udev para especificar dirty pages para dispositivos usb, ou seja, cache em RAM antes de gravar arquivos em dispositivos USB

Dirty pages é o nome utilizado para definir quanto de cache em memória RAM deve ser utilizada antes de efetuar a gravação dos dados em dispositivos de armazenamento.

Um problema conhecido a muitos anos no Desktop Linux é a configuração padrão que estipula a configuração de dirty pages para todo o sistema e é muito difícil encontrar a informação de como configurar o dirty pages de forma isolada para cada dispositivo de armazenamento.

Valores baixos trazem lentidão para o sistema, mas valores altos são ruins para o uso de dispositivos removíveis plugados na USB, pois ao efetuar cópias de arquivos grandes o usuário é informado que a cópia foi concluída ao terminar de mover o arquivo para cache em RAM e não a gravação real do arquivo no dispositivo de armazenamento.

Para efetuar a troca manualmente basta utilizar 2 comandos, veja o exemplo considerando que o dispositivo USB é o /dev/sdb, primeiro iremos estipular o uso de 16 MB de max_bytes, que equivale ao dirty pages, no segundo comando ativamos esse limite:

echo 16777216 > /sys/block/sdb/bdi/max_bytes
echo 1 > /sys/block/sdb/bdi/strict_limit

Esse repositório inclui um arquivo de configuração para o udev que automatiza a tarefa e utiliza sempre 16 MB de dirty pages para dispositivos de armazenamento plugados em portas USB.
