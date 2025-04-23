# Bài 14: Thêm và cấu hình các devices cần thiết

## Mục tiêu
- Hiểu về các devices cần thiết cho dự án Stronghold Template
- Học cách thêm và cấu hình từng loại device
- Nắm vững cách các devices tương tác với nhau để tạo gameplay

## 1. Tổng quan về các devices cần thiết

Dự án Stronghold Template sử dụng nhiều devices khác nhau để tạo ra trải nghiệm gameplay. Dưới đây là danh sách các devices chính mà chúng ta sẽ sử dụng:

- **Player Spawner Devices** (4): Để người chơi xuất hiện trong game
- **Guard Spawner Devices** (7): Để tạo ra các lính canh AI
- **Tracker Device** (1): Để theo dõi mục tiêu và tiến trình
- **HUD Message Devices** (2): Để hiển thị thông báo cho người chơi
- **Item Granter Device** (1): Để cung cấp vũ khí và vật phẩm cho người chơi
- **End Game Devices** (3): Để kết thúc trò chơi trong các tình huống khác nhau
- **Map Indicator Device** (1): Để đánh dấu pháo đài trên bản đồ

Hãy bắt đầu thêm và cấu hình từng device.

## 2. Xây dựng pháo đài (Stronghold)

Trước khi thêm các devices, bạn cần xây dựng pháo đài - nơi các lính canh AI sẽ tuần tra và người chơi sẽ phải xâm nhập:

1. Sử dụng các props và galleries để xây dựng một pháo đài
2. Tạo các khu vực khác nhau như tháp canh, hành lang, phòng bảo vệ, v.v.
3. Đảm bảo có nhiều đường đi khác nhau để người chơi có thể lựa chọn cách tiếp cận

