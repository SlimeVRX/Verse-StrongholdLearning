# Bài 4: Thiết lập Stronghold Game Manager

## Giới thiệu về Game Manager
Stronghold Game Manager là lớp chính quản lý toàn bộ trạng thái và logic của trò chơi. Nó điều phối các thành phần khác, xử lý các sự kiện chính và quản lý luồng gameplay.

## Tạo file Verse cho Game Manager
1. Mở Verse Explorer
2. Nhấp chuột phải vào tên dự án
3. Chọn "Add new verse file to project"
4. Đặt tên file là "stronghold_game_manager" và chọn "Create empty"

## Thêm mã Verse cho Game Manager
1. Mở file Verse vừa tạo
2. Thêm các namespace cần thiết:
   ```verse
   using { /Fortnite.com/AI }
   using { /Fortnite.com/Characters }
   using { /Fortnite.com/Devices }
   using { /Fortnite.com/Game }
   using { /UnrealEngine.com/Temporary/Diagnostics }
   using { /UnrealEngine.com/Temporary/SpatialMath }
   using { /Verse.org/Simulation }
   using { /Verse.org/Verse }
   ```
3. Tạo lớp stronghold_game_manager với các thuộc tính và phương thức cơ bản:
   ```verse
   stronghold_game_manager := class(creative_device):
       # Thuộc tính
       @editable var LeashPositions : []stronghold_leash_position = array{}
       @editable var FallbackPosition : stronghold_leash_position = stronghold_leash_position{}
       @editable var GuardSpawners : []guard_spawner_device = array{}
       @editable var ReinforcementSpawners : []guard_spawner_device = array{}
       @editable var HUDMessageDeviceDetected : hud_message_device = hud_message_device{}
       @editable var HUDMessageDeviceUndetected : hud_message_device = hud_message_device{}
       @editable var HUDMessageDeviceFallback : hud_message_device = hud_message_device{}
       @editable var HUDMessageDeviceReinforcements : hud_message_device = hud_message_device{}
       
       # Biến trạng thái
       var GuardsAlerted : int = 0
       var GuardsTotal : int = 0
       var ReinforcementsSpawned : logic = false
       
       # Sự kiện
       OnGuardEliminated : event(Agent : agent) = event(Agent : agent){}
       OnPlayerDetected : event(Agent : agent) = event(Agent : agent){}
       OnAllGuardsUnalerted : event() = event(){}
       OnReinforcementsSpawned : event() = event(){}
       
       # Phương thức OnBegin
       OnBegin<override>()<suspends>:void=
           # Khởi tạo số lượng lính canh
           set GuardsTotal = GetTotalGuards()
           
           # Đăng ký sự kiện cho mỗi guard spawner
           for (GuardSpawner : GuardSpawners):
               GuardSpawner.EliminatedEvent.Subscribe(OnGuardEliminatedHandler)
               GuardSpawner.AlertedEvent.Subscribe(OnGuardAlertedHandler)
               GuardSpawner.UnalertedEvent.Subscribe(OnGuardUnalertedHandler)
   ```
4. Thêm các phương thức xử lý sự kiện:
   ```verse
   # Xử lý khi lính canh bị tiêu diệt
   OnGuardEliminatedHandler(Agent : agent):void=
       OnGuardEliminated.Signal(Agent)
       
   # Xử lý khi lính canh phát hiện người chơi
   OnGuardAlertedHandler(Agent : agent):void=
       set GuardsAlerted = GuardsAlerted + 1
       if (GuardsAlerted = 1):
           HUDMessageDeviceDetected.Show()
           OnPlayerDetected.Signal(Agent)
           if (not ReinforcementsSpawned):
               SpawnReinforcements()
               
   # Xử lý khi lính canh không còn cảnh giác
   OnGuardUnalertedHandler(Agent : agent):void=
       set GuardsAlerted = Max(GuardsAlerted - 1, 0)
       if (GuardsAlerted = 0):
           HUDMessageDeviceUndetected.Show()
           OnAllGuardsUnalerted.Signal()
           
   # Phương thức tạo lính tiếp viện
   SpawnReinforcements():void=
       set ReinforcementsSpawned = true
       HUDMessageDeviceReinforcements.Show()
       for (ReinforcementSpawner : ReinforcementSpawners):
           ReinforcementSpawner.Spawn()
       OnReinforcementsSpawned.Signal()
       
   # Phương thức lấy tổng số lính canh
   GetTotalGuards():int=
       var Total:int = 0
       for (GuardSpawner : GuardSpawners):
           set Total = Total + GuardSpawner.SpawnLimit
       return Total
   ```
5. Lưu file và quay lại UEFN

## Biên dịch mã Verse
1. Trong UEFN, nhấp vào menu "Verse"
2. Chọn "Build Verse Code" hoặc nhấn F8
3. Đợi quá trình biên dịch hoàn tất

## Thêm Game Manager Device vào map
1. Mở Content Browser và tìm "Stronghold Game Manager" trong Creative Devices
2. Kéo thiết bị vào map (vị trí không quan trọng)
3. Trong Details panel, thiết lập các thông số:
   - Leash Positions: Thêm các Leash Position đã tạo trước đó
   - Fallback Position: Chọn Leash Position đã đánh dấu là Fallback
   - Guard Spawners: Sẽ thêm sau khi tạo các Guard Spawner
   - Reinforcement Spawners: Sẽ thêm sau khi tạo các Reinforcement Spawner
   - HUD Message Devices: Sẽ thêm sau khi tạo các HUD Message Device

## Vai trò của Game Manager trong hệ thống
- **Điều phối**: Quản lý tất cả các thành phần khác trong hệ thống
- **Xử lý sự kiện**: Phản ứng với các sự kiện như lính canh bị tiêu diệt, người chơi bị phát hiện
- **Quản lý trạng thái**: Theo dõi trạng thái của trò chơi (số lượng lính canh, trạng thái cảnh giác)
- **Tạo tiếp viện**: Quản lý việc tạo lính tiếp viện khi người chơi bị phát hiện