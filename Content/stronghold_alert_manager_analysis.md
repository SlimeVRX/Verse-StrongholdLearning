# Phân tích file stronghold_alert_manager.verse

## Mục đích
`stronghold_alert_manager` là lớp quản lý trạng thái cảnh báo trong game, bao gồm âm nhạc và hiệu ứng ánh sáng. Nó phản ứng với các sự kiện từ Game Manager để thay đổi không khí của game dựa trên trạng thái cảnh giác của lính canh.

## Cấu trúc lớp

### Tags
- **alerted_lights_tag**: Tag cho đèn cảnh báo khi lính canh ở trạng thái cảnh giác
- **combat_lights_tag**: Tag cho đèn cảnh báo khi lính canh ở trạng thái chiến đấu

### Thuộc tính chính
- **StrongholdGameManager**: Tham chiếu đến Game Manager để theo dõi các sự kiện
- **RadioCombat**: Radio Device phát nhạc khi lính canh ở trạng thái chiến đấu
- **RadioAlerted**: Radio Device phát nhạc khi lính canh ở trạng thái cảnh giác

## Các phương thức chính

### OnBegin
Phương thức này được gọi khi trò chơi bắt đầu. Nó thiết lập các sự kiện lắng nghe từ Game Manager và tìm tất cả các đèn có tag tương ứng.

```verse
OnBegin<override>():void=
    # Find all lights with the alerted and combat tags
    AlertedLights := GetCreativeObjectsWithTag(alerted_lights_tag{})
    CombatLights := GetCreativeObjectsWithTag(combat_lights_tag{})
    
    # Listen for player detected and unalerted events
    StrongholdGameManager.PlayerDetectedEvent.Subscribe(OnPlayerDetected)
    StrongholdGameManager.AllGuardsUnalertedEvent.Subscribe(OnAllGuardsUnalerted)
```

### OnPlayerDetected
Được gọi khi người chơi bị phát hiện. Nó bật đèn cảnh báo và phát nhạc cảnh giác.

```verse
OnPlayerDetected():void=
    # Turn on alerted lights and music
    for (Light : AlertedLights):
        if (AlertedLight := customizable_light_device[Light]):
            AlertedLight.TurnOn()
    
    RadioAlerted.Play()
    RadioCombat.Stop()
```

### OnAllGuardsUnalerted
Được gọi khi tất cả lính canh trở về trạng thái không cảnh giác. Nó tắt đèn cảnh báo và dừng nhạc cảnh giác.

```verse
OnAllGuardsUnalerted():void=
    # Turn off all lights and music
    for (Light : AlertedLights):
        if (AlertedLight := customizable_light_device[Light]):
            AlertedLight.TurnOff()
    
    for (Light : CombatLights):
        if (CombatLight := customizable_light_device[Light]):
            CombatLight.TurnOff()
    
    RadioAlerted.Stop()
    RadioCombat.Stop()
```

### OnGuardCombat
Được gọi khi lính canh bắt đầu chiến đấu. Nó bật đèn chiến đấu và phát nhạc chiến đấu.

```verse
OnGuardCombat():void=
    # Turn on combat lights and music
    for (Light : CombatLights):
        if (CombatLight := customizable_light_device[Light]):
            CombatLight.TurnOn()
    
    RadioCombat.Play()
    RadioAlerted.Stop()
```

## Cách hoạt động của Alert Manager

### Trạng thái cảnh báo
Alert Manager quản lý ba trạng thái chính:
1. **Normal**: Không có cảnh báo, đèn tắt, không có nhạc
2. **Alerted**: Lính canh cảnh giác, đèn cảnh báo bật, nhạc cảnh giác phát
3. **Combat**: Lính canh chiến đấu, đèn chiến đấu bật, nhạc chiến đấu phát

### Luồng hoạt động
1. Khi trò chơi bắt đầu, Alert Manager ở trạng thái Normal
2. Khi người chơi bị phát hiện, Alert Manager chuyển sang trạng thái Alerted
3. Khi lính canh bắt đầu chiến đấu, Alert Manager chuyển sang trạng thái Combat
4. Khi tất cả lính canh trở về trạng thái không cảnh giác, Alert Manager chuyển về trạng thái Normal

## Tầm quan trọng của Alert Manager
- **Phản hồi trực quan**: Cung cấp phản hồi trực quan về trạng thái game
- **Không khí**: Tạo không khí căng thẳng khi người chơi bị phát hiện
- **Thông tin**: Giúp người chơi biết khi nào họ đã thoát khỏi sự phát hiện

## Tương tác với các thành phần khác
- Nhận sự kiện từ `stronghold_game_manager` để biết khi nào thay đổi trạng thái
- Điều khiển Radio Devices để phát nhạc
- Điều khiển Customizable Light Devices để bật/tắt đèn