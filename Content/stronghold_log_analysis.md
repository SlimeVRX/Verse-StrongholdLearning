# Phân tích file stronghold_log.verse

## Mục đích
`stronghold_log.verse` định nghĩa một hệ thống ghi log đơn giản nhưng hiệu quả cho trải nghiệm Stronghold Template. Nó tạo ra một kênh log riêng biệt để in thông tin về tiến trình của game vào output log của UEFN, giúp cho việc debug và theo dõi hoạt động của game dễ dàng hơn.

## Cấu trúc

### stronghold_log_channel
Một lớp kênh log tùy chỉnh kế thừa từ `log_channel`. Kênh này được sử dụng để phân biệt các log của Stronghold với các log khác trong UEFN.

```verse
stronghold_log_channel := class(log_channel){}
```

### Hàm Log
Một hàm tiện ích để in thông tin vào kênh log Stronghold. Nó nhận vào một chuỗi văn bản và một mức độ log tùy chọn (mặc định là Debug).

```verse
Log<internal>(Text:string, ?Level:log_level=log_level.Debug):void=
    Logger:log = log{Channel:=stronghold_log_channel}
    Logger.Print(Text, ?Level:=Level)
```

## Cách sử dụng
Các file khác trong dự án Stronghold sử dụng hàm `Log` này để ghi lại thông tin về tiến trình của game. Ví dụ:

```verse
# Từ stronghold_billboard_cinematic.verse
Log("Cinematic Mode Engaged - Players should be frozen and invisible")

# Từ stronghold_game_manager.verse
Log("Game manager - Completed Stronghold undetected")

# Từ stronghold_intro_explosion.verse
Log("Intro Sequence - Guard Alerted")
```

## Vai trò trong AI và NPCs
Mặc dù `stronghold_log.verse` không trực tiếp quản lý AI hay NPCs, nó đóng vai trò quan trọng trong việc debug và theo dõi hành vi của AI:

### Debug hành vi AI
Hệ thống log cho phép các nhà phát triển theo dõi trạng thái và hành vi của AI trong thời gian thực. Ví dụ:
- Khi nào một lính canh phát hiện người chơi
- Khi nào một lính canh chuyển từ trạng thái tuần tra sang trạng thái cảnh giác
- Khi nào một lính canh bị tiêu diệt

### Theo dõi sự kiện AI
Hệ thống log giúp theo dõi các sự kiện liên quan đến AI, như:
- Khi nào lính canh được tạo ra
- Khi nào lính canh bắt đầu điều tra
- Khi nào tất cả lính canh trở về trạng thái không cảnh giác

### Phân tích vấn đề
Khi AI không hoạt động như mong đợi, hệ thống log giúp xác định nguyên nhân bằng cách hiển thị chuỗi sự kiện dẫn đến vấn đề.

## Lợi ích
- **Debug dễ dàng**: Giúp theo dõi luồng thực thi của game
- **Phân tích vấn đề**: Dễ dàng xác định nguyên nhân khi có lỗi xảy ra
- **Tổ chức log**: Tách biệt log của Stronghold với các log khác trong UEFN
- **Mức độ log**: Cho phép lọc log theo mức độ quan trọng (Debug, Info, Warning, Error)

## Mở rộng
Hệ thống log này có thể được mở rộng để bao gồm các tính năng bổ sung như:
- Ghi log vào file
- Hiển thị log trên màn hình trong chế độ debug
- Gửi log đến một dịch vụ từ xa để phân tích

## Thực hành tốt nhất
Khi sử dụng hệ thống log trong dự án của riêng bạn:
- Sử dụng các thông điệp log mô tả và có ý nghĩa
- Chọn mức độ log phù hợp (Debug cho thông tin chi tiết, Error cho lỗi nghiêm trọng)
- Ghi log tại các điểm quan trọng trong luồng thực thi
- Bao gồm thông tin hữu ích như ID của NPC, trạng thái hiện tại, và hành động đang thực hiện