# Bài 15: Thêm Verse script vào devices

## Mục tiêu
- Hiểu cách tạo và thêm Verse script vào devices
- Học cách triển khai logic gameplay phức tạp bằng Verse
- Nắm vững cách các script tương tác với devices và với nhau

## 1. Giới thiệu về Verse script trong Stronghold Template

Trong dự án Stronghold Template, Verse script đóng vai trò quan trọng trong việc tạo ra logic gameplay phức tạp. Các script này sẽ điều khiển hành vi của lính canh, phản ứng khi người chơi bị phát hiện, và quản lý trạng thái trò chơi.

Chúng ta sẽ tạo và thêm các Verse script sau:
- **Stronghold Game Manager**: Quản lý trạng thái trò chơi tổng thể
- **Stronghold Leash Position**: Quản lý khu vực tuần tra của lính canh
- **Stronghold Alert Manager**: Quản lý âm nhạc và hiệu ứng khi lính canh phát hiện người chơi

## 2. Tạo Verse Device cho Stronghold Game Manager

Đầu tiên, chúng ta sẽ tạo Verse Device cho Stronghold Game Manager:

1. Trong UEFN, nhấp vào tab "Verse"
2. Chọn "New File" để tạo một file Verse mới
3. Chọn "Verse Device" và đặt tên là "Stronghold_Game_Manager"
4. Nhấp vào "Create"

