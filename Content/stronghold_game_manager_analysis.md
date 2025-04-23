# Phân tích file stronghold_game_manager.verse

## Mục đích
`stronghold_game_manager` là lớp chính quản lý toàn bộ trạng thái và logic của trò chơi Stronghold. Nó điều phối các thành phần khác và xử lý các sự kiện chính trong game.

## Cấu trúc lớp

### Thuộc tính chính
- **GuardsInitialSpawners**: Mảng các Guard Spawner Devices tạo ra lính canh ban đầu tại pháo đài
- **GuardsInitialSpawnersAdditional**: Mảng các Guard Spawner Devices bổ sung cho chế độ nhiều người chơi
- **GuardsReinforcementSpawners**: Mảng các Guard Spawner Devices tạo ra lính tiếp viện khi người chơi bị phát hiện
- **GuardTracker**: Tracker Device theo dõi số lượng lính canh bị tiêu diệt
- **StrongholdLeashReference**: Tham chiếu đến Leash Position của pháo đài
- **FallbackLeashReference**: Tham chiếu đến Leash Position của vị trí fallback

### Biến trạng thái
- **StrongholdGuards**: Mảng tất cả các lính canh tại pháo đài
- **ReinforcementGuards**: Mảng các lính tiếp viện
- **PlayerDetected**: Trạng thái người chơi có bị phát hiện hay không
- **DetectedPlayer**: Người chơi đã bị phát hiện
- **AnyGuardAlerted**: Có lính canh nào đang trong trạng thái cảnh giác không

### Events
- **PlayerDetectedEvent**: Kích hoạt khi người chơi bị phát hiện
- **AllGuardsUnalertedEvent**: Kích hoạt khi tất cả lính canh trở về trạng thái không cảnh giác
- **AllGuardsEliminatedEvent**: Kích hoạt khi tất cả lính canh bị tiêu diệt

## Các phương thức chính

### OnBegin
Phương thức này được gọi khi trò chơi bắt đầu. Nó khởi tạo các biến trạng thái và thiết lập các sự kiện theo dõi.

### MonitorGuardPerception
Phương thức này liên tục theo dõi trạng thái nhận thức của tất cả lính canh. Nó kiểm tra xem có lính canh nào đang trong trạng thái cảnh giác không và cập nhật trạng thái game tương ứng.

### OnGuardSpawned
Được gọi khi một lính canh được tạo ra. Nó thêm lính canh vào mảng StrongholdGuards và tăng biến đếm NumGuardsSpawned.

### OnReinforcementSpawned
Được gọi khi một lính tiếp viện được tạo ra. Nó thêm lính tiếp viện vào mảng ReinforcementGuards, áp dụng leash và chỉ định mục tiêu tấn công.

### OnGuardEliminated
Được gọi khi một lính canh bị tiêu diệt. Nó cập nhật trạng thái game và kiểm tra xem tất cả lính canh đã bị tiêu diệt chưa.

### SpawnReinforcements
Tạo ra lính tiếp viện khi người chơi bị phát hiện. Số lượng lính tiếp viện phụ thuộc vào số lượng người chơi.

## Luồng hoạt động
1. Khi trò chơi bắt đầu, `OnBegin` được gọi để khởi tạo trạng thái
2. `MonitorGuardPerception` liên tục theo dõi trạng thái nhận thức của lính canh
3. Khi người chơi bị phát hiện, `PlayerDetectedEvent` được kích hoạt và `SpawnReinforcements` được gọi
4. Khi tất cả lính canh trở về trạng thái không cảnh giác, `AllGuardsUnalertedEvent` được kích hoạt
5. Khi tất cả lính canh bị tiêu diệt, `AllGuardsEliminatedEvent` được kích hoạt

## Tương tác với các thành phần khác
- Tương tác với `stronghold_leash_position` để quản lý khu vực hoạt động của lính canh
- Cung cấp sự kiện cho `stronghold_alert_manager` và `stronghold_bark_manager` để phản hồi trạng thái game
- Điều khiển Guard Spawner Devices để tạo ra lính canh và lính tiếp viện