# Отчёт по лабораторной работе №10

**Студент:** Maksim Alehanov
**Группа:** ИУ8-25
**Тема:** Создание и конфигурирование виртуальной среды разработки с Vagrant

---

## 1. Цель работы

Научиться описывать и поднимать виртуальную среду разработки с помощью Vagrant.

> Примечание: на Apple Silicon (arm64) VirtualBox не поддерживается, поэтому
> в качестве провайдера используется **docker**. Вариант из методички с
> VirtualBox приведён в файле `Vagrantfile.virtualbox`.

## 2. Выполнение

### 2.1. Vagrantfile (docker-провайдер)

```ruby
Vagrant.configure("2") do |config|
  config.vm.provider "docker" do |d|
    d.image           = "ubuntu:22.04"
    d.name            = "lab10-dev"
    d.cmd             = ["tail", "-f", "/dev/null"]
    d.remains_running = true
    d.has_ssh         = false
  end

  config.vm.synced_folder "shared", "/vagrant", disabled: true
end
```

### 2.2. Проверка и запуск

```sh
$ vagrant validate
Vagrantfile validated successfully.

$ vagrant up --provider=docker
==> default: Creating the container...
    default:   Name: lab10-dev
    default:  Image: ubuntu:22.04
==> default: Starting container...

$ vagrant status
default                   running (docker)

$ docker ps
lab10-dev | ubuntu:22.04 | Up ... seconds
```

Среда поднимается и работает. Остановка — `vagrant halt`, удаление —
`vagrant destroy`.

### 2.3. Вариант VirtualBox

В `Vagrantfile.virtualbox` сохранён вариант из методички с боксом
`bento/ubuntu-19.10` и provisioning-скриптом (установка docker.io, образ
fastide). На Apple Silicon не запускается, приведён для справки.

## 3. Результаты

- Описан Vagrantfile, конфигурация проходит `vagrant validate`.
- Среда поднимается командой `vagrant up` и переходит в состояние `running`.
- Приведён вариант конфигурации для VirtualBox.
