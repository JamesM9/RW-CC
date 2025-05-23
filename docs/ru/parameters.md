# Параметры PX4

Полная документация по параметрам PX4: https://docs.px4.io/master/en/advanced_config/parameter_reference.html.

Для изменения параметров PX4 используйте программу QGroundControl, [подключившись к Клеверу по Wi-Fi](gcs_bridge.md) или USB. Перейдите в панель *Vehicle Setup* (кликнув на логотип QGroundControl в левом верхнем углу и выберите меню *Parameters*.

## Рекомендованные значения

### Общие параметры

|Параметр|Значение|Примечание|
|-|-|-|
|`SENS_FLOW_ROT`|0 (*No rotation*)|В случае использования "железного" [PX4Flow](px4flow.md), оставьте значение по умолчанию|
|`SENS_FLOW_MINHGT`|0.0|Для [дальномера VL53L1X](laser.md)|
|`SENS_FLOW_MAXHGT`|4.0|Для [дальномера VL53L1X](laser.md)|
|`SENS_FLOW_MAXR`|10.0||
|`SYS_HAS_MAG`|0|При невозможности запуска магнитометра (ошибка *No mags found*)|

### Настройки подсистемы Estimator

В случае использования LPE ([прошивка COEX](firmware.md)):

|Параметр|Значение|Примечание|
|-|-|-|
|`LPE_FUSION`|86|Чекбоксы: *flow* + *vis* + *land detector* + *gyro comp*. При полете над ровным полом возможно включение *pub agl as lpos down*. <br>Подробнее: [Optical Flow](optical_flow.md), [ArUco-маркеры](aruco_map.md), [GPS](gps.md).|
|`LPE_VIS_DELAY`|0.0||
|`LPE_VIS_Z`|0.1||
|`LPE_FLW_SCALE`|1.0||
|`LPE_FLW_R`|0.2||
|`LPE_FLW_RR`|0.0||
|`LPE_FLW_QMIN`|10||
|`ATT_W_EXT_HDG`|0.5|Включение использования внешнего угла по рысканью (при навигации по [карте маркеров](aruco_map.md))|
|`ATT_EXT_HDG_M`|1 (*Vision*)||
|`ATT_W_MAG`|0|Выключение магнитометра (при навигации внутри помещения)|

В случае использования EKF2 (официальная прошивка):

<!-- markdownlint-disable MD044 -->

|Параметр|Значение|Примечание|
|-|-|-|
|`EKF2_AID_MASK`\*|26|Чекбоксы: *flow* + *vision position* + *vision yaw*.<br>Подробнее: [Optical Flow](optical_flow.md), [ArUco-маркеры](aruco_map.md), [GPS](gps.md).|
|`EKF2_OF_DELAY`|0||
|`EKF2_OF_QMIN`|10||
|`EKF2_OF_N_MIN`|0.05||
|`EKF2_OF_N_MAX`|0.2||
|`EKF2_HGT_MODE`\*|3 (*Vision*)|При наличии [дальномера](laser.md) и полете над ровным полом — 2 (*Range sensor*)|
|`EKF2_EVA_NOISE`|0.1 rad или 5 deg||
|`EKF2_EVP_NOISE`|0.1||
|`EKF2_EV_DELAY`|0||
|`EKF2_MAG_TYPE`|5 (*None*)|Выключение магнитометра (при навигации внутри помещения)|

\* — начиная с версии PX4 1.14 помеченные звездочкой параметры заменены на следующие:

|Параметр|Значение|Примечание|
|-|-|-|
|`EKF2_EV_CTRL`|11|Чекбоксы: *Horizontal position* + *Vertical position* + *Yaw*|
|`EKF2_GPS_CTRL`|0|Все чекбоксы сняты|
|`EKF2_BARO_CTRL`|0 (*Disabled*)|Барометр отключен|
|`EKF2_OF_CTRL`|1 (*Enabled*)|Optical flow включен|
|`EKF2_HGT_REF`|3 (*Vision*)|При наличии [дальномера](laser.md) и полете над ровным полом — 2 (*Range sensor*)|
|`EKF2_RNG_CTRL`|2 (*Enabled*)|Дальномер включен|

<!-- markdownlint-enable MD031 -->

> **Info** См. также: список параметров по умолчанию в [симуляторе](simulation.md): https://github.com/CopterExpress/clover/blob/master/clover_simulation/airframes/4500_clover.

## Дополнительная информация

Параметр `SYS_MC_EST_GROUP` отвечает за выбор Estimator'а.

Estimator это подсистема, которая вычисляет текущее состояние (state) коптера, используя показания с датчиков. В состояние коптера входит:

* угловая скорость коптера – roll_rate, pitch_rate, yaw_rate;
* ориентация коптера (в локальной системе координат) – roll (крен), pitch (тангаж), yaw (рысканье) (одно из представлений);
* позиция коптера (в локальной системе координат) – x, y, z;
* скорость коптера (в локальной системе координат) – vx, vy, vz;
* глобальные координаты коптера – latitude, longitude, altitude;
* высота над поверхностью;
* другие параметры (дрейф гироскопов, скорость ветра и пр.).

`SYS_AUTOCONFIG` – сброс всех параметров (при установке в значение 1).

## EKF2

`EKF2_AID_MASK` – выбор датчиков, которые используются EKF2 для вычисления состояния коптера.

`EKF2_HGT_MODE` – основной источник данных о высоте (z в локальной системе координат):

* 0 – давление с барометра.
* 1 – GPS.
* 2 – дальномер (например, vl53l1x).
* 3 – данные с VPE.

Вариант 2 является наиболее точным, но его корректно использовать, только если поверхность, над которой летает коптер – плоская. В противном случае начало координат по Z будет двигаться вверх и вниз с изменением высоты поверхности.

## Multicopter Position Control (полет по позиции)

Данные параметры настраивают полет коптера по позиции (режимы POSCTL, OFFBOARD, AUTO).

`MPC_THR_HOVER` – газ висения. Данный параметр необходимо установить на примерный процент газа, необходимый для того, чтобы коптер удерживал высоту. Если коптер имеет тенденцию набирать или терять высоту в режиме удержания высоты – можно уменьшить или увеличить это значение.

`MPC_XY_P` – коэффициент *P* регулятора по позиции. Этот параметр влияет на то, насколько резко коптер будет выполнять заданные команды по позиции. Слишком большое значение может вызвать перестрелы.

`MPC_XY_VEL_P` – коэффициент *P* регулятора по скорости. Данный параметр также влияет на точность и резкость выполнения коптером заданной позиции. При слишком большом значении возможны перестрелы.

`MPC_XY_VEL_MAX` – максимальная горизонтальная скорость в режимах POSCTL, OFFBOARD, AUTO.

`MPC_Z_P`, `MPC_Z_VEL_P` – коэффициенты *P* регуляторов по вертикальной позиции и скорости. Влияют на удерживание коптером необходимой высоты.

`MPC_LAND_SPEED` – вертикальная скорость посадки в режиме LAND.

## LPE + Q attitude estimator

Данные параметры настраивают поведение модулей `lpe` и `q`, которые вычисляют состояние (ориентацию, позицию) коптера. Эти параметры применяются **только** если параметр `SYS_MC_EST_GROUP` установлен в значение `1` (local_position_estimator, attitude_estimator_q).

## Commander

Преарм-чеки, переключение режимов и состояний коптера.

## Sensors

Включение, выключение и настройка различных датчиков.
