# AI và NPCs trong UEFN

## Khái niệm cơ bản

### NPC (Non-Player Character)
NPCs là các nhân vật trong game không được điều khiển bởi người chơi. Trong UEFN, NPCs có thể là:
- Lính canh (Guards)
- Động vật hoang dã (Wildlife)
- Nhân vật tùy chỉnh (Custom characters)

### AI (Artificial Intelligence)
AI là hệ thống điều khiển hành vi của NPCs, giúp chúng có thể:
- Đưa ra quyết định
- Phản ứng với môi trường
- Tương tác với người chơi

## Các loại NPC trong UEFN

### Guard NPCs
- **Mô tả**: Lính canh có khả năng tuần tra, phát hiện và tấn công người chơi
- **Hành vi**: Tuần tra, phát hiện, truy đuổi, tấn công
- **Trạng thái**: Unaware (không nhận thức), Suspicious (nghi ngờ), Alerted (cảnh giác)

### Wildlife NPCs
- **Mô tả**: Động vật hoang dã với hành vi tự nhiên
- **Hành vi**: Di chuyển tự do, phản ứng khi bị tấn công
- **Loại**: Passive (thụ động), Neutral (trung lập), Aggressive (hung hăng)

### Custom NPCs
- **Mô tả**: NPCs tùy chỉnh với hành vi được lập trình bằng Verse
- **Ứng dụng**: NPCs với logic phức tạp không có sẵn trong các loại tiêu chuẩn

## Hệ thống nhận thức của NPCs

### Sight (Thị giác)
- NPCs có thể phát hiện người chơi trong tầm nhìn
- Các yếu tố ảnh hưởng: khoảng cách, góc nhìn, vật cản

### Sound (Âm thanh)
- NPCs có thể phản ứng với âm thanh từ người chơi
- Các yếu tố ảnh hưởng: loại âm thanh, khoảng cách, vật cản

### Memory
- NPCs có thể nhớ vị trí cuối cùng của người chơi
- Thời gian nhớ có thể được cấu hình

## Các thiết bị liên quan đến AI trong UEFN

### NPC Spawner Device
- Tạo và quản lý NPCs
- Cấu hình hành vi, ngoại hình và thuộc tính của NPCs

### AI Patrol Path Device
- Định nghĩa đường đi tuần tra cho NPCs
- Tạo các điểm kiểm soát (waypoints) cho NPCs di chuyển

### Leash Device
- Giới hạn khu vực hoạt động của NPCs
- Định nghĩa khu vực trong và ngoài cho NPCs

## Lập trình AI với Verse

### Agents và Characters
- **Agent**: Đại diện cho một thực thể trong game có thể thực hiện hành động
- **Character**: Một loại Agent đặc biệt có thể di chuyển và tương tác với môi trường

### Events
- Sử dụng Events để phản ứng với các sự kiện trong game
- Ví dụ: phát hiện người chơi, nhận damage, bị tiêu diệt

### Arrays
- Quản lý nhiều NPCs cùng một lúc
- Theo dõi trạng thái của từng NPC

### Custom Behaviors
- Tạo hành vi tùy chỉnh cho NPCs bằng Verse
- Kết hợp các hành vi cơ bản để tạo ra hành vi phức tạp