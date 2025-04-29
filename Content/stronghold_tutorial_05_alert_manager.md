# Bài 5: Thiết lập Stronghold Alert Manager

## Giới thiệu về Alert Manager
Alert Manager là lớp quản lý trạng thái cảnh báo trong game, bao gồm âm nhạc và hiệu ứng ánh sáng. Nó phản ứng với các sự kiện từ Game Manager để thay đổi không khí của game dựa trên trạng thái cảnh giác của lính canh.

## Tạo file Verse cho Alert Manager
1. Mở Verse Explorer
2. Nhấp chuột phải vào tên dự án
3. Chọn "Add new verse file to project"
4. Đặt tên file là "stronghold_alert_manager" và chọn "Create empty"

## Thêm mã Verse cho Alert Manager
1. Mở file Verse vừa tạo
2. Thêm các namespace cần thiết:
   ```verse
   using { /Fortnite.com/Devices }
   using { /Verse.org/Simulation }
   using { /UnrealEngine.com/Temporary/Diagnostics }
   using { /UnrealEngine.com/Temporary/SpatialMath }
   ```
3. Tạo lớp stronghold_alert_manager với các thuộc tính và phương thức cơ bản:
   ```verse
   stronghold_alert_manager := class(creative_device):
       # Tags cho đèn cảnh báo
       var alerted_lights_tag : tag = "alerted_lights"
       var combat_lights_tag : tag = "combat_lights"
       
       # Thuộc tính
       @editable var StrongholdGameManager : stronghold_game_manager = stronghold_game_manager{}
       @editable var RadioCombat : radio_device = radio_device{}
       @editable var RadioAlerted : radio_device = radio_device{}
       @editable var AlertedLights : []customizable_light_device = array{}
       @editable var CombatLights : []customizable_light_device = array{}
       
       # Phương thức OnBegin
       OnBegin<override>()<suspends>:void=
           # Đăng ký sự kiện từ Game Manager
           StrongholdGameManager.OnPlayerDetected.Subscribe(OnPlayerDetectedHandler)
           StrongholdGameManager.OnAllGuardsUnalerted.Subscribe(OnAllGuardsUnalertedHandler)
           
           # Tắt tất cả đèn và nhạc khi bắt đầu
           TurnOffAllLights()
           StopAllMusic()
   ```
4. Thêm các phương thức xử lý sự kiện và điều khiển đèn/nhạc:
   ```verse
   # Xử lý khi người chơi bị phát hiện
   OnPlayerDetectedHandler(Agent : agent):void=
       # Bật đèn cảnh báo và nhạc cảnh giác
       TurnOnAlertedLights()
       RadioAlerted.Play()
       
   # Xử lý khi tất cả lính canh không còn cảnh giác
   OnAllGuardsUnalertedHandler():void=
       # Tắt tất cả đèn và nhạc
       TurnOffAllLights()
       StopAllMusic()
       
   # Phương thức bật đèn cảnh báo
   TurnOnAlertedLights():void=
       # Tắt đèn chiến đấu trước
       for (Light : CombatLights):
           Light.TurnOff()
       
       # Bật đèn cảnh báo
       for (Light : AlertedLights):
           Light.TurnOn()
       
   # Phương thức tắt tất cả đèn
   TurnOffAllLights():void=
       for (Light : AlertedLights):
           Light.TurnOff()
       for (Light : CombatLights):
           Light.TurnOff()
       
   # Phương thức dừng tất cả nhạc
   StopAllMusic():void=
       RadioAlerted.Stop()
       RadioCombat.Stop()
   ```
5. Lưu file và quay lại UEFN

## Biên dịch mã Verse
1. Trong UEFN, nhấp vào menu "Verse"
2. Chọn "Build Verse Code" hoặc nhấn F8
3. Đợi quá trình biên dịch hoàn tất

## Thêm Alert Manager Device vào map
1. Mở Content Browser và tìm "Stronghold Alert Manager" trong Creative Devices
2. Kéo thiết bị vào map (vị trí không quan trọng)
3. Trong Details panel, thiết lập các thông số:
   - Stronghold Game Manager: Chọn Game Manager đã tạo trước đó

## Thêm Radio Devices
1. Tìm "Radio" trong Content Browser
2. Kéo hai Radio Device vào map
3. Đặt tên cho chúng (ví dụ: "RadioAlerted" và "RadioCombat")
4. Cấu hình mỗi Radio Device:
   - Chọn bản nhạc phù hợp (nhạc căng thẳng cho cảnh báo, nhạc chiến đấu cho combat)
   - Thiết lập âm lượng và các tùy chọn khác
5. Trong Alert Manager, gán hai Radio Device này vào các thuộc tính tương ứng

## Thêm Customizable Light Devices
1. Tìm "Customizable Light" trong Content Browser
2. Kéo nhiều Light Device vào map, đặt ở các vị trí chiến lược
3. Chia thành hai nhóm: đèn cảnh báo và đèn chiến đấu
4. Cấu hình mỗi Light Device:
   -