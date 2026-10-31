MIFAOGAMES / WiFiLobby — ЭТАП 1: серверные снимки состояния

Добавлен scripts/server_persistence.gd и autoload ServerPersistence.
При роли host каждые 60 секунд создаётся user://server_saves/host_snapshot.json.
При сворачивании приложения также выполняется попытка сохранить снимок.
Снимок включает профиль Host, временный боевой инвентарь Host и roster игроков.
ServerPersistence.read_snapshot() читает сохранение, но НЕ применяет его автоматически.
Это сознательное ограничение: текущий проект не содержит полноценного серверного
хранилища состояния каждого клиента, а roster не заменяет полный инвентарь игроков.

ВАЖНО: ЭТО НЕ ПОЛНОЦЕННЫЙ ANDROID FOREGROUND SERVICE.
Сейчас ENet и игровая симуляция работают в Godot. При сворачивании Android
может остановить игровой цикл, поэтому клиенты могут потерять соединение.
Чтобы реализовать непрерывную работу, необходимо перенести authoritative game
simulation + ENet в независимый процесс/сервис Android (например Kotlin service
с native Godot headless или самостоятельным серверным runtime), обеспечить IPC
и Android notification actions, а затем проверить ограничения Android 14+.
Просто уведомление и Kotlin-сервис не способны продолжить текущую GDScript
симуляцию после остановки Godot.

Текущий Online Host использует UDP 24567 (см. ONLINE_README_RU.txt).
