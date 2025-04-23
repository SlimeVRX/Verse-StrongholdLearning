# Bài 16: Thiết lập Leash Devices cho AI tuần tra

## Mục tiêu
- Hiểu về khái niệm Leash trong AI tuần tra
- Học cách thiết lập và cấu hình AI Patrol Path Devices
- Nắm vững cách kết hợp Leash và Patrol Paths để tạo hành vi tuần tra phức tạp

## 1. Giới thiệu về Leash và AI tuần tra

Trong dự án Stronghold Template, việc thiết lập hành vi tuần tra cho AI là một phần quan trọng để tạo ra trải nghiệm stealth thú vị. Có hai khái niệm chính cần hiểu:

- **Leash**: Xác định khu vực mà AI có thể di chuyển. AI sẽ cố gắng ở trong khu vực này và quay lại nếu đi ra ngoài.
- **Patrol Path**: Xác định đường đi cụ thể mà AI sẽ tuần tra theo.

Kết hợp Leash và Patrol Paths, bạn có thể tạo ra các hành vi tuần tra phức tạp và thực tế cho AI.

## 2. Hiểu về Leash trong Verse

Trong bài học trước, chúng ta đã tạo Stronghold_Leash_Position để quản lý khu vực tuần tra của lính canh. Hãy nhớ lại cách Leash hoạt động trong Verse:

```verse
# Đặt leash cho guard
if (Character := Agent.GetFortCharacter[]):
    if (Leashable := Character.GetFortLeashable[]):
        # Lấy vị trí của device này
        Position := GetTransform().Translation
        
        # Đặt vị trí leash
        Leashable.SetLeashPosition(Position, LeashInnerRadius, LeashOuterRadius)
```

Leash có hai bán kính:
- **Inner Radius**: Khu vực mà AI phải đạt đến khi được gán leash
- **Outer Radius**: Khu vực mà AI sẽ cố gắng ở trong