![Xây dựng pháo đài](https://cdn2.unrealengine.com/building-stronghold-1920x1080-1920x1080-e5c9c1a9e5c7.png)

## 3. Thêm và cấu hình Player Spawner Devices

Player Spawner Devices được sử dụng để người chơi xuất hiện trong game:

1. Trong Creative Mode, mở tab Devices và tìm "Player Spawner"
2. Đặt 4 Player Spawner Devices cách pháo đài khoảng 80 mét để tránh người chơi bị phát hiện ngay khi bắt đầu
3. Cấu hình mỗi Player Spawner như sau:

| Option | Value | Explanation |
|--------|-------|-------------|
| Visible in Game | False | Device này sẽ không hiển thị trong game |

![Player Spawner](https://cdn2.unrealengine.com/player-spawner-1920x1080-1920x1080-e5c9c1a9e5c7.png)

## 4. Thêm và cấu hình Guard Spawner Devices

Guard Spawner Devices được sử dụng để tạo ra các lính canh AI:

1. Trong Creative Mode, mở tab Devices và tìm "Guard Spawner"
2. Đặt 3 Guard Spawner Devices trong pháo đài và 4 Guard Spawner Devices bên ngoài pháo đài để làm lực lượng tiếp viện

### Cấu hình Guard Spawner cho Sniper (2 devices)

Hai trong số các Guard Spawner trong pháo đài sẽ được dùng cho lính bắn tỉa:

| Option | Value | Explanation |
|--------|-------|-------------|
| Spawn Count | 1 | Device này sẽ có một lính canh xuất hiện tại một thời điểm |
| Item List | Rail Gun | Chọn Add Element rồi chọn một súng bắn tỉa trong Item Definition |
| Allow Infinite Spawn | False | Lính canh từ device này sẽ không xuất hiện vô hạn |
| Team Index | 2 | Người chơi sẽ là Team 1, nghĩa là lính canh sẽ thù địch với người chơi khi họ phát hiện ra |
| Spawn Timer | 1.0 | Đặt thời gian tối thiểu giữa các lần xuất hiện lính canh |
| Spawn Radius | 2.5 | Đặt khoảng cách tối đa từ device mà lính canh có thể xuất hiện |
| Show Health Bar | True | Thanh máu sẽ được hiển thị phía trên lính canh |
| Max Patrol Distance | 2.5 | Đặt khoảng cách tuần tra tối đa của lính canh từ spawner |
| Visibility Range | 70.0 | Đặt khoảng cách nhận thức tầm nhìn tối đa của lính canh khi không nhận thức. Nghe không bị ảnh hưởng bởi điều này |
| Drop Inventory on Elimination | False | Lính canh sẽ không rơi kho đồ của họ khi bị tiêu diệt |
| Accuracy | VERY HIGH | Xác định mức độ chính xác của lính canh khi bắn |

![Guard Spawner Sniper](https://cdn2.unrealengine.com/guard-spawner-sniper-1920x1080-1920x1080-e5c9c1a9e5c7.png)

### Cấu hình Guard Spawner cho Assault (1 device)

Guard Spawner tiếp theo trong pháo đài sẽ được dùng cho lính tấn công:

| Option | Value | Explanation |
|--------|-------|-------------|
| Guard Type | Grotto | Đặt loại lính canh sẽ được xuất hiện bởi device này |
| Item List | Assault Rifle | Chọn Add Element rồi chọn một súng trường tấn công trong Item Definition |
| Allow Infinite Spawn | False | Lính canh sẽ không xuất hiện vô hạn từ device này |
| Team Index | 2 | Người chơi sẽ là Team 1, nghĩa là lính canh sẽ thù địch với người chơi khi họ phát hiện ra |
| Spawn Timer | 1.0 | Đặt thời gian tối thiểu giữa các lần xuất hiện lính canh |
| Spawn Radius | 18.0 | Đặt khoảng cách tối đa từ device mà lính canh có thể xuất hiện |
| Show Health Bar | True | Thanh máu sẽ được hiển thị phía trên lính canh |
| Max Patrol Distance | 18.0 | Đặt khoảng cách tuần tra tối đa của lính canh từ spawner |
| Visibility Range | 70.0 | Đặt khoảng cách nhận thức tầm nhìn tối đa của lính canh khi không nhận thức. Nghe không bị ảnh hưởng bởi điều này |
| Drop Inventory on Elimination | False | Lính canh sẽ không rơi kho đồ của họ khi bị tiêu diệt |
| Accuracy | HIGH | Xác định mức độ chính xác của lính canh khi bắn |

![Guard Spawner Assault](https://cdn2.unrealengine.com/guard-spawner-assault-1920x1080-1920x1080-e5c9c1a9e5c7.png)

### Cấu hình Guard Spawner cho Reinforcements (4 devices)

Bốn Guard Spawner cuối cùng sẽ được đặt bên ngoài pháo đài để làm lực lượng tiếp viện. Đặt các device này cách pháo đài ít nhất 40 mét.

Tiếp viện sẽ chỉ xuất hiện nếu các lính canh ban đầu tại pháo đài bị cảnh báo bởi sự hiện diện của người chơi.

| Option | Value | Explanation |
|--------|-------|-------------|
| Guard Type | Grotto | Đặt loại lính canh sẽ được xuất hiện bởi device này |
| Spawn Count | 2 | Đặt số lượng lính canh mà spawner này có thể có hoạt động tại bất kỳ thời điểm nào |
| Item List | Ranger Assault Rifle | Chọn Add Element rồi chọn một súng trường tấn công ranger trong Item Definition |
| Allow Infinite Spawn | False | Lính canh sẽ không xuất hiện vô hạn từ device này |
| Total Spawn Limit | 2 | Đặt số lượng lính canh tối đa mà spawner này có thể tạo ra trong suốt vòng đời của nó |
| Team Index | 2 | Người chơi sẽ là Team 1, nghĩa là lính canh sẽ thù địch với người chơi khi họ phát hiện ra |
| Spawn Radius | 5.0 | Đặt khoảng cách tối đa từ device mà lính canh có thể xuất hiện |
| Show Health Bar | True | Thanh máu sẽ được hiển thị phía trên lính canh |
| Max Patrol Distance | 200.0 | Đặt khoảng cách tuần tra tối đa của lính canh từ spawner |
| Visibility Range | 70.0 | Đặt khoảng cách nhận thức tầm nhìn tối đa của lính canh khi không nhận thức. Nghe không bị ảnh hưởng bởi điều này |
| Drop Inventory on Elimination | False | Lính canh sẽ không rơi kho đồ của họ khi bị tiêu diệt |
| Accuracy | HIGH | Xác định mức độ chính xác của lính canh khi bắn |

![Guard Spawner Reinforcements](https://cdn2.unrealengine.com/guard-spawner-reinforcements-1920x1080-1920x1080-e5c9c1a9e5c7.png)

## 5. Thêm và cấu hình Tracker Device

Tracker Device được sử dụng để hiển thị mục tiêu và theo dõi tổng số lính canh cần tiêu diệt, có thể thay đổi tùy thuộc vào việc tiếp viện đã xuất hiện hay chưa:

1. Trong Creative Mode, mở tab Devices và tìm "Tracker"
2. Đặt Tracker Device vào map
3. Cấu hình Tracker Device như sau:

| Option | Value | Explanation |
|--------|-------|-------------|
| Stat to Track | Events | Xác định thống kê nào sẽ được sử dụng làm Tracker Value |
| Target Value | 6 | Đặt giá trị mục tiêu mà Tracker sẽ được coi là hoàn thành |
| Assign on Game Start | False | Xác định liệu người chơi có được gán Tracker này khi trò chơi bắt đầu hay không |
| Assign When Joining in Progress | False | Xác định liệu người chơi có được gán Tracker này khi tham gia một trò chơi đang diễn ra hay không |
| Tracker Title | Eliminate Stronghold Guards | Gán tiêu đề cho Tracker sẽ được hiển thị nếu Show on HUD được bật |
| Description Text | Number of Guards | Gán mô tả cho Tracker sẽ được hiển thị bên dưới tiêu đề nếu Show on HUD được bật |
| Sharing | Team | Xác định liệu tiến trình Tracker có được tính riêng lẻ, theo đội, hay mọi người đóng góp vào một giá trị Tracker duy nhất |
| Winning Team | Team Index | Xác định đội nào thắng vòng khi Tracker hoàn thành |

![Tracker Device](https://cdn2.unrealengine.com/tracker-device-1920x1080-1920x1080-e5c9c1a9e5c7.png)

## 6. Thêm và cấu hình HUD Message Devices

HUD Message Devices hiển thị thông báo cho tất cả người chơi khi tiếp viện được kích hoạt. Thông báo này được kích hoạt thông qua Verse khi một trong các lính canh tại pháo đài bị cảnh báo:

1. Trong Creative Mode, mở tab Devices và tìm "HUD Message"
2. Đặt hai devices, một cho fallback và một cho reinforcement
3. Cấu hình các HUD Message Devices như sau:

### Fallback Message

| Option | Value | Explanation |
|--------|-------|-------------|
| Message | Guards Retreating to the Stronghold! | Chèn thông báo sẽ được hiển thị |

### Reinforcement Message

| Option | Value | Explanation |
|--------|-------|-------------|
| Message | Detected! Incoming Reinforcement! | Chèn thông báo sẽ được hiển thị |

![HUD Message](https://cdn2.unrealengine.com/hud-message-1920x1080-1920x1080-e5c9c1a9e5c7.png)

## 7. Thêm và cấu hình Item Granter Device

Item Granter Device được sử dụng để cung cấp cho người chơi một loadout với vũ khí và vật phẩm để chiến đấu với lính canh:

1. Trong Creative Mode, mở tab Devices và tìm "Item Granter"
2. Đặt Item Granter Device vào map
3. Cấu hình Item Granter Device như sau:

| Option | Value | Explanation |
|--------|-------|-------------|
| On Grant Action | Keep All | Xác định hành động thực hiện khi device cấp vật phẩm |
| Grant | All Items | Tất cả vật phẩm trong device sẽ được cấp |
| Item List | Select three weapons and a healing item | Chọn Add Element rồi chọn vật phẩm trong Item Definition |
| Index 0 | Auto Shotgun | Chọn một súng shotgun tự động trong Item Definition |
| Index 1 | Assault Rifle | Chọn một súng trường tấn công trong Item Definition |
| Index 2 | Suppressed Sniper Rifle | Chọn một súng bắn tỉa có giảm thanh trong Item Definition |
| Index 3 | Bandage | Chọn một băng trong Item Definition |

![Item Granter](https://cdn2.unrealengine.com/item-granter-1920x1080-1920x1080-e5c9c1a9e5c7.png)

## 8. Thêm và cấu hình Map Indicator Device

Map Indicator Device được sử dụng để đánh dấu pháo đài trên bản đồ của người chơi:

1. Trong Creative Mode, mở tab Devices và tìm "Map Indicator"
2. Đặt Map Indicator Device vào map
3. Cấu hình Map Indicator Device như sau:

| Option | Value | Explanation |
|--------|-------|-------------|
| Small Icon | UI Icon Enemy 64 | Chọn một biểu tượng để hiển thị |
| Large Icon | UI Icon Enemy 128 | Chọn một biểu tượng để hiển thị |
| Icon Color | Red | Chọn màu biểu tượng |

![Map Indicator](https://cdn2.unrealengine.com/map-indicator-1920x1080-1920x1080-e5c9c1a9e5c7.png)

## 9. Thêm và cấu hình End Game Devices

End Game Devices được sử dụng để kết thúc trò chơi trong các tình huống khác nhau. Chúng ta sẽ sử dụng ba End Game Devices cho việc hoàn thành pháo đài mà không bị phát hiện, hoàn thành pháo đài sau khi bị phát hiện, hoặc đơn giản là không thể tiêu diệt tất cả lính canh:

1. Trong Creative Mode, mở tab Devices và tìm "End Game"
2. Đặt ba End Game Devices vào map
3. Cấu hình các End Game Devices như sau:

### End Game - Undetected

| Option | Value | Explanation |
|--------|-------|-------------|
| Winning Team | Activating Team | Xác định đội nào sẽ thắng khi device được kích hoạt |
| Custom Victory Callout | Stronghold was cleared! [Undetected] | Đặt thông báo hiển thị khi chiến thắng hoặc kết thúc trò chơi hợp tác |
| Game End Callout | Cooperative | Đặt loại callout của màn hình kết thúc trò chơi. Cooperative hiển thị cho mọi người cùng một màn hình kết thúc sử dụng Custom Victory Callout |

### End Game - Detected

| Option | Value | Explanation |
|--------|-------|-------------|
| Winning Team | Activating Team | Xác định đội nào sẽ thắng khi device được kích hoạt |
| Custom Victory Callout | Stronghold was cleared! [Detected] | Đặt thông báo hiển thị khi chiến thắng hoặc kết thúc trò chơi hợp tác |
| Game End Callout | Cooperative | Đặt loại callout của màn hình kết thúc trò chơi. Cooperative hiển thị cho mọi người cùng một màn hình kết thúc sử dụng Custom Victory Callout |

### End Game - Fail

| Option | Value | Explanation |
|--------|-------|-------------|
| Winning Team | Activating Team | Xác định đội nào sẽ thắng khi device được kích hoạt |
| Custom Victory Callout | Game Over! Stronghold is Undefeated! | Đặt thông báo hiển thị khi chiến thắng hoặc kết thúc trò chơi hợp tác |
| Game End Callout | Cooperative | Đặt loại callout của màn hình kết thúc trò chơi. Cooperative hiển thị cho mọi người cùng một màn hình kết thúc sử dụng Custom Victory Callout |

![End Game](https://cdn2.unrealengine.com/end-game-1920x1080-1920x1080-e5c9c1a9e5c7.png)

## 10. Lưu dự án

Sau khi hoàn thành việc thêm và cấu hình tất cả các devices, đừng quên lưu dự án của bạn:

1. Nhấp vào "File" > "Save All" hoặc nhấn Ctrl+Shift+S
2. Nhấp vào "Save"

## Tóm tắt

Trong bài học này, bạn đã học:
- Cách xây dựng pháo đài cho dự án Stronghold Template
- Cách thêm và cấu hình Player Spawner Devices
- Cách thêm và cấu hình Guard Spawner Devices cho lính bắn tỉa, lính tấn công và tiếp viện
- Cách thêm và cấu hình Tracker Device để theo dõi tiến trình
- Cách thêm và cấu hình HUD Message Devices để hiển thị thông báo
- Cách thêm và cấu hình Item Granter Device để cung cấp vũ khí
- Cách thêm và cấu hình Map Indicator Device để đánh dấu pháo đài
- Cách thêm và cấu hình End Game Devices cho các tình huống khác nhau

Trong bài học tiếp theo, chúng ta sẽ học cách thêm Verse script vào devices để tạo logic gameplay phức tạp hơn.

## Câu hỏi suy ngẫm
1. Làm thế nào các thiết lập khác nhau của Guard Spawner Devices ảnh hưởng đến hành vi của lính canh?
2. Tại sao chúng ta cần ba End Game Devices khác nhau thay vì chỉ một?
3. Làm thế nào bạn có thể điều chỉnh các thiết lập để tạo ra một trải nghiệm stealth khó khăn hơn hoặc dễ dàng hơn?
4. Làm thế nào các devices khác nhau tương tác với nhau để tạo ra một trải nghiệm gameplay hoàn chỉnh?
