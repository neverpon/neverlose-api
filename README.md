# ПОЛНАЯ ДОКУМЕНТАЦИЯ NEVERLOSE LUA API

## Содержание
1. [Глобальные функции (_G)](#глобальные-функции-_g)
2. [Битовые операции (bit)](#битовые-операции-bit)
3. [Система цветов (color)](#система-цветов-color)
4. [Общие функции (common)](#общие-функции-common)
5. [Консольные переменные (cvar)](#консольные-переменные-cvar)
6. [База данных (db)](#база-данных-db)
7. [Система сущностей (entity)](#система-сущностей-entity)
8. [ESP система (esp)](#esp-система-esp)
9. [Система событий (events)](#система-событий-events)
10. [Файловая система (files)](#файловая-система-files)
11. [Глобальные переменные (globals)](#глобальные-переменные-globals)
12. [JSON (json)](#json-json)
13. [Система материалов (materials)](#система-материалов-materials)
14. [Математические функции (math)](#математические-функции-math)
15. [Интерфейс пользователя (ui)](#интерфейс-пользователя-ui)
16. [Сетевые функции (network)](#сетевые-функции-network)
17. [Panorama интерфейс (panorama)](#panorama-интерфейс-panorama)
18. [Rage система (rage)](#rage-система-rage)
19. [Рендеринг (render)](#рендеринг-render)
20. [Утилиты (utils)](#утилиты-utils)
21. [Векторные операции (vector)](#векторные-операции-vector)

## Глобальные функции (_G)

### Основные функции
- `assert(expression, text, ...)` - Проверяет условие, выдает ошибку если false
- `error(text, level)` - Генерирует ошибку и прерывает выполнение
- `getmetatable(object)` - Возвращает метатаблицу объекта
- `ipairs(tbl)` - Итератор для таблиц (индексы 1, 2, 3...)
- `print(text, ...)` - Выводит текст в консоль
- `print_error(text, ...)` - Выводит ошибку в консоль со звуком
- `print_chat(text, ...)` - Выводит текст в игровой чат
- `print_raw(text, ...)` - Выводит цветной текст в консоль (используя "\aRRGGBB")
- `print_dev(text, ...)` - Выводит текст в верхнюю-левую панель консоли
- `tonumber(value, base)` - Преобразует в число
- `tostring(var)` - Преобразует в строку
- `type(var)` - Возвращает тип переменной
- `unpack(tbl, start_index, end_index)` - Распаковывает таблицу в аргументы
- `xpcall(func, err_callback, ...)` - Безопасный вызов функции с обработкой ошибок

### Преобразование временных единиц
- `to_ticks(time)` - Преобразует секунды в тики
- `to_time(ticks)` - Преобразует тики в секунды

### Система классов
- `new_class()` - Создает новую систему классов для организации кода
  ```lua
  local ctx = new_class()
      :struct 'struct_one' {
          variable1 = 'test',
          
          some_function = function(self, arg1)
              print(arg1)
              print(string.format('Hello World (%s)', self.variable1))
          end
      }
      
  ctx.struct_one:some_function('test')
  ```

## Битовые операции (bit)

### Функции битовых операций
- `bit.arshift(x, n)` - Арифметический сдвиг вправо
- `bit.band(x1, x2, ...)` - Битовое И
- `bit.bnot(x)` - Битовое НЕ
- `bit.bor(x1, x2, ...)` - Битовое ИЛИ
- `bit.bswap(x)` - Обмен байтов (конвертация endianness)
- `bit.bxor(x1, x2, ...)` - Битовое исключающее ИЛИ
- `bit.lshift(x, n)` - Логический сдвиг влево
- `bit.rol(x, n)` - Циклический сдвиг влево
- `bit.ror(x, n)` - Циклический сдвиг вправо
- `bit.rshift(x, n)` - Логический сдвиг вправо
- `bit.tobit(x)` - Нормализует число для битовых операций
- `bit.tohex(x, n)` - Преобразует в шестнадцатеричную строку

## Система цветов (color)

### Создание цветов
```lua
-- RGBA формат
local red = color(255, 0, 0, 255)
local green = color(0, 255, 0)
local transparent_blue = color(0, 0, 255, 128)

-- HEX формат
local yellow = color("#FFFF00FF")
```

### Методы цветов
- `col:clone()` - Создает копию цвета
- `col:init(r, g, b, a)` - Устанавливает RGBA значения
- `col:init(value)` - Устанавливает цвет из HEX строки
- `col:as_fraction(r, g, b, a)` - Устанавливает значения как доли (0.0-1.0)
- `col:as_int32(value)` - Устанавливает цвет из 32-битного целого числа
- `col:as_hsv(h, s, v, a)` - Устанавливает из HSV значений
- `col:as_hsl(h, s, l, a)` - Устанавливает из HSL значений
- `col:to_fraction()` - Получает значения как доли
- `col:to_hex()` - Получает как HEX строку
- `col:to_int32()` - Получает как 32-битное целое число
- `col:to_hsv()` - Получает HSV значения
- `col:to_hsl()` - Получает HSL значения
- `col:lerp(other, weight)` - Линейная интерполяция между цветами
- `col:grayscale(weight)` - Преобразует в оттенки серого
- `col:alpha_modulate(alpha)` - Изменяет альфа-канал
- `col:unpack()` - Получает r, g, b, a значения

### Прямой доступ к компонентам
```lua
local col = color(255, 0, 0, 255)
col.r = 128  -- Изменить компонент красного
col.g = 128  -- Изменить компонент зеленого
col.b = 0    -- Изменить компонент синего
col.a = 200  -- Изменить альфа-канал
```

## Общие функции (common)

### Функции даты и времени
- `common.get_date(format, unix_time)` - Форматирует дату
- `common.get_unixtime()` - Возвращает UNIX время в секундах
- `common.get_timestamp()` - Возвращает высокоточную метку времени в миллисекундах
- `common.get_system_time()` - Возвращает системное время Windows

### Функции игры
- `common.get_product_version()` - Получает версию игрового клиента
- `common.get_game_directory()` - Получает путь к папке игрового клиента
- `common.get_map_data()` - Получает данные текущей карты
- `common.get_username()` - Возвращает имя пользователя Neverlose
- `common.get_config_name()` - Возвращает имя текущего конфига
- `common.get_active_scripts()` - Возвращает таблицу активных скриптов
- `common.get_mouse_wheel_delta()` - Возвращает изменение колеса мыши
- `common.is_in_thirdperson()` - Проверяет, находится ли камера в режиме от третьего лица
- `common.reload_script()` - Перезагружает текущий скрипт
- `common.unload_script()` - Выгружает текущий скрипт
- `common.force_full_update()` - Принудительно отправляет полный пакет обновления

### Изменение игровых значений
- `common.set_clan_tag(text)` - Устанавливает клан-тег
- `common.set_name(text)` - Устанавливает имя в игре

### UI и Уведомления
- `common.add_event(text, icon_name)` - Добавляет событие в верхнюю-левую панель
- `common.add_notify(title, text)` - Отображает уведомление

### Клавиши и ввод
- `common.is_button_down(key)` - Проверяет, нажата ли кнопка
- `common.is_button_released(key)` - Проверяет, отпущена ли кнопка

## Консольные переменные (cvar)

### Основные методы
- `cvar_object:call(...)` - Вызывает консольную команду с аргументами
- `cvar_object:int(value, raw)` - Получает/устанавливает целочисленное значение
- `cvar_object:float(value, raw)` - Получает/устанавливает значение с плавающей точкой
- `cvar_object:string(value)` - Получает/устанавливает строковое значение

### Колбэки
- `cvar_object:set_callback(callback)` - Регистрирует колбэк на изменение значения
- `cvar_object:unset_callback(callback)` - Отменяет колбэк

### Примеры использования
```lua
-- Изменение значения
cvar.mp_teammates_are_enemies:int(1)

-- Выполнение команды
cvar.clear:call()

-- Получение значения
local interp = cvar.cl_interp:float()

-- Установка колбэка на изменение
cvar.sv_cheats:set_callback(function(cvar_obj, old_value, new_value)
    print("sv_cheats изменен с " .. old_value .. " на " .. new_value)
end)
```

## База данных (db)

### Хранение и доступ к данным
- `db.key_name` - Доступ к сохраненному значению
- `db.key_name = value` - Сохранение значения (сохраняется между перезагрузками скрипта)

### Пример использования
```lua
-- Получение сохраненных данных или создание нового объекта
local data = db.test or {}

-- Изменение данных
data.name = 'User'
data.score = 100

-- Сохранение данных перед выгрузкой скрипта
events.shutdown:set(function()
    db.test = data
end)
```

## Система сущностей (entity)

### Получение сущностей
- `entity.get(idx, by_userid)` - Получает сущность по индексу
- `entity.get_local_player()` - Получает сущность локального игрока
- `entity.get_players(enemies_only, include_dormant, callback)` - Получает игроков
- `entity.get_entities(class, include_dormant, callback)` - Получает сущности по классу
- `entity.get_threat(hittable)` - Получает текущую угрозу
- `entity.get_game_rules()` - Получает сущность правил игры
- `entity.get_player_resource()` - Получает сущность ресурсов игрока

### Доступ к сетевым свойствам
```lua
-- Получение свойства
local health = player.m_iHealth
local pitch = player.m_flPoseParameter[12]
local stamina = player['m_flStamina']

-- Установка свойства
player.m_bSpotted = true
player.m_flPoseParameter[12] = 0.5
player['m_nSkin'] = 2
```

### Общие методы сущностей
- `ent:is_player()` - Проверяет, является ли сущность игроком
- `ent:is_weapon()` - Проверяет, является ли сущность оружием
- `ent:is_dormant()` - Проверяет, является ли сущность спящей
- `ent:is_bot()` - Проверяет, является ли сущность ботом
- `ent:is_alive()` - Проверяет, жива ли сущность
- `ent:is_enemy()` - Проверяет, является ли сущность врагом
- `ent:is_visible()` - Проверяет, видима ли сущность
- `ent:is_occluded(to_entity)` - Проверяет, полностью ли скрыта сущность
- `ent:get_index()` - Получает индекс сущности
- `ent:get_name()` - Получает имя сущности
- `ent:get_origin()` - Получает позицию сущности
- `ent:get_angles()` - Получает углы сущности
- `ent:get_simulation_time()` - Получает время симуляции
- `ent:get_classname()` - Получает имя класса сущности
- `ent:get_classid()` - Получает ID класса сущности
- `ent:get_materials()` - Получает материалы сущности
- `ent:get_model_name()` - Получает имя модели сущности

### Методы игрока
- `player:get_network_state()` - Получает сетевое состояние игрока
- `player:get_bbox()` - Получает ограничивающий прямоугольник
- `player:get_player_info()` - Получает информацию об игроке
- `player:get_player_weapon(all_weapons)` - Получает оружие игрока
- `player:get_anim_state()` - Получает состояние анимации
- `player:get_anim_overlay(idx)` - Получает оверлей анимации
- `player:get_eye_position()` - Получает позицию глаз
- `player:get_bone_position(idx)` - Получает позицию кости
- `player:get_hitbox_position(idx)` - Получает позицию хитбокса
- `player:get_steam_avatar()` - Получает аватар Steam
- `player:get_xuid()` - Получает Steam ID
- `player:get_resource()` - Получает ресурсы игрока
- `player:get_spectators()` - Получает наблюдающих игроков
- `player:set_icon(icon)` - Устанавливает иконку в таблице счета
- `player:simulate_movement(origin, velocity, flags)` - Имитирует движение

### Методы оружия
- `weapon:get_weapon_index()` - Получает индекс оружия
- `weapon:get_weapon_icon()` - Получает иконку оружия
- `weapon:get_weapon_info()` - Получает информацию об оружии
- `weapon:get_weapon_owner()` - Получает владельца оружия
- `weapon:get_weapon_reload()` - Получает процент перезарядки
- `weapon:get_max_speed()` - Получает максимальную скорость с этим оружием
- `weapon:get_spread()` - Получает разброс оружия
- `weapon:get_inaccuracy()` - Получает неточность оружия

### Ключи информации об оружии (weapon_info)
Доступны через: `weapon:get_weapon_info()`
```lua
-- Основные свойства
weapon_info.max_player_speed             -- Максимальная скорость
weapon_info.attack_move_speed_factor     -- Множитель скорости при атаке
weapon_info.spread                       -- Базовый разброс
weapon_info.spread_alt                   -- Альтернативный разброс

-- Неточность при различных действиях
weapon_info.inaccuracy_crouch            -- Неточность в присяде
weapon_info.inaccuracy_stand             -- Неточность стоя
weapon_info.inaccuracy_jump              -- Неточность в прыжке
weapon_info.inaccuracy_land              -- Неточность при приземлении
weapon_info.inaccuracy_ladder            -- Неточность на лестнице
weapon_info.inaccuracy_fire              -- Неточность при стрельбе
weapon_info.inaccuracy_move              -- Неточность при движении

-- Отдача
weapon_info.recoil_seed                  -- Сид отдачи
weapon_info.recoil_angle                 -- Угол отдачи
weapon_info.recoil_magnitude             -- Величина отдачи

-- Другие свойства
weapon_info.weapon_name                  -- Название оружия
weapon_info.weapon_price                 -- Цена оружия
weapon_info.cycle_time                   -- Время между выстрелами
weapon_info.damage                       -- Урон
weapon_info.armor_ratio                  -- Соотношение брони
weapon_info.penetration                  -- Пробивная способность
weapon_info.range                        -- Дальность
```

### Контекст симуляции движения (sim_ctx)
Доступен через: `player:simulate_movement()`

- `sim:think(ticks)` - Симулирует движение на указанное количество тиков
- `sim.origin` - Позиция игрока после симуляции
- `sim.velocity` - Скорость игрока после симуляции
- `sim.view_offset` - Смещение обзора по оси Z
- `sim.duck_amount` - Значение приседания после симуляции
- `sim.did_hit_collision` - Флаг столкновения во время симуляции
- `sim.obb_mins` - Минимальные точки ограничивающего объема
- `sim.obb_maxs` - Максимальные точки ограничивающего объема
- `sim.simulation_ticks` - Количество тиков симуляции
- `sim.gravity_per_apply` - Применённая гравитационная сила
- `sim.max_speed` - Максимальная скорость при симуляции
- `sim.stamina` - Значение выносливости после симуляции
- `sim.surface_friction` - Трение поверхности после симуляции

## ESP система (esp)

### Доступные классы ESP
- `esp.enemy` - ESP для врагов
- `esp.team` - ESP для союзников
- `esp.self` - ESP для себя

### Создание элементов ESP
- `esp.esp_class:new_text(name, preview, callback)` - Создает текстовый элемент ESP
  ```lua
  local health_text = esp.enemy:new_text("Health", "LOW HP", function(player)
      local health = player.m_iHealth
      if health < 20 then
          return "LOW HP"  -- Показывать только при здоровье < 20
      end
      return nil  -- Не показывать
  end)
  ```

- `esp.esp_class:new_bar(name, callback)` - Создает полосу ESP
  ```lua
  local speed_bar = esp.enemy:new_bar("Speed", function(player)
      local velocity = player.m_vecVelocity
      local speed = velocity:length()
      if speed < 2 then
          return nil  -- Не показывать при стоянии на месте
      end
      -- Возвращает процент от максимальной скорости
      return speed / 260 * 100
  end)
  ```

- `esp.esp_class:new_item(name)` - Создает произвольный элемент ESP
  ```lua
  local item_example = esp.enemy:new_item("Custom Item")
  local item_group = item_example:create()
  local switch_ref = item_group:switch("Enable Feature")
  
  events.render:set(function()
      print("Item Example Selected: " .. tostring(item_example:get()))
      print("Switch Enabled: " .. tostring(switch_ref:get()))
  end)
  ```

### Методы группы ESP
- `esp_group:get()` - Получает значение элемента
- `esp_group:set()` - Устанавливает значение элемента
- `esp_group:name(value)` - Получает/устанавливает имя элемента
- `esp_group:create()` - Прикрепляет группу к элементу

## Система событий (events)

### Игровые события (GameEvents)
```lua
local hitgroup_str = {
    [0] = 'generic',
    'head', 'chest', 'stomach',
    'left arm', 'right arm',
    'left leg', 'right leg',
    'neck', 'generic', 'gear'
}

events.player_hurt:set(function(e)
    local me = entity.get_local_player()
    local attacker = entity.get(e.attacker, true)
    
    if me == attacker then
        local user = entity.get(e.userid, true)
        local hitgroup = hitgroup_str[e.hitgroup]
        
        print(('Hit %s in the %s for %d damage (%d health remaining)'):format(
            user:get_name(), hitgroup,
            e.dmg_health, e.health
        ))
    end
end)
```

### События чита
- `events.render` - Вызывается каждый кадр
  ```lua
  events.render:set(function(ctx)
      render.rect(vector(0, 0), vector(100, 100), color(230, 150))
  end)
  ```

- `events.render_glow` - Вызывается при подготовке glow object manager
  ```lua
  events.render_glow:set(function(ctx)
      ctx:render(origin, target, 0.15, 'lg', color(255, 0, 0))
  end)
  ```

- `events.override_view` - Вызывается при подготовке камеры
- `events.createmove` - Вызывается при подготовке команды движения
  ```lua
  events.createmove:set(function(cmd)
      if cmd.in_speed then
          cmd.view_angles.z = 50  -- Roll angle при удержании Shift
      end
  end)
  ```

- `events.createmove_run` - Вызывается при выполнении команды движения
- `events.aim_fire` - Вызывается при выстреле аимбота
- `events.aim_ack` - Вызывается при подтверждении выстрела аимбота
- `events.bullet_fire` - Вызывается при выстреле пули
- `events.console_input` - Вызывается при выполнении консольной команды
  ```lua
  events.console_input:set(function(text)
      if text == '/roll' then
          local random_int = utils.random_int(1, 6)
          print(common.get_username() .. ' rolled a ' .. random_int)
          return false  -- Предотвращает обработку команды игрой
      end
  end)
  ```

- `events.draw_model` - Вызывается перед отрисовкой модели
  ```lua
  events.draw_model:set(function(ctx)
      local me = entity.get_local_player()
      
      if ctx.entity == me then
          -- Переопределение модели локального игрока
          ctx:draw(custom_material)
          
          -- Предотвращает отрисовку оригинальной модели
          return false
      end
  end)
  ```

- `events.level_init` - Вызывается после полного подключения к серверу
- `events.pre_render` - Вызывается перед отрисовкой кадра
- `events.post_render` - Вызывается после отрисовки кадра
- `events.net_update_start` - Вызывается перед обработкой обновлений сущностей
- `events.net_update_end` - Вызывается после получения пакета обновления сущностей
- `events.config_state` - Вызывается при обновлении состояния конфигурации
- `events.mouse_input` - Вызывается при вводе мыши
- `events.shutdown` - Вызывается при выгрузке скрипта
- `events.pre_update_clientside_animation` - Вызывается до UpdateClientSideAnimation
- `events.post_update_clientside_animation` - Вызывается после UpdateClientSideAnimation
- `events.grenade_override_view` - Вызывается для переопределения отображения гранаты
- `events.grenade_warning` - Вызывается при отображении предупреждения о гранате
- `events.grenade_prediction` - Вызывается при предсказании траектории гранаты
- `events.localplayer_transparency` - Вызывается для переопределения прозрачности игрока

### Сложные события
- `events.voice_message` - Вызывается при получении голосового пакета
  ```lua
  events.voice_message(function(ctx)
      local buffer = ctx.buffer
      local code = buffer:read_bits(16)
      
      if code ~= 0x1337 then
          return
      end
      
      local tickcount = buffer:read_bits(32)
      
      print(string.format(
          'received voice packet from %s | pct_tickcount: %d',
          ctx.entity:get_name(), tickcount
      ))
  end)
  
  -- Отправка голосового пакета
  events.voice_message:call(function(buffer)
      buffer:write_bits(0x1337, 16)
      buffer:write_bits(globals.tickcount, 32)
  end)
  ```

### Управление событиями
- `events.event_name:set(callback)` - Устанавливает колбэк для события
- `events.event_name:unset(callback)` - Отменяет колбэк для события
- `events.event_name:call(...)` - Вызывает указанное событие

### Альтернативный синтаксис
```lua
-- Установка колбэка
events.event_name(callback, true)

-- Отмена колбэка
events.event_name(callback, false)

-- Переключение состояния колбэка
events.event_name(callback)
```

## Файловая система (files)

### Функции файловой системы
- `files.create_folder(path)` - Создает новую папку
- `files.read(path)` - Читает содержимое файла
- `files.write(path, contents, is_binary)` - Записывает данные в файл
- `files.get_crc32(path)` - Получает CRC32 контрольную сумму файла

### Примеры использования
```lua
-- Создание папки
files.create_folder("neverlose/configs")

-- Чтение файла
local content = files.read("neverlose/configs/config.json")

-- Запись в файл
files.write("neverlose/configs/config.json", json.stringify(config_data))

-- Получение контрольной суммы
local checksum = files.get_crc32("neverlose/configs/config.json")
```

## Глобальные переменные (globals)

### Доступные переменные
- `globals.curtime` - Серверное время в секундах
- `globals.realtime` - Локальное время в секундах
- `globals.frametime` - Длительность последнего кадра в секундах
- `globals.framecount` - Количество кадров с начала игры
- `globals.absoluteframetime` - Длительность последнего кадра в секундах
- `globals.tickcount` - Количество тиков, прошедших на сервере
- `globals.tickinterval` - Длительность тика в секундах
- `globals.max_players` - Максимальное количество игроков на сервере
- `globals.is_connected` - True если игрок подключен
- `globals.is_in_game` - True если игрок в игре
- `globals.choked_commands` - Количество задержанных команд
- `globals.commandack` - Текущий номер команды, подтвержденной сервером
- `globals.commandack_prev` - Номер последней отправленной команды
- `globals.last_outgoing_command` - Номер последней подтвержденной сервером команды
- `globals.server_tick` - Последний полученный тик сервера
- `globals.client_tick` - Собственный тик клиента
- `globals.delta_tick` - Последний действительный тик снапшота сервера
- `globals.clock_offset` - Разница между счетчиками тиков сервера и клиента

## JSON (json)

### Функции для работы с JSON
- `json.parse(json_text)` - Преобразует JSON строку в Lua значение
- `json.stringify(value)` - Преобразует Lua значение в JSON строку

### Примеры использования
```lua
-- Преобразование Lua таблицы в JSON
local config = {
    name = "My Config",
    settings = {
        aimbot = true,
        fov = 120,
        smooth = 0.5
    }
}
local json_text = json.stringify(config)

-- Преобразование JSON строки в Lua таблицу
local parsed = json.parse(json_text)
print(parsed.name)  -- "My Config"
print(parsed.settings.fov)  -- 120
```

## Система материалов (materials)

### Функции материалов
- `materials.get(path, force_load)` - Получает материал
- `materials.get_materials(partial_path, force_load, callback)` - Получает материалы
- `materials.create(name, key_values)` - Создает новый материал

### Методы материалов
- `material:get_name()` - Получает имя материала
- `material:get_texture_group_name()` - Получает имя группы текстур
- `material:var_flag(flag, value)` - Получает/устанавливает флаги материала
- `material:shader_param(name, value)` - Получает/устанавливает параметры шейдера
- `material:color_modulate(color)` - Получает/устанавливает модуляцию цвета
- `material:alpha_modulate(alpha)` - Получает/устанавливает модуляцию альфа-канала
- `material:is_valid()` - Проверяет валидность материала
- `material:reset()` - Сбрасывает свойства материала
- `material:override(mat)` - Переопределяет свойства материала

### Пример работы с материалами
```lua
-- Получение материала
local mat = materials.get("models/player/ct_fbi/ct_fbi_glass", true)

-- Изменение свойств
mat:var_flag(var_flags["SELFILLUM"], true)
mat:color_modulate(color(255, 0, 0, 200))

-- Создание материала
local custom_mat = materials.create("custom_material", [[
    "UnlitGeneric" {
        "$basetexture" "models/debug/debugwhite"
        "$color" "[1 0 0]"
        "$alpha" "0.8"
    }
]])
```

### Флаги материалов (var_flags)
```lua
local var_flags = {
    ["DEBUG"] = 0,
    ["NO_DEBUG_OVERRIDE"] = 1,
    ["NO_DRAW"] = 2,
    ["USE_IN_FILLRATE_MODE"] = 3,
    ["VERTEXCOLOR"] = 4,
    ["VERTEXALPHA"] = 5,
    ["SELFILLUM"] = 6,
    ["ADDITIVE"] = 7,
    ["ALPHATEST"] = 8,
    ["MULTIPASS"] = 9,
    ["ZNEARER"] = 10,
    ["MODEL"] = 11,
    ["FLAT"] = 12,
    ["NOCULL"] = 13,
    ["NOFOG"] = 14,
    ["IGNOREZ"] = 15,
    ["DECAL"] = 16,
    ["ENVMAPSPHERE"] = 17,
    ["NOALPHAMOD"] = 18,
    ["ENVMAPCAMERASPACE"] = 19,
    ["BASEALPHAENVMAPMASK"] = 20,
    ["TRANSLUCENT"] = 21,
    ["NORMALMAPALPHAENVMAPMASK"] = 22,
    ["NEEDS_SOFTWARE_SKINNING"] = 23,
    ["OPAQUETEXTURE"] = 24,
    ["ENVMAPMODE"] = 25,
    ["SUPPRESS_DECALS"] = 26,
    ["HALFLAMBERT"] = 27,
    ["WIREFRAME"] = 28,
    ["ALLOWALPHATOCOVERAGE"] = 29,
    ["IGNORE_ALPHA_MODULATION"] = 30,
    ["VERTEXFOG"] = 31
}
```

## Математические функции (math)

### Дополнительные математические функции
- `math.abs(x)` - Абсолютное значение числа
- `math.acos(x)` - Арккосинус (в радианах)
- `math.asin(x)` - Арксинус (в радианах)
- `math.atan(x)` - Арктангенс (в радианах)
- `math.atan2(x, y)` - Арктангенс y/x (в радианах)
- `math.ceil(x)` - Округление вверх
- `math.clamp(value, min, max)` - Ограничение числа в диапазоне
- `math.cos(x)` - Косинус (в радианах)
- `math.cosh(x)` - Гиперболический косинус
- `math.deg(x)` - Преобразование радианов в градусы
- `math.exp(x)` - e в степени x
- `math.floor(x)` - Округление вниз
- `math.fmod(x, y)` - Остаток от деления x на y
- `math.frexp(x)` - Мантисса и экспонента числа
- `math.huge` - Значение больше любого числа
- `math.ldexp(x, e)` - x * 2^e
- `math.log(x)` - Натуральный логарифм
- `math.log10(x)` - Логарифм по основанию 10
- `math.map(value, in_from, in_to, out_from, out_to, should_clamp)` - Линейное отображение
- `math.max(x, ...)` - Максимальное значение
- `math.min(x, ...)` - Минимальное значение
- `math.modf(x)` - Целая и дробная части
- `math.normalize_yaw(x)` - Нормализация угла поворота
- `math.pi` - Значение числа pi
- `math.pow(x, y)` - x в степени y
- `math.rad(x)` - Преобразование градусов в радианы
- `math.random(m, n)` - Случайное число
- `math.randomseed(x)` - Устанавливает зерно генератора случайных чисел
- `math.sin(x)` - Синус (в радианах)
- `math.sinh(x)` - Гиперболический синус
- `math.sqrt(x)` - Квадратный корень
- `math.tan(x)` - Тангенс (в радианах)
- `math.tanh(x)` - Гиперболический тангенс

## Интерфейс пользователя (ui)

### Общие функции UI
- `ui.get_alpha()` - Получает прозрачность меню
- `ui.get_size()` - Получает размер меню
- `ui.get_position()` - Получает позицию меню
- `ui.get_mouse_position()` - Получает позицию мыши
- `ui.get_binds()` - Получает привязки горячих клавиш
- `ui.get_style(name)` - Получает цвета стиля
- `ui.get_icon(name)` - Получает иконку fontawesome
- `ui.create(group)` - Создает группу UI
- `ui.create(tab, group, column)` - Создает группу UI в указанной вкладке
- `ui.find(...)` - Находит элементы UI
- `ui.sidebar(name, icon_name)` - Получает/устанавливает вкладку боковой панели
- `ui.localize(lang, str, localized)` - Локализует текст

### Методы создания групп UI
- `group:switch(name, init)` - Создает переключатель
- `group:slider(name, min, max, init, scale, tooltip)` - Создает ползунок
- `group:combo(name, items, ...)` - Создает выпадающий список
- `group:selectable(name, items, ...)` - Создает выбираемый список
- `group:color_picker(name, color)` - Создает выбор цвета
- `group:button(name, callback, alt_style)` - Создает кнопку
- `group:hotkey(name, default_key)` - Создает горячую клавишу
- `group:input(name, text)` - Создает поле ввода
- `group:list(name, items, ...)` - Создает список
- `group:listable(name, items, ...)` - Создает выбираемый список
- `group:label(text)` - Создает метку
- `group:texture(texture, size, color, mode, rounding)` - Создает текстуру

### Методы элементов UI
- `item:get()` - Получает значение элемента
- `item:id()` - Получает уникальный ID элемента
- `item:list()` - Получает список элементов (для combo/selectable)
- `item:type()` - Получает тип элемента
- `item:override(value, ...)` - Переопределяет значение элемента
- `item:get_override()` - Получает переопределенное значение
- `item:update(...)` - Обновляет значения элемента
- `item:reset()` - Сбрасывает элемент к исходному значению
- `item:set(value, ...)` - Устанавливает значение элемента
- `item:name(value)` - Получает/устанавливает имя элемента
- `item:tooltip(value)` - Получает/устанавливает подсказку элемента
- `item:visibility(state)` - Получает/устанавливает видимость элемента
- `item:disabled(state)` - Получает/устанавливает отключение элемента
- `item:set_callback(callback, force_call)` - Устанавливает колбэк изменения
- `item:unset_callback(callback)` - Отменяет колбэк
- `item:color_picker(color)` - Прикрепляет выбор цвета
- `item:create()` - Прикрепляет группу к элементу
- `item:parent()` - Получает родительский объект элемента

### Примеры создания UI
```lua
-- Создание группы
local group = ui.create("Example Group")

-- Создание элементов
local switch = group:switch("Enable Feature", false)
local slider = group:slider("Speed", 0, 100, 50, 0.1, function(val) return val .. "%" end)
local combo = group:combo("Mode", "Mode A", "Mode B", "Mode C")
local color = group:color_picker("Color", color(255, 0, 0, 255))
local button = group:button("Apply", function() print("Applied!") end)
local hotkey = group:hotkey("Toggle Key")

-- Многоцветный color picker
local multi_color = group:color_picker("Gradient", {
    ["Simple"] = {
        color(255, 255, 255)
    },
    ["Double"] = {
        color(255, 255, 255),
        color(0, 0, 0)
    },
    ["Multiple"] = {
        color(255, 0, 0),
        color(0, 255, 0),
        color(0, 0, 255),
        color(255, 0, 255)
    }
})

-- Получение выбранного режима и цветов
local mode, colors = multi_color:get()
local top_left, top_right, bottom_left, bottom_right = unpack(multi_color:get("Multiple"))

-- Колбэк на изменение
switch:set_callback(function(ref)
    print("Switch is now: " .. tostring(ref:get()))
    
    -- Изменение видимости других элементов
    slider:visibility(ref:get())
end)
```

## Сетевые функции (network)

### HTTP запросы
- `network.get(url, headers, callback)` - HTTP GET запрос
- `network.post(url, data, headers, callback)` - HTTP POST запрос

### Примеры использования
```lua
-- GET запрос
network.get("https://api.example.com/data", nil, function(response)
    local data = json.parse(response)
    print("Received data: " .. data.message)
end)

-- POST запрос с данными
network.post("https://api.example.com/submit", 
    {
        username = "player",
        score = 100
    }, 
    {
        ["Content-Type"] = "application/json"
    }, 
    function(response)
        local result = json.parse(response)
        print("Submission result: " .. result.status)
    }
)
```

## Panorama интерфейс (panorama)

### Функции Panorama
- `panorama.loadstring(js_code, panel)` - Загружает и выполняет JavaScript код
- `panorama[api]` - Доступ к API Panorama
- `panorama[panel][api]` - Доступ к API конкретной панели

### Примеры использования
```lua
-- Доступ к API из панели по умолчанию
local MyPersonaAPI = panorama.MyPersonaAPI
print(MyPersonaAPI.GetXuid())

-- Доступ к API из конкретной панели
local UiToolkitAPI = panorama.CSGOMainMenu.UiToolkitAPI
UiToolkitAPI.CloseAllVisiblePopups()

-- Выполнение JavaScript кода
panorama.loadstring([[
    GameStateAPI.GetPlayerXuidStringFromEntIndex(0)
]])
```

## Rage система (rage)

### Anti-Aim функции
- `rage.antiaim:get_max_desync()` - Получает максимальное значение desync
- `rage.antiaim:get_rotation(value)` - Получает текущий поворот anti-aim
- `rage.antiaim:get_target(return_fr)` - Получает целевой поворот
- `rage.antiaim:inverter(value)` - Получает/устанавливает состояние инвертера
- `rage.antiaim:override_hidden_pitch(value)` - Переопределяет скрытый наклон
- `rage.antiaim:override_hidden_yaw_offset(value)` - Переопределяет скрытое смещение поворота

### Exploit функции
- `rage.exploit:get()` - Получает заряд эксплойта (0.0-1.0)
- `rage.exploit:allow_charge(value)` - Разрешает/блокирует заряд эксплойта
- `rage.exploit:allow_defensive(value)` - Разрешает/блокирует defensive эксплойт
- `rage.exploit:force_teleport()` - Принудительно активирует телепорт
- `rage.exploit:force_charge()` - Принудительно заряжает эксплойт

### Пример использования
```lua
-- Получение текущего состояния
local desync = rage.antiaim:get_max_desync()
local rotation = rage.antiaim:get_rotation()
local exploit_charge = rage.exploit:get()

-- Изменение настроек
if exploit_charge >= 1.0 then
    rage.antiaim:inverter(true)
    rage.exploit:force_teleport()
end
```

## Рендеринг (render)

### Общие функции рендеринга
- `render.screen_size()` - Получает размер экрана
- `render.camera_position()` - Получает позицию камеры
- `render.camera_angles(angles)` - Получает/устанавливает углы камеры
- `render.world_to_screen(position)` - Преобразует мировые координаты в экранные
- `render.get_offscreen(position, radius, accurate)` - Получает положение на краю экрана
- `render.get_pixel(position)` - Получает цвет пикселя экрана
- `render.load_font(name, size, flags)` - Загружает шрифт
- `render.load_image(contents, size)` - Загружает изображение
- `render.load_image_rgba(contents, size)` - Загружает RGBA изображение
- `render.load_image_from_file(path, size)` - Загружает изображение из файла
- `render.measure_text(font, flags, text)` - Измеряет размер текста
- `render.highlight_hitbox(entity, hitbox, color)` - Подсвечивает хитбокс
- `render.get_scale(type)` - Получает масштаб DPI

### Функции отрисовки
- `render.blur(position_a, position_b, strength, alpha, rounding)` - Размытие
- `render.line(position_a, position_b, color)` - Линия
- `render.poly(color, positions, ...)` - Полигон
- `render.poly_blur(opacity, strength, positions, ...)` - Размытый полигон
- `render.poly_line(color, positions, ...)` - Контур полигона
- `render.rect(position_a, position_b, color, rounding, no_clamp)` - Прямоугольник
- `render.rect_outline(position_a, position_b, color, thickness, rounding, no_clamp)` - Контур прямоугольника
- `render.gradient(position_a, position_b, top_left, top_right, bottom_left, bottom_right, rounding)` - Градиент
- `render.circle(position, color, radius, start_deg, pct)` - Круг
- `render.circle_outline(position, color, radius, start_deg, pct, thickness)` - Контур круга
- `render.circle_gradient(position, color_outer, color_inner, radius, start_deg, pct)` - Градиентный круг
- `render.circle_3d(position, color, radius, start_deg, pct, outline)` - 3D круг
- `render.circle_3d_outline(position, color, radius, start_deg, pct, thickness)` - Контур 3D круга
- `render.circle_3d_gradient(position, color_outer, color_inner, radius, start_deg, pct)` - Градиентный 3D круг
- `render.text(font, position, color, flags, text, ...)` - Текст
- `render.texture(texture, position, size, color, mode, rounding)` - Текстура
- `render.push_rotation(degrees)` - Применяет поворот для последующих элементов
- `render.pop_rotation()` - Отменяет установленный поворот
- `render.push_clip_rect(pos_a, pos_b, intersect)` - Применяет область отсечения
- `render.pop_clip_rect()` - Отменяет область отсечения
- `render.shadow(pos_a, pos_b, clr, thickness, offset, rounding)` - Тень

### Объекты шрифта и изображений
- `ImgObject`
  - `img.width` - Ширина изображения
  - `img.height` - Высота изображения
  - `img.resolution` - Разрешение изображения

- `FontObject`
  - `font.width` - Ширина шрифта
  - `font.height` - Высота шрифта
  - `font.spacing` - Интервал шрифта
  - `font:set_size(size)` - Устанавливает новый размер шрифта

### Примеры рендеринга
```lua
-- Загрузка шрифта
local font = render.load_font("Arial", 16, "ab")  -- Anti-aliased, bold

-- Отрисовка текста
render.text(font, vector(100, 100), color(255, 255, 255), "c", "Centered Text")

-- Создание и отрисовка изображения
local image = render.load_image_from_file("neverlose/images/icon.png", vector(64, 64))
render.texture(image, vector(200, 200), vector(64, 64), color(255, 255, 255))

-- Отрисовка интерфейса
events.render:set(function()
    local screen = render.screen_size()
    local center = screen * 0.5
    
    -- Фон
    render.rect(center - vector(100, 50), center + vector(100, 50), color(30, 30, 30, 200), 5)
    
    -- Обводка
    render.rect_outline(center - vector(100, 50), center + vector(100, 50), color(255, 0, 0), 1, 5)
    
    -- Текст
    render.text(1, center, color(255, 255, 255), "c", "Hello World!")
    
    -- Индикатор
    render.circle(center + vector(0, 30), color(0, 255, 0), 10, 0, 1)
end)
```

## Утилиты (utils)

### Консольные и отложенные функции
- `utils.console_exec(cmd, ...)` - Выполняет консольную команду
- `utils.execute_after(delay, callback, ...)` - Отложенное выполнение

### Сетевые функции
- `utils.net_channel()` - Возвращает структуру NetChannel

### Трассировка
- `utils.trace_line(from, to, skip, mask, type)` - Трассировка линии через мир
- `utils.trace_hull(from, to, mins, maxs, skip, mask, type)` - Трассировка объема через мир
- `utils.trace_bullet(from_entity, from, to, skip)` - Трассировка пули

### Поиск по памяти
- `utils.opcode_scan(module, signature, offset)` - Сканирование сигнатуры в памяти модуля
- `utils.create_interface(module, interface)` - Создает интерфейс
- `utils.get_netvar_offset(table, prop)` - Получает смещение сетевого свойства
- `utils.get_vfunc(index, ...)` - Возвращает функцию виртуальной таблицы
- `utils.get_vfunc(module, interface, index, ...)` - Возвращает функцию из интерфейса

### Случайные числа
- `utils.random_int(min, max)` - Случайное целое число
- `utils.random_float(min, max)` - Случайное число с плавающей точкой
- `utils.random_seed(seed)` - Устанавливает зерно для генератора случайных чисел

### Структура NetChannel
- `net.time` - Текущее сетевое время
- `net.time_connected` - Время подключения в секундах
- `net.time_since_last_received` - Время с момента последнего полученного пакета
- `net.is_loopback` - True если сервер локальный
- `net.is_playback` - True если воспроизводится демо
- `net.is_timing_out` - True если клиент испытывает тайм-аут
- `net.sequence_nr[flow]` - Номер последней отправленной последовательности
- `net.latency[flow]` - Текущая задержка (RTT)
- `net.avg_latency[flow]` - Средняя задержка в секундах
- `net.loss[flow]` - Процент потери пакетов (0.0-1.0)
- `net.choke[flow]` - Процент задержки пакетов (0.0-1.0)
- `net.packets[flow]` - Среднее количество пакетов/сек
- `net.data[flow]` - Поток данных в байтах/сек
- `net:get_server_info()` - Получает информацию о сервере
- `net:is_valid_packet(flow, frame)` - Проверяет валидность пакета
- `net:get_packet_time(flow, frame)` - Получает время отправки пакета
- `net:get_packet_bytes(flow, frame, group)` - Получает размер группы пакета
- `net:get_packet_response_latency(flow, frame)` - Получает задержку ответа пакета

## Векторные операции (vector)

### Создание и инициализация
```lua
local vec = vector(100, 200, 300)  -- Создание вектора
vec:init(10, 20, 30)              -- Инициализация существующего вектора
```

### Методы векторов
- `vec:angles(pitch, yaw)` - Преобразует угол в направляющий вектор
- `vec:angles(angle)` - Преобразует угол в направляющий вектор
- `vec:angles()` - Возвращает угловой вектор, представляющий нормаль вектора
- `vec:ceil()` - Округляет координаты вверх
- `vec:clone()` - Создает копию вектора
- `vec:closest_ray_point(ray_start, ray_end)` - Ближайшая точка на луче
- `vec:cross(other)` - Векторное произведение
- `vec:dist(other)` - Евклидово расстояние
- `vec:dist2d(other)` - 2D расстояние
- `vec:dist2dsqr(other)` - Квадрат 2D расстояния
- `vec:distsqr(other)` - Квадрат Евклидова расстояния
- `vec:dist_to_ray(ray_start, ray_direction)` - Расстояние до луча
- `vec:dot(other)` - Скалярное произведение
- `vec:floor()` - Округляет координаты вниз
- `vec:in_range(other, range)` - Проверяет, находится ли в заданном расстоянии
- `vec:length()` - Длина вектора
- `vec:length2d()` - 2D длина вектора
- `vec:length2dsqr()` - Квадрат 2D длины вектора
- `vec:lengthsqr()` - Квадрат длины вектора
- `vec:lerp(other, weight)` - Линейная интерполяция
- `vec:normalize()` - Нормализует вектор, возвращает длину
- `vec:normalized()` - Возвращает нормализованную копию вектора
- `vec:scale(scalar)` - Умножает вектор на скаляр
- `vec:scaled(scalar)` - Возвращает копию вектора, умноженную на скаляр
- `vec:to(other)` - Возвращает направляющий вектор к другому вектору
- `vec:to_screen()` - Преобразует в экранные координаты
- `vec:unpack()` - Возвращает x, y, z координаты вектора
- `vec:vectors()` - Возвращает правый и верхний векторы от направляющего вектора

### Доступ к компонентам
```lua
local vec = vector(100, 200, 300)
print(vec.x, vec.y, vec.z)  -- 100, 200, 300

-- Изменение компонентов
vec.x = 10
vec.y = 20
vec.z = 30
```

### Пример использования
```lua
-- Нахождение ближайшего врага к перекрестию
events.render:set(function()
    local screen_center = render.screen_size() * 0.5
    
    local local_player = entity.get_local_player()
    if not local_player or not local_player:is_alive() then
        return
    end
    
    local camera_position = render.camera_position()
    local camera_angles = render.camera_angles()
    
    -- Преобразуем углы в направляющий вектор
    local direction = vector():angles(camera_angles)
    
    local closest_distance, closest_enemy = math.huge
    for _, enemy in ipairs(entity.get_players(true)) do
        local head_position = enemy:get_hitbox_position(1)
        
        -- Расстояние от головы до луча камеры
        local ray_distance = head_position:dist_to_ray(
            camera_position, direction
        )
        
        if ray_distance < closest_distance then
            closest_distance = ray_distance
            closest_enemy = enemy
        end
    end
    
    if closest_enemy then
        render.text(
            1,
            vector(screen_center.x, screen_center.y + 20),
            color(),
            "cd",
            string.format(
                "Ближайший враг к перекрестию: %s", closest_enemy:get_name()
            )
        )
    end
end)
```