![Tạo Verse Device](https://cdn2.unrealengine.com/create-verse-device-1920x1080-1920x1080-e5c9c1a9e5c7.png)

## 3. Viết code cho Stronghold Game Manager

Sau khi tạo Verse Device, bạn cần viết code cho nó. Double-click vào file Verse để mở editor và nhập code sau:

```verse
using { /Fortnite.com/AI }
using { /Fortnite.com/Characters }
using { /Fortnite.com/Devices }
using { /Fortnite.com/Game }
using { /UnrealEngine.com/Temporary/Diagnostics }
using { /UnrealEngine.com/Temporary/SpatialMath }
using { /Verse.org/Simulation }
using { /Verse.org/Verse }

# The Stronghold is a game mode in which the goal is for players to eliminate all hostile enemies at a heavily guarded Stronghold
stronghold_game_manager := class(creative_device):
    # References to the Guard Spawner devices that spawn the initial guards at the stronghold
    @editable
    Guards_InitialSpawners : []guard_spawner_device = array{}

    # References to the Guard Spawner devices that spawn reinforcements when the player is detected
    @editable
    Guards_ReinforcementSpawners : []guard_spawner_device = array{}

    # Reference to the Tracker device that tracks the number of guards eliminated
    @editable
    GuardTracker : tracker_device = tracker_device{}

    # Reference to the HUD Message device that displays a message when reinforcements are incoming
    @editable
    HUDMessage_Reinforcements : hud_message_device = hud_message_device{}

    # Reference to the HUD Message device that displays a message when guards are retreating
    @editable
    HUDMessage_Fallback : hud_message_device = hud_message_device{}

    # Reference to the End Game device that ends the game when all guards are eliminated (undetected)
    @editable
    EndGame_Undetected : end_game_device = end_game_device{}

    # Reference to the End Game device that ends the game when all guards are eliminated (detected)
    @editable
    EndGame_Detected : end_game_device = end_game_device{}

    # Reference to the End Game device that ends the game when the player fails
    @editable
    EndGame_Fail : end_game_device = end_game_device{}

    # Reference to the Item Granter device that grants items to the player
    @editable
    ItemGranter : item_granter_device = item_granter_device{}

    # Inner radius of the leash for guards at the stronghold
    @editable
    LeashInnerRadius : float = 1000.0

    # Outer radius of the leash for guards at the stronghold
    @editable
    LeashOuterRadius : float = 2000.0

    # Inner radius of the leash for guards at the fallback position
    @editable
    FallbackLeashInnerRadius : float = 500.0

    # Outer radius of the leash for guards at the fallback position
    @editable
    FallbackLeashOuterRadius : float = 1000.0

    # Whether to show debug information
    @editable
    ShowDebug : logic = false

    # The number of guards that need to be eliminated to win
    var GuardsToEliminate : int = 0

    # Whether the player has been detected
    var PlayerDetected : logic = false

    # Whether reinforcements have been spawned
    var ReinforcementsSpawned : logic = false

    # The agents of all guards
    var AllGuards : []agent = array{}

    # Event that is signaled when a guard is alerted
    GuardAlertedEvent : event(agent) = event(agent){}

    # Event that is signaled when all guards have lost track of the player
    AllGuardsUnalertedEvent : event() = event(){}

    # This function is called when the device is started in a running game
    OnBegin<override>()<suspends>:void=
        # Initialize the number of guards to eliminate
        set GuardsToEliminate = Guards_InitialSpawners.Length

        # Update the tracker target value
        GuardTracker.SetTargetValue(GuardsToEliminate)

        # Subscribe to events from the initial guard spawners
        for (Spawner : Guards_InitialSpawners):
            Spawner.SpawnedEvent.Subscribe(OnGuardSpawned)
            Spawner.EliminatedEvent.Subscribe(OnGuardEliminated)
            Spawner.AlertedEvent.Subscribe(OnGuardAlerted)
            Spawner.UnawareEvent.Subscribe(OnGuardUnaware)

        # Subscribe to events from the reinforcement guard spawners
        for (Spawner : Guards_ReinforcementSpawners):
            Spawner.SpawnedEvent.Subscribe(OnReinforcementSpawned)
            Spawner.EliminatedEvent.Subscribe(OnGuardEliminated)

        # Enable the initial guard spawners
        for (Spawner : Guards_InitialSpawners):
            Spawner.Enable()

        # Grant items to all players
        ItemGranter.GrantItems()

        # Start monitoring guard alertness
        spawn { MonitorGuardAlertness() }

    # This function is called when a guard is spawned
    OnGuardSpawned(Agent : agent) : void =
        if (ShowDebug):
            Print("Guard spawned: {Agent}")

        # Add the guard to the list of all guards
        set AllGuards = AllGuards + array{Agent}

    # This function is called when a reinforcement is spawned
    OnReinforcementSpawned(Agent : agent) : void =
        if (ShowDebug):
            Print("Reinforcement spawned: {Agent}")

        # Add the guard to the list of all guards
        set AllGuards = AllGuards + array{Agent}

        # Increase the number of guards to eliminate
        set GuardsToEliminate += 1

        # Update the tracker target value
        GuardTracker.SetTargetValue(GuardsToEliminate)

    # This function is called when a guard is eliminated
    OnGuardEliminated(Result : device_ai_interaction_result) : void =
        if (ShowDebug):
            Print("Guard eliminated by {Result.Agent}")

        # Increment the tracker
        GuardTracker.Increment()

        # Check if all guards have been eliminated
        if (GuardTracker.GetCurrentValue() >= GuardsToEliminate):
            if (PlayerDetected):
                # End the game (detected)
                EndGame_Detected.Activate(Result.Agent)
            else:
                # End the game (undetected)
                EndGame_Undetected.Activate(Result.Agent)

    # This function is called when a guard is alerted
    OnGuardAlerted(Agent : agent) : void =
        if (ShowDebug):
            Print("Guard alerted: {Agent}")

        # Set player detected flag
        set PlayerDetected = true

        # Signal the guard alerted event
        GuardAlertedEvent.Signal(Agent)

        # Spawn reinforcements if not already spawned
        if (not ReinforcementsSpawned):
            set ReinforcementsSpawned = true
            HUDMessage_Reinforcements.Show()

            # Enable reinforcement spawners
            for (Spawner : Guards_ReinforcementSpawners):
                Spawner.Enable()

    # This function is called when a guard becomes unaware
    OnGuardUnaware(Agent : agent) : void =
        if (ShowDebug):
            Print("Guard unaware: {Agent}")

    # This function monitors the alertness of all guards
    MonitorGuardAlertness()<suspends>:void=
        loop:
            # Wait for a short time
            Sleep(1.0)

            # Skip if player has not been detected
            if (not PlayerDetected):
                continue

            # Check if any guard is still alerted
            var AnyGuardAlerted : logic = false
            for (Guard : AllGuards):
                if (Character := Guard.GetFortCharacter[]):
                    if (GuardPerception := Character.GetFortGuardPerception[]):
                        if (GuardPerception.GetAlertLevel() = fort_guard_alert_level.Alerted or 
                            GuardPerception.GetAlertLevel() = fort_guard_alert_level.LostTarget):
                            set AnyGuardAlerted = true
                            break

            # If no guard is alerted, signal the all guards unalerted event
            if (not AnyGuardAlerted and PlayerDetected):
                set PlayerDetected = false
                AllGuardsUnalertedEvent.Signal()
                HUDMessage_Fallback.Show()
```

Sau khi nhập code, nhấp vào "Build Verse Code" để biên dịch script.

![Build Verse Code](https://cdn2.unrealengine.com/build-verse-code-1920x1080-1920x1080-e5c9c1a9e5c7.png)

## 4. Thêm Stronghold Game Manager vào map

Sau khi biên dịch script, bạn cần thêm Stronghold Game Manager vào map:

1. Trong Content Browser, điều hướng đến All/[Tên Dự Án]/CreativeDevices/
2. Tìm và chọn Stronghold_Game_Manager
3. Kéo Stronghold_Game_Manager vào map
4. Với Stronghold_Game_Manager được chọn, cấu hình các tùy chọn trong panel Details:

| Option | Value | Explanation |
|--------|-------|-------------|
| Visible in Game | True | Device này sẽ hiển thị trong game |
| Enabled at Game Start | True | Device này sẽ được bật khi game bắt đầu |
| Guards_InitialSpawners | 3 Array elements | Thêm 3 phần tử vào thiết lập này |
| 0 | Guard Spawner Init | Đây là mảng tất cả các devices được sử dụng để spawn các Guards ban đầu tại pháo đài |
| 1 | Guard Spawner Sniper Tower 1 | |
| 2 | Guard Spawner Sniper Tower 2 | |
| Guards_ReinforcementSpawners | 4 Array elements | Thêm 4 phần tử vào thiết lập này |
| 0 | Guard Spawner Reinforcement 1 | Đây là mảng tất cả các devices được sử dụng để spawn các Guards tiếp viện |
| 1 | Guard Spawner Reinforcement 2 | |
| 2 | Guard Spawner Reinforcement 3 | |
| 3 | Guard Spawner Reinforcement 4 | |
| GuardTracker | Tracker | Tham chiếu đến Tracker device |
| HUDMessage_Reinforcements | HUD Message Reinforcements | Tham chiếu đến HUD Message device cho tiếp viện |
| HUDMessage_Fallback | HUD Message Fallback | Tham chiếu đến HUD Message device cho fallback |
| EndGame_Undetected | End Game Undetected | Tham chiếu đến End Game device cho undetected |
| EndGame_Detected | End Game Detected | Tham chiếu đến End Game device cho detected |
| EndGame_Fail | End Game Fail | Tham chiếu đến End Game device cho fail |
| ItemGranter | Item Granter | Tham chiếu đến Item Granter device |
| LeashInnerRadius | 1000.0 | Bán kính trong của leash cho guards tại pháo đài |
| LeashOuterRadius | 2000.0 | Bán kính ngoài của leash cho guards tại pháo đài |
| FallbackLeashInnerRadius | 500.0 | Bán kính trong của leash cho guards tại vị trí fallback |
| FallbackLeashOuterRadius | 1000.0 | Bán kính ngoài của leash cho guards tại vị trí fallback |
| ShowDebug | True | Hiển thị thông tin debug |

![Stronghold Game Manager](https://cdn2.unrealengine.com/stronghold-game-manager-1920x1080-1920x1080-e5c9c1a9e5c7.png)

## 5. Tạo Verse Device cho Stronghold Leash Position

Tiếp theo, chúng ta sẽ tạo Verse Device cho Stronghold Leash Position:

1. Trong UEFN, nhấp vào tab "Verse"
2. Chọn "New File" để tạo một file Verse mới
3. Chọn "Verse Device" và đặt tên là "Stronghold_Leash_Position"
4. Nhấp vào "Create"

## 6. Viết code cho Stronghold Leash Position

Sau khi tạo Verse Device, bạn cần viết code cho nó. Double-click vào file Verse để mở editor và nhập code sau:

```verse
using { /Fortnite.com/AI }
using { /Fortnite.com/Characters }
using { /Fortnite.com/Devices }
using { /UnrealEngine.com/Temporary/SpatialMath }
using { /Verse.org/Random }
using { /Verse.org/Simulation }

# Defines a leash volume that can be assigned to guards
stronghold_leash_position := class(creative_device):
    # Leash is applied by default to all guards spawned by those devices
    @editable
    GuardsSpawners : []guard_spawner_device = array{}

    # Guards on those patrol paths can go outside the leash (only one device per path)
    @editable
    PatrolPaths : []ai_patrol_path_device = array{}

    # Set the leash inner radius. This value must be in centimeters.
    # This defines the volume that must be reached when this leash is assigned to guards
    @editable
    LeashInnerRadius : float = 1000.0

    # Set the leash outer radius. This value must be in centimeters.
    # This defines the volume that guards will try to stay within
    @editable
    LeashOuterRadius : float = 2000.0

    # Whether to show debug information
    @editable
    ShowDebug : logic = false

    # This function is called when the device is started in a running game
    OnBegin<override>()<suspends>:void=
        # Subscribe to events from the guard spawners
        for (Spawner : GuardsSpawners):
            Spawner.SpawnedEvent.Subscribe(OnGuardSpawned)

        # Set up patrol paths
        for (PatrolPath : PatrolPaths):
            PatrolPath.Enable()

    # This function is called when a guard is spawned
    OnGuardSpawned(Agent : agent) : void =
        if (ShowDebug):
            Print("Setting leash for guard: {Agent}")

        # Set the leash for the guard
        if (Character := Agent.GetFortCharacter[]):
            if (Leashable := Character.GetFortLeashable[]):
                # Get the position of this device
                Position := GetTransform().Translation

                # Set the leash position
                Leashable.SetLeashPosition(Position, LeashInnerRadius, LeashOuterRadius)

                if (ShowDebug):
                    Print("Leash set at position {Position} with inner radius {LeashInnerRadius} and outer radius {LeashOuterRadius}")
```

Sau khi nhập code, nhấp vào "Build Verse Code" để biên dịch script.

## 7. Thêm Stronghold Leash Position vào map

Sau khi biên dịch script, bạn cần thêm Stronghold Leash Position vào map:

1. Trong Content Browser, điều hướng đến All/[Tên Dự Án]/CreativeDevices/
2. Tìm và chọn Stronghold_Leash_Position
3. Kéo hai Stronghold_Leash_Position vào map, một cho pháo đài và một cho vị trí fallback
4. Với mỗi Stronghold_Leash_Position được chọn, cấu hình các tùy chọn trong panel Details:

### Stronghold Leash

| Option | Value | Explanation |
|--------|-------|-------------|
| Visible in Game | False | Device này sẽ không hiển thị trong game |
| GuardsSpawners | 3 Array elements | Thêm 3 phần tử vào thiết lập này |
| 0 | Guard Spawner Init | Đây là mảng tất cả các devices được sử dụng để spawn các Guards tại pháo đài |
| 1 | Guard Spawner Sniper Tower 1 | |
| 2 | Guard Spawner Sniper Tower 2 | |
| PatrolPaths | 0 Array elements | Không có patrol paths cho leash này |
| LeashInnerRadius | 1000.0 | Bán kính trong của leash |
| LeashOuterRadius | 2000.0 | Bán kính ngoài của leash |
| ShowDebug | True | Hiển thị thông tin debug |

### Fallback Leash

| Option | Value | Explanation |
|--------|-------|-------------|
| Visible in Game | False | Device này sẽ không hiển thị trong game |
| GuardsSpawners | 4 Array elements | Thêm 4 phần tử vào thiết lập này |
| 0 | Guard Spawner Reinforcement 1 | Đây là mảng tất cả các devices được sử dụng để spawn các Guards tiếp viện |
| 1 | Guard Spawner Reinforcement 2 | |
| 2 | Guard Spawner Reinforcement 3 | |
| 3 | Guard Spawner Reinforcement 4 | |
| PatrolPaths | 0 Array elements | Không có patrol paths cho leash này |
| LeashInnerRadius | 500.0 | Bán kính trong của leash |
| LeashOuterRadius | 1000.0 | Bán kính ngoài của leash |
| ShowDebug | True | Hiển thị thông tin debug |

![Stronghold Leash Position](https://cdn2.unrealengine.com/stronghold-leash-position-1920x1080-1920x1080-e5c9c1a9e5c7.png)

## 8. Tạo Verse Device cho Stronghold Alert Manager

Cuối cùng, chúng ta sẽ tạo Verse Device cho Stronghold Alert Manager:

1. Trong UEFN, nhấp vào tab "Verse"
2. Chọn "New File" để tạo một file Verse mới
3. Chọn "Verse Device" và đặt tên là "Stronghold_Alert_Manager"
4. Nhấp vào "Create"

## 9. Viết code cho Stronghold Alert Manager

Sau khi tạo Verse Device, bạn cần viết code cho nó. Double-click vào file Verse để mở editor và nhập code sau:

```verse
using { /Verse.org/Simulation }
using { /Verse.org/Simulation/Tags }
using { /Verse.org/Colors }
using { /UnrealEngine.com/Temporary/Diagnostics }
using { /Fortnite.com/Devices }

# tags for customizable lights
alerted_lights_tag := class(tag){}
combat_lights_tag := class(tag){}

# Script that handles music and turn on lights when guards are alerted
stronghold_alert_manager := class(creative_device):
    # Reference to the Game Manager to monitor perception events
    @editable
    StrongholdGameManager : stronghold_game_manager = stronghold_game_manager{}

    # Reference to Radio that plays combat music
    @editable
    RadioCombat : radio_device = radio_device{}

    # Reference to Radio that plays alerted music
    @editable
    RadioAlerted : radio_device = radio_device{}

    # Reference to Customizable Light devices that turn on when guards are alerted
    @editable
    AlertedLights : []customizable_light_device = array{}

    # Reference to Customizable Light devices that turn on when guards are in combat
    @editable
    CombatLights : []customizable_light_device = array{}

    # Whether to show debug information
    @editable
    ShowDebug : logic = false

    # This function is called when the device is started in a running game
    OnBegin<override>()<suspends>:void=
        # Subscribe to events from the Game Manager
        StrongholdGameManager.GuardAlertedEvent.Subscribe(OnGuardAlerted)
        StrongholdGameManager.AllGuardsUnalertedEvent.Subscribe(OnAllGuardsUnalerted)

        # Turn off all lights initially
        for (Light : AlertedLights):
            Light.TurnOff()

        for (Light : CombatLights):
            Light.TurnOff()

        # Stop all radios initially
        RadioCombat.Stop()
        RadioAlerted.Stop()

    # This function is called when a guard is alerted
    OnGuardAlerted(Agent : agent) : void =
        if (ShowDebug):
            Print("Alert Manager: Guard alerted")

        # Turn on combat lights
        for (Light : CombatLights):
            Light.TurnOn()

        # Turn off alerted lights
        for (Light : AlertedLights):
            Light.TurnOff()

        # Play combat music
        RadioAlerted.Stop()
        RadioCombat.Play()

    # This function is called when all guards have lost track of the player
    OnAllGuardsUnalerted() : void =
        if (ShowDebug):
            Print("Alert Manager: All guards unalerted")

        # Turn on alerted lights
        for (Light : AlertedLights):
            Light.TurnOn()

        # Turn off combat lights
        for (Light : CombatLights):
            Light.TurnOff()

        # Play alerted music
        RadioCombat.Stop()
        RadioAlerted.Play()
```

Sau khi nhập code, nhấp vào "Build Verse Code" để biên dịch script.

## 10. Thêm Stronghold Alert Manager vào map

Sau khi biên dịch script, bạn cần thêm Stronghold Alert Manager vào map:

1. Trong Content Browser, điều hướng đến All/[Tên Dự Án]/CreativeDevices/
2. Tìm và chọn Stronghold_Alert_Manager
3. Kéo Stronghold_Alert_Manager vào map
4. Với Stronghold_Alert_Manager được chọn, cấu hình các tùy chọn trong panel Details:

| Option | Value | Explanation |
|--------|-------|-------------|
| Visible in Game | True | Device này sẽ hiển thị trong game |
| StrongholdGameManager | Stronghold_Game_Manager | Tham chiếu đến Stronghold Game Manager |
| RadioCombat | Radio Combat | Tham chiếu đến Radio device cho nhạc chiến đấu |
| RadioAlerted | Radio Alerted | Tham chiếu đến Radio device cho nhạc cảnh báo |
| AlertedLights | Array elements | Thêm các Customizable Light devices cho trạng thái cảnh báo |
| CombatLights | Array elements | Thêm các Customizable Light devices cho trạng thái chiến đấu |
| ShowDebug | True | Hiển thị thông tin debug |

![Stronghold Alert Manager](https://cdn2.unrealengine.com/stronghold-alert-manager-1920x1080-1920x1080-e5c9c1a9e5c7.png)

## 11. Thêm Radio Devices

Để hoàn thành thiết lập, bạn cần thêm Radio Devices cho nhạc:

1. Trong Creative Mode, mở tab Devices và tìm "Radio"
2. Đặt hai Radio Devices vào map
3. Cấu hình Radio Devices như sau:

### Radio Combat

| Option | Value | Explanation |
|--------|-------|-------------|
| Audio | Music_StW_High_Combat01_Cue | Nhạc chiến đấu khi người chơi bị phát hiện |
| Auto Play | False | Radio sẽ không tự động phát |
| Auto Stop | False | Radio sẽ không tự động dừng |
| Loop | True | Nhạc sẽ lặp lại |

### Radio Alerted

| Option | Value | Explanation |
|--------|-------|-------------|
| Audio | Music_StW_Low_Combat01_Cue | Nhạc cảnh báo khi lính canh đang tìm kiếm |
| Auto Play | False | Radio sẽ không tự động phát |
| Auto Stop | False | Radio sẽ không tự động dừng |
| Loop | True | Nhạc sẽ lặp lại |

![Radio Devices](https://cdn2.unrealengine.com/radio-devices-1920x1080-1920x1080-e5c9c1a9e5c7.png)

## 12. Thêm Customizable Light Devices

Cuối cùng, bạn cần thêm Customizable Light Devices cho hiệu ứng ánh sáng:

1. Trong Creative Mode, mở tab Devices và tìm "Customizable Light"
2. Đặt nhiều Customizable Light Devices vào map, một số cho trạng thái cảnh báo và một số cho trạng thái chiến đấu
3. Cấu hình Customizable Light Devices như sau:

### Alerted Lights

| Option | Value | Explanation |
|--------|-------|-------------|
| Light Color | Yellow | Màu vàng cho trạng thái cảnh báo |
| Light Intensity | 5000 | Cường độ ánh sáng |
| Light Radius | 1000 | Bán kính ánh sáng |
| Auto On | False | Đèn sẽ không tự động bật |

### Combat Lights

| Option | Value | Explanation |
|--------|-------|-------------|
| Light Color | Red | Màu đỏ cho trạng thái chiến đấu |
| Light Intensity | 5000 | Cường độ ánh sáng |
| Light Radius | 1000 | Bán kính ánh sáng |
| Auto On | False | Đèn sẽ không tự động bật |

![Customizable Light Devices](https://cdn2.unrealengine.com/customizable-light-devices-1920x1080-1920x1080-e5c9c1a9e5c7.png)

## 13. Lưu dự án

Sau khi hoàn thành việc thêm và cấu hình tất cả các Verse scripts và devices, đừng quên lưu dự án của bạn:

1. Nhấp vào "File" > "Save All" hoặc nhấn Ctrl+Shift+S
2. Nhấp vào "Save"

## Tóm tắt

Trong bài học này, bạn đã học:
- Cách tạo Verse Device cho Stronghold Game Manager, Stronghold Leash Position và Stronghold Alert Manager
- Cách viết code Verse để quản lý trạng thái trò chơi, khu vực tuần tra của lính canh và hiệu ứng khi lính canh phát hiện người chơi
- Cách thêm và cấu hình các Verse scripts vào map
- Cách thêm và cấu hình Radio Devices và Customizable Light Devices để tạo hiệu ứng âm thanh và ánh sáng

Trong bài học tiếp theo, chúng ta sẽ học cách thiết lập Leash Devices cho AI tuần tra.

## Câu hỏi suy ngẫm
1. Làm thế nào Stronghold Game Manager, Stronghold Leash Position và Stronghold Alert Manager tương tác với nhau để tạo ra một trải nghiệm gameplay hoàn chỉnh?
2. Tại sao việc sử dụng events trong Verse lại quan trọng trong việc tạo ra các phản ứng động trong game?
3. Làm thế nào bạn có thể mở rộng các scripts hiện có để thêm các tính năng mới như các loại lính canh khác nhau hoặc các mục tiêu phụ?
4. Làm thế nào các hiệu ứng âm thanh và ánh sáng góp phần tạo ra không khí và phản hồi cho người chơi trong một trò chơi stealth?
