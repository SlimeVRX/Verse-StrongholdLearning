# Thực hành tạo dự án Stronghold Template

## Giới thiệu
Stronghold Template là một mẫu dự án trong UEFN cho phép bạn tạo một trò chơi stealth, nơi người chơi phải tiêu diệt các lính canh AI. Dự án này sử dụng nhiều tính năng của Verse như Arrays, Events, Agents và Characters để tạo ra một trải nghiệm chơi game phong phú.

Trong bài thực hành này, chúng ta sẽ tạo một phiên bản đơn giản của Stronghold Template, tập trung vào việc thiết lập AI và NPCs.

## Yêu cầu
- UEFN (Unreal Editor for Fortnite) đã cài đặt
- Kiến thức cơ bản về Verse và UEFN
- Hiểu biết về các khái niệm AI và NPC trong game

## Bước 1: Tạo dự án mới

1. Mở UEFN và chọn "Create New"
2. Chọn "Blank" template
3. Đặt tên dự án là "StrongholdTemplate" và nhấp "Create"
4. Khi dự án mở, nhấp vào "Island Settings" từ thanh công cụ
5. Thiết lập các thông số cơ bản:
   - Max Players: 4
   - Respawn Time: 5 seconds
   - Starting Inventory: Empty
   - Starting Health: 100
   - Starting Shields: 0
6. Trong tab "Debug", bật "Show Debug Options" để dễ dàng debug trong quá trình phát triển

## Bước 2: Xây dựng pháo đài

1. Sử dụng các prefab và assets từ thư viện để xây dựng một pháo đài nhỏ
2. Tạo các điểm tuần tra cho lính canh bằng cách đặt các marker
3. Tạo các điểm ẩn nấp và đường di chuyển cho người chơi
4. Tạo một khu vực bên ngoài pháo đài cho vụ nổ mở đầu

## Bước 3: Thêm các devices cần thiết

### Player Spawner Device
1. Thêm Player Spawner Device vào map
2. Cấu hình để người chơi xuất hiện ở vị trí an toàn bên ngoài pháo đài
3. Thiết lập các tùy chọn như "Spawn in Air" và "Spawn with Inventory"

### Guard Spawner Devices
1. Thêm Guard Spawner Devices cho các loại lính canh khác nhau:
   - Lính bắn tỉa trên tháp canh
   - Lính tuần tra trong pháo đài
   - Lính tiếp viện xuất hiện khi có báo động
2. Cấu hình mỗi Guard Spawner với các tùy chọn phù hợp:
   - Guard Type: Sentry, Patrol, etc.
   - Weapon: Assault Rifle, Shotgun, etc.
   - Health: 100-200 tùy loại lính
   - Perception: Visual và Audio

### Item Granter Device
1. Thêm Item Granter Device để cung cấp vũ khí cho người chơi
2. Cấu hình để cung cấp các vũ khí stealth (Suppressed Pistol, Bow) và vũ khí tấn công (Assault Rifle, Shotgun)

### Tracker Device
1. Thêm Tracker Device để theo dõi tiến trình của người chơi
2. Cấu hình để đếm số lính canh đã bị tiêu diệt

### HUD Message Devices
1. Thêm HUD Message Devices để hiển thị thông báo cho người chơi
2. Tạo các thông báo cho các tình huống khác nhau:
   - "You've been detected!"
   - "Guards are searching for you"
   - "All guards eliminated"
   - "Mission failed"

### End Game Devices
1. Thêm End Game Devices cho các tình huống kết thúc game:
   - Thắng: Khi tất cả lính canh bị tiêu diệt
   - Thua: Khi tất cả người chơi bị tiêu diệt