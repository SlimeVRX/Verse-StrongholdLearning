# Bài 13: Tạo dự án mới và thiết lập Island Settings

## Mục tiêu
- Hiểu cách tạo dự án mới trong UEFN
- Học cách thiết lập Island Settings cho dự án Stronghold Template
- Nắm vững các thiết lập cần thiết cho một trò chơi stealth với AI

## 1. Giới thiệu về Stronghold Template

Stronghold Template là một mẫu dự án trong UEFN cho phép bạn tạo một trò chơi stealth, nơi người chơi phải tiêu diệt các lính canh AI. Dự án này sử dụng nhiều tính năng của Verse như Arrays, Events, Agents và Characters để tạo ra một trải nghiệm chơi game phong phú.

Trong dự án này, người chơi có thể chọn cách chơi của mình bằng cách lẻn qua hoặc chiến đấu trực tiếp với các lính canh AI. Các lính canh AI sẽ tuần tra các khu vực được chỉ định và phản ứng khi phát hiện người chơi.

Gameplay hỗ trợ cả chơi đơn và chơi theo đội tối đa 4 người chơi.

## 2. Tạo dự án mới

Để bắt đầu, bạn cần tạo một dự án mới trong UEFN:

1. Mở UEFN và chọn "Create New" để tạo một dự án mới
2. Chọn "Empty" để bắt đầu với một dự án trống
3. Đặt tên cho dự án của bạn (ví dụ: "MyStrongholdProject")
4. Chọn vị trí lưu dự án và nhấp vào "Create"

![Tạo dự án mới](https://cdn2.unrealengine.com/create-new-project-1920x1080-1920x1080-e5c9c1a9e5c7.png)

## 3. Thiết lập Island Settings

Sau khi tạo dự án mới, bạn cần thiết lập Island Settings để cấu hình các quy tắc trò chơi. Island Settings là một device đặc biệt đã có sẵn trong mọi dự án UEFN.

### Tìm Island Settings

1. Trong Outliner (thường nằm ở bên phải màn hình), tìm và chọn "IslandSettings"
2. Trong panel Details (thường nằm ở bên phải màn hình), tìm mục "User Options - Game Rules"

![Island Settings](https://cdn2.unrealengine.com/island-settings-1920x1080-1920x1080-e5c9c1a9e5c7.png)

### Thiết lập Game Rules

Bạn cần thiết lập các Game Rules như sau:

| Option | Value | Explanation |
|--------|-------|-------------|
| Max Players | 4 | Số lượng người chơi tối đa là 4 |
| Teams | Cooperative | Đây sẽ là một trò chơi hợp tác |
| Team Size | 4 | Kích thước đội là 4 người |
| Spawn Pad Selection | Near Teammates | Người chơi sẽ xuất hiện gần nhau |
| Auto Start | False | Trò chơi sẽ đợi để bắt đầu cho đến khi được kích hoạt thủ công |
| Game Start Countdown | 3 | Trò chơi sẽ bắt đầu sau 3 giây |
| Harvest Style | Creative | Các giá trị Creative được sử dụng cho việc thu thập tài nguyên trong trò chơi |
| Allow Building | None | Người chơi sẽ không được phép xây dựng trong trò chơi |
| Environment Damage | Off | Người chơi sẽ không được phép phá hủy môi trường |
| Structure Damage | None | Người chơi sẽ không được phép phá hủy cấu trúc |
| Respawn Time | 5.0 | Người chơi sẽ hồi sinh sau 5 giây |
| Jump Fatigue | True | Nhảy liên tục sẽ áp dụng hình phạt cho độ cao nhảy |
| Glider Redeploy | True | Người chơi sẽ có thể tự do triển khai dù lượn mà không cần sử dụng vật phẩm |
| Flight Speed | 1.0x | Sẽ có hệ số nhân chuyển động là 1 khi bay |
| Game Winner Display Time | 3.0 | Tên người chiến thắng trò chơi tổng thể sẽ được hiển thị ở cuối trò chơi trong 3 giây |
| Game Score Display Time | 15.0 | Bảng điểm cuối cùng sẽ được hiển thị ở cuối trò chơi trong 15 giây |
| Round Winner Display Time | 3.0 | Tên người chiến thắng vòng sẽ được hiển thị ở cuối vòng trong 3 giây |
| Round Score Display Time | 15.0 | Bảng điểm sẽ được hiển thị ở cuối vòng trong 15 giây |
| HUD Info Type | True | Tiêu diệt kẻ thù AI sẽ được theo dõi trong HUD |
| Map Screen Display | Overview Map | Bản đồ tổng quan sẽ hiển thị khi người chơi nhấn phím Map |
| Game End Callout | Cooperative | Hiển thị cho mọi người cùng một màn hình kết thúc và sử dụng Victory Sound |
| Victory Sound | Success 1 | Xác định âm thanh phát khi người chơi chiến thắng trò chơi |

Bạn có thể sử dụng thanh tìm kiếm để tìm nhanh các thiết lập cụ thể.

![Game Rules](https://cdn2.unrealengine.com/game-rules-1920x1080-1920x1080-e5c9c1a9e5c7.png)

## 4. Thiết lập Debug Options

Để giúp việc phát triển và gỡ lỗi dễ dàng hơn, bạn nên bật một số tùy chọn debug:

1. Trong Island Settings, tìm mục "Debug"
2. Bật "Verse Debug Draw" để có thể hiển thị các hình vẽ debug từ code Verse
3. Bật "Verse Debug Log" để xem các thông báo debug từ code Verse

![Debug Options](https://cdn2.unrealengine.com/debug-options-1920x1080-1920x1080-e5c9c1a9e5c7.png)

## 5. Thiết lập Island Time

Để tạo không khí phù hợp cho trò chơi stealth, bạn có thể thiết lập thời gian trên đảo:

1. Trong Island Settings, tìm mục "Time of Day"
2. Thiết lập "Time of Day" thành "Night" hoặc "Dusk" để tạo không khí bí ẩn
3. Bạn cũng có thể điều chỉnh các thiết lập ánh sáng khác để phù hợp với trò chơi stealth

![Time of Day](https://cdn2.unrealengine.com/time-of-day-1920x1080-1920x1080-e5c9c1a9e5c7.png)

## 6. Thiết lập Island Size và Terrain

Để tạo không gian cho pháo đài và khu vực xung quanh:

1. Trong Island Settings, tìm mục "Island Size"
2. Chọn kích thước phù hợp cho dự án của bạn (ví dụ: "Medium" hoặc "Large")
3. Tùy chỉnh địa hình để tạo không gian cho pháo đài và khu vực xung quanh

![Island Size](https://cdn2.unrealengine.com/island-size-1920x1080-1920x1080-e5c9c1a9e5c7.png)

## 7. Lưu dự án

Sau khi hoàn thành các thiết lập, đừng quên lưu dự án của bạn:

1. Nhấp vào "File" > "Save All" hoặc nhấn Ctrl+Shift+S
2. Đặt tên cho map của bạn và chọn vị trí lưu
3. Nhấp vào "Save"

## 8. Kiểm tra thiết lập

Để kiểm tra xem các thiết lập của bạn đã hoạt động chính xác chưa:

1. Nhấp vào nút "Play" trên thanh công cụ hoặc nhấn Alt+P
2. Kiểm tra xem các thiết lập như số lượng người chơi tối đa, thời gian hồi sinh, v.v. có hoạt động như mong đợi không
3. Nhấn Esc để thoát khỏi chế độ Play

## Tóm tắt

Trong bài học này, bạn đã học:
- Cách tạo một dự án mới trong UEFN
- Cách tìm và thiết lập Island Settings
- Các thiết lập cần thiết cho một trò chơi stealth với AI
- Cách thiết lập debug options để giúp phát triển và gỡ lỗi
- Cách thiết lập thời gian và kích thước đảo

Trong bài học tiếp theo, chúng ta sẽ học cách thêm và cấu hình các devices cần thiết cho dự án Stronghold Template.

## Câu hỏi suy ngẫm
1. Tại sao việc thiết lập "Teams" thành "Cooperative" lại quan trọng trong một trò chơi stealth?
2. Làm thế nào các thiết lập như "Allow Building" và "Environment Damage" ảnh hưởng đến gameplay?
3. Tại sao việc bật "Verse Debug Draw" và "Verse Debug Log" lại hữu ích trong quá trình phát triển?
4. Làm thế nào bạn có thể điều chỉnh các thiết lập để tạo ra một trải nghiệm stealth khác biệt?