![Leash Concept](https://cdn2.unrealengine.com/leash-concept-1920x1080-1920x1080-e5c9c1a9e5c7.png)

## 3. Thêm AI Patrol Path Devices

Bây giờ, chúng ta sẽ thêm AI Patrol Path Devices để tạo đường đi cụ thể cho lính canh:

1. Trong Creative Mode, mở tab Devices và tìm "AI Patrol Path"
2. Đặt một AI Patrol Path Device vào map
3. Cấu hình AI Patrol Path Device như sau:

| Option | Value | Explanation |
|--------|-------|-------------|
| Visible in Game | False | Device này sẽ không hiển thị trong game |
| Patrol Path Group | 1 | Nhóm đường tuần tra. Lính canh sẽ tuần tra theo các đường trong cùng một nhóm |
| Patrol Path Type | Bidirectional | Lính canh sẽ đi theo cả hai hướng trên đường tuần tra |
| Patrol Path Spacing | 500.0 | Khoảng cách giữa các lính canh trên cùng một đường tuần tra |

![AI Patrol Path](https://cdn2.unrealengine.com/ai-patrol-path-1920x1080-1920x1080-e5c9c1a9e5c7.png)

## 4. Thêm AI Patrol Path Node Devices

Sau khi thêm AI Patrol Path Device, bạn cần thêm các AI Patrol Path Node Devices để xác định các điểm trên đường tuần tra:

1. Trong Creative Mode, mở tab Devices và tìm "AI Patrol Path Node"
2. Đặt nhiều AI Patrol Path Node Devices vào map để tạo đường tuần tra
3. Cấu hình mỗi AI Patrol Path Node Device như sau:

| Option | Value | Explanation |
|--------|-------|-------------|
| Visible in Game | False | Device này sẽ không hiển thị trong game |
| Patrol Path | AI Patrol Path 1 | Đường tuần tra mà node này thuộc về |
| Wait Time Min | 2.0 | Thời gian tối thiểu mà lính canh sẽ đợi tại node này |
| Wait Time Max | 5.0 | Thời gian tối đa mà lính canh sẽ đợi tại node này |

![AI Patrol Path Node](https://cdn2.unrealengine.com/ai-patrol-path-node-1920x1080-1920x1080-e5c9c1a9e5c7.png)

## 5. Tạo nhiều đường tuần tra

Để tạo một hệ thống tuần tra phức tạp, bạn nên tạo nhiều đường tuần tra khác nhau:

1. Tạo một đường tuần tra cho khu vực chính của pháo đài
2. Tạo một đường tuần tra cho tháp canh
3. Tạo một đường tuần tra cho khu vực xung quanh pháo đài

Mỗi đường tuần tra nên có một Patrol Path Group khác nhau để quản lý riêng biệt.

![Multiple Patrol Paths](https://cdn2.unrealengine.com/multiple-patrol-paths-1920x1080-1920x1080-e5c9c1a9e5c7.png)

## 6. Cấu hình Guard Spawner Devices để sử dụng Patrol Paths

Sau khi tạo các đường tuần tra, bạn cần cấu hình Guard Spawner Devices để sử dụng chúng:

1. Chọn Guard Spawner Device
2. Trong panel Details, tìm mục "Spawn On Patrol Path Group"
3. Đặt giá trị thành nhóm đường tuần tra tương ứng (ví dụ: 1 cho đường tuần tra chính)

![Guard Spawner Patrol Path](https://cdn2.unrealengine.com/guard-spawner-patrol-path-1920x1080-1920x1080-e5c9c1a9e5c7.png)

## 7. Cập nhật Stronghold_Leash_Position để hỗ trợ Patrol Paths

Bây giờ, chúng ta cần cập nhật Stronghold_Leash_Position để hỗ trợ các Patrol Paths:

1. Chọn Stronghold_Leash_Position cho pháo đài
2. Trong panel Details, tìm mục "PatrolPaths"
3. Thêm các AI Patrol Path Devices vào mảng này

![Leash Position Patrol Paths](https://cdn2.unrealengine.com/leash-position-patrol-paths-1920x1080-1920x1080-e5c9c1a9e5c7.png)

## 8. Tạo Leash Fallback cho khi lính canh mất dấu người chơi

Khi lính canh mất dấu người chơi, chúng nên quay lại một vị trí an toàn. Chúng ta sẽ sử dụng Leash Fallback cho mục đích này:

1. Đảm bảo rằng Stronghold_Leash_Position thứ hai (cho vị trí fallback) đã được đặt ở một vị trí phù hợp
2. Cấu hình Stronghold_Game_Manager để sử dụng Leash Fallback khi lính canh mất dấu người chơi

![Leash Fallback](https://cdn2.unrealengine.com/leash-fallback-1920x1080-1920x1080-e5c9c1a9e5c7.png)

## 9. Tạo Patrol Path cho tiếp viện

Tiếp viện cũng nên có đường tuần tra riêng của họ:

1. Tạo một AI Patrol Path Device mới với Patrol Path Group là 2
2. Thêm các AI Patrol Path Node Devices để tạo đường tuần tra từ vị trí tiếp viện đến pháo đài
3. Cấu hình Guard Spawner Devices cho tiếp viện để sử dụng Patrol Path Group 2

![Reinforcement Patrol Path](https://cdn2.unrealengine.com/reinforcement-patrol-path-1920x1080-1920x1080-e5c9c1a9e5c7.png)

## 10. Tạo Verse Device cho Patrol Path Manager

Để quản lý các đường tuần tra một cách linh hoạt hơn, chúng ta sẽ tạo một Verse Device mới:

1. Trong UEFN, nhấp vào tab "Verse"
2. Chọn "New File" để tạo một file Verse mới
3. Chọn "Verse Device" và đặt tên là "Stronghold_Patrol_Path_Manager"
4. Nhấp vào "Create"

## 11. Viết code cho Patrol Path Manager

Sau khi tạo Verse Device, bạn cần viết code cho nó. Double-click vào file Verse để mở editor và nhập code sau:

```verse
using { /Fortnite.com/AI }
using { /Fortnite.com/Characters }
using { /Fortnite.com/Devices }
using { /UnrealEngine.com/Temporary/SpatialMath }
using { /Verse.org/Simulation }

# Script that manages patrol paths for guards
stronghold_patrol_path_manager := class(creative_device):
    # Reference to the Game Manager to monitor perception events
    @editable
    StrongholdGameManager : stronghold_game_manager = stronghold_game_manager{}

    # Reference to the main patrol paths
    @editable
    MainPatrolPaths : []ai_patrol_path_device = array{}

    # Reference to the fallback patrol paths
    @editable
    FallbackPatrolPaths : []ai_patrol_path_device = array{}

    # Reference to the reinforcement patrol paths
    @editable
    ReinforcementPatrolPaths : []ai_patrol_path_device = array{}

    # Whether to show debug information
    @editable
    ShowDebug : logic = false

    # This function is called when the device is started in a running game
    OnBegin<override>()<suspends>:void=
        # Subscribe to events from the Game Manager
        StrongholdGameManager.GuardAlertedEvent.Subscribe(OnGuardAlerted)
        StrongholdGameManager.AllGuardsUnalertedEvent.Subscribe(OnAllGuardsUnalerted)

        # Enable main patrol paths
        for (PatrolPath : MainPatrolPaths):
            PatrolPath.Enable()

        # Disable fallback and reinforcement patrol paths initially
        for (PatrolPath : FallbackPatrolPaths):
            PatrolPath.Disable()

        for (PatrolPath : ReinforcementPatrolPaths):
            PatrolPath.Disable()

    # This function is called when a guard is alerted
    OnGuardAlerted(Agent : agent) : void =
        if (ShowDebug):
            Print("Patrol Path Manager: Guard alerted")

        # Disable main patrol paths
        for (PatrolPath : MainPatrolPaths):
            PatrolPath.Disable()

        # Enable reinforcement patrol paths
        for (PatrolPath : ReinforcementPatrolPaths):
            PatrolPath.Enable()

    # This function is called when all guards have lost track of the player
    OnAllGuardsUnalerted() : void =
        if (ShowDebug):
            Print("Patrol Path Manager: All guards unalerted")

        # Disable reinforcement patrol paths
        for (PatrolPath : ReinforcementPatrolPaths):
            PatrolPath.Disable()

        # Enable fallback patrol paths
        for (PatrolPath : FallbackPatrolPaths):
            PatrolPath.Enable()
```

Sau khi nhập code, nhấp vào "Build Verse Code" để biên dịch script.

## 12. Thêm Patrol Path Manager vào map

Sau khi biên dịch script, bạn cần thêm Patrol Path Manager vào map:

1. Trong Content Browser, điều hướng đến All/[Tên Dự Án]/CreativeDevices/
2. Tìm và chọn Stronghold_Patrol_Path_Manager
3. Kéo Stronghold_Patrol_Path_Manager vào map
4. Với Stronghold_Patrol_Path_Manager được chọn, cấu hình các tùy chọn trong panel Details:

| Option | Value | Explanation |
|--------|-------|-------------|
| Visible in Game | True | Device này sẽ hiển thị trong game |
| StrongholdGameManager | Stronghold_Game_Manager | Tham chiếu đến Stronghold Game Manager |
| MainPatrolPaths | Array elements | Thêm các AI Patrol Path Devices cho đường tuần tra chính |
| FallbackPatrolPaths | Array elements | Thêm các AI Patrol Path Devices cho đường tuần tra fallback |
| ReinforcementPatrolPaths | Array elements | Thêm các AI Patrol Path Devices cho đường tuần tra tiếp viện |
| ShowDebug | True | Hiển thị thông tin debug |

![Patrol Path Manager](https://cdn2.unrealengine.com/patrol-path-manager-1920x1080-1920x1080-e5c9c1a9e5c7.png)

## 13. Kiểm tra hệ thống tuần tra

Để kiểm tra hệ thống tuần tra, bạn nên chạy game và quan sát hành vi của lính canh:

1. Nhấp vào nút "Play" trên thanh công cụ hoặc nhấn Alt+P
2. Quan sát lính canh tuần tra theo các đường đã định
3. Kích hoạt cảnh báo bằng cách để lính canh phát hiện bạn
4. Quan sát lính canh chuyển sang hành vi tấn công
5. Trốn thoát và quan sát lính canh quay lại vị trí fallback
6. Nhấn Esc để thoát khỏi chế độ Play

![Test Patrol System](https://cdn2.unrealengine.com/test-patrol-system-1920x1080-1920x1080-e5c9c1a9e5c7.png)

## 14. Tinh chỉnh hệ thống tuần tra

Dựa trên kết quả kiểm tra, bạn có thể cần tinh chỉnh hệ thống tuần tra:

1. Điều chỉnh vị trí của các AI Patrol Path Node Devices để tạo đường tuần tra tốt hơn
2. Điều chỉnh Wait Time Min và Wait Time Max để lính canh đợi lâu hơn hoặc ngắn hơn tại các điểm
3. Điều chỉnh Patrol Path Spacing để lính canh giữ khoảng cách phù hợp
4. Điều chỉnh Leash Inner Radius và Outer Radius để lính canh có không gian di chuyển phù hợp

![Fine-tune Patrol System](https://cdn2.unrealengine.com/fine-tune-patrol-system-1920x1080-1920x1080-e5c9c1a9e5c7.png)

## 15. Lưu dự án

Sau khi hoàn thành việc thiết lập và tinh chỉnh hệ thống tuần tra, đừng quên lưu dự án của bạn:

1. Nhấp vào "File" > "Save All" hoặc nhấn Ctrl+Shift+S
2. Nhấp vào "Save"

## Tóm tắt

Trong bài học này, bạn đã học:
- Cách hiểu và sử dụng khái niệm Leash trong AI tuần tra
- Cách thêm và cấu hình AI Patrol Path Devices và AI Patrol Path Node Devices
- Cách tạo nhiều đường tuần tra cho các khu vực và tình huống khác nhau
- Cách cấu hình Guard Spawner Devices để sử dụng Patrol Paths
- Cách tạo và sử dụng Patrol Path Manager để quản lý đường tuần tra một cách linh hoạt
- Cách kiểm tra và tinh chỉnh hệ thống tuần tra

Trong bài học tiếp theo, chúng ta sẽ học cách thiết lập Audio và Visual Effects để tăng cường trải nghiệm gameplay.

## Câu hỏi suy ngẫm
1. Làm thế nào việc kết hợp Leash và Patrol Paths tạo ra hành vi tuần tra thực tế hơn cho AI?
2. Tại sao việc có các đường tuần tra khác nhau cho các tình huống khác nhau (bình thường, cảnh báo, tiếp viện) lại quan trọng trong một trò chơi stealth?
3. Làm thế nào bạn có thể sử dụng hệ thống tuần tra để tạo ra các tình huống gameplay thú vị?
4. Làm thế nào bạn có thể mở rộng hệ thống tuần tra để tạo ra các hành vi AI phức tạp hơn?
