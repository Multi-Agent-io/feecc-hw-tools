# Feecc-hw-tools

Микросервис для взаимодействия с внешними устройствами (терминал автомобильных весов BT-009 и т.д.) по порту RS232

## Запуск

### Запуск микросервиса

В директории с файлом ```docker-compose.yaml``` (общий для микросервисов feecc-hw-tools и feecc-dispatcher) выполнить команду: 
```
docker-compose up --build
```

**Или**

Для запуска только feecc-hw-tools выполнить в директории с файлом ```docker-compose.yaml``` команду:
```
docker-compose up mongo
```

И в директории feecc_hw_tools команду:
```
uvicorn src.api.app:app --reload
```

### Запуск виртуальных устройств

#### Linux

Открыть пару виртуальных портов командой:
```
socat -d -d pty,raw,echo=0 pty,raw,echo=0
```
По паре для каждого устройства

#### Windows

Открыть виртуальные порты можно с помощью стороннего приложения, например: <https://freevirtualserialports.com/>


Затем добавить имена портов виртуальных устройств в ```config```
> Имена COM-портов различаются в разных системах. 
> 
> Для Linux это `/dev/pts/.` или `/dev/tty/.`
> 
> В Windows `COM.`

## Эндпойнты

+ **GET /devices/{device_id}** --- получить текущее состояние устройства
+ **POST /devices/{device_id}** --- изменить состояние устройства