# Bài 17: Thiết lập Audio và Visual Effects

## Mục tiêu bài học
- Hiểu cách thiết lập âm thanh (audio) cho NPCs và AI
- Học cách tạo hiệu ứng hình ảnh (visual effects) để tăng trải nghiệm người chơi
- Nắm vững cách kết hợp âm thanh và hiệu ứng hình ảnh với hành vi của AI
- Thực hành thiết lập hệ thống cảnh báo và phản hồi trực quan cho người chơi

## Nội dung bài học

### 1. Giới thiệu về Audio và Visual Effects trong UEFN

Âm thanh và hiệu ứng hình ảnh đóng vai trò quan trọng trong việc tạo ra trải nghiệm game sống động và hấp dẫn. Trong UEFN, bạn có thể sử dụng các thiết bị (devices) và Verse để tạo ra các hiệu ứng âm thanh và hình ảnh phản hồi cho hành vi của AI và tương tác của người chơi.

#### Tầm quan trọng của Audio và Visual Effects
- **Phản hồi trực quan**: Giúp người chơi hiểu được trạng thái của NPCs (phát hiện, cảnh giác, tấn công)
- **Tăng tính nhập vai**: Tạo cảm giác thực tế và sống động cho thế giới game
- **Hướng dẫn người chơi**: Sử dụng âm thanh và hiệu ứng để chỉ dẫn người chơi về các mối nguy hiểm hoặc cơ hội
- **Tạo không khí**: Thiết lập không khí và cảm xúc cho các tình huống khác nhau trong game

### 2. Thiết lập Audio cho NPCs

#### Sử dụng Audio Player Device
Audio Player Device là thiết bị chính để phát âm thanh trong UEFN. Bạn có thể sử dụng nó để tạo ra các "barks" (lời thoại ngắn) cho NPCs.

```verse
# Tham chiếu đến Audio Player Device trong Verse
@editable
BarkDevice : audio_player_device = audio_player_device{}
```

#### Tạo hệ thống Barks cho NPCs
"Barks" là thuật ngữ trong phát triển game chỉ những lời thoại ngắn mà NPCs phát ra khi phản ứng với các sự kiện như phát hiện người chơi, bị tấn công, v.v.

```verse
# Lớp đại diện cho một bark của NPC
audio_npc_bark := class<concrete>:
    # Audio device để phát barks
    @editable
    BarkDevice : audio_player_device := audio_player_device{}
    
    # Tùy chọn cho phép NPCs lặp lại bark
    @editable
    CanRepeat : logic = true
    
    # Độ trễ giữa sự kiện và thời điểm bắt đầu bark
    @editable
    Delay : float = 0.0
    
    # Độ trễ trước khi lặp lại bark này
    @editable
    Cooldown : float = 5.0
    
    # Tên bark để ghi log
    @editable
    BarkID : string = "Missing ID"
```

#### Quản lý Barks trong Verse
Bạn có thể tạo một lớp quản lý để điều khiển việc phát các barks dựa trên các sự kiện khác nhau:

```verse
# Lớp quản lý barks từ guards
stronghold_bark_manager := class(creative_device):
    # Tham chiếu đến Game Manager để theo dõi các sự kiện nhận thức
    @editable
    StrongholdGameManager : stronghold_game_manager := stronghold_game_manager{}
    
    # Audio Player Devices
    @editable
    BarkNPCDown : audio_npc_bark = audio_npc_bark{BarkID := "Man Down", Delay := 0.3}
    
    @editable
    BarkFallback : audio_npc_bark = audio_npc_bark{BarkID := "Fallback", CanRepeat := false, Delay := 3.0}
    
    @editable
    BarkNeedBackup : audio_npc_bark = audio_npc_bark{BarkID := "Need Backup", CanRepeat := false, Delay := 2.0}
    
    @editable
    BarkGoToLeash : audio_npc_bark = audio_npc_bark{BarkID := "Reinforcements En Route", CanRepeat := false, Delay := 4.0}
```

#### Cấu hình Audio Player Device
Khi thiết lập Audio Player Device, bạn cần cấu hình các tùy chọn sau:

| Tùy chọn | Giá trị | Giải thích |
|----------|---------|------------|
| Volume | 4.0 | Âm lượng của âm thanh (có thể thay đổi tùy thuộc vào bản ghi âm) |
| Restart Audio when Activated | True | Âm thanh sẽ phát từ đầu khi được kích hoạt |
| Play on Hit | False | Thiết bị sẽ không phát âm thanh khi bị người chơi tấn công |
| Play Location | Instigating Player | Âm thanh sẽ được phát dựa trên vị trí của người chơi kích hoạt thay vì vị trí của thiết bị |
| Enable Volume Attenuation | False | Không thay đổi âm lượng dựa trên khoảng cách từ thiết bị hoặc guard |

#### Sử dụng Radio Device cho nhạc nền
Radio Device có thể được sử dụng để phát nhạc nền phù hợp với trạng thái của game:

```verse
# Tham chiếu đến Radio Devices
@editable
RadioCombat : radio_device := radio_device{}

@editable
RadioAlerted : radio_device := radio_device{}
```

### 3. Thiết lập Visual Effects

#### Sử dụng Customizable Light Device
Customizable Light Device có thể được sử dụng để tạo ra các hiệu ứng ánh sáng phản ánh trạng thái của NPCs:

```verse
# Tìm tất cả đèn với tag cụ thể
FindLightsWithTag() : void =
    TaggedAlertedLightDevices := GetCreativeObjectsWithTag(alerted_lights_tag{})
    TaggedCombatLightDevices := GetCreativeObjectsWithTag(combat_lights_tag{})
    
    for (AlertedLight : TaggedAlertedLightDevices, CustomizableLight := customizable_light_device[AlertedLight]):
        CustomizableLight.TurnOff()
```

#### Cấu hình Customizable Light Device
Khi thiết lập Customizable Light Device, bạn cần cấu hình các tùy chọn sau:

| Tùy chọn | Giá trị | Giải thích |
|----------|---------|------------|
| Initial State | False | Trạng thái ban đầu của đèn khi thiết bị được kích hoạt |
| Light Size | 100.00 | Kích thước, phạm vi và biên độ của hiệu ứng ánh sáng |

#### Sử dụng VFX Creator Device
VFX Creator Device có thể được sử dụng để tạo ra các hiệu ứng hình ảnh đặc biệt như pháo hiệu khi NPCs phát hiện người chơi:

```verse
# Tham chiếu đến VFX Creator
@editable
FlareAlarmVFXCreator : vfx_creator_device := vfx_creator_device{}
```

#### Cấu hình VFX Creator Device
Khi thiết lập VFX Creator Device, bạn cần cấu hình các tùy chọn sau:

| Tùy chọn | Giá trị | Giải thích |
|----------|---------|------------|
| Start Effects When Enabled | False | Xác định liệu thiết bị có thực thi hiệu ứng khi được kích hoạt hay không |
| Sprite Size | 2.0 | Đặt kích thước ban đầu của Sprite hiệu ứng |
| Sprite Duration | 5.0 | Đặt thời gian mỗi sprite sẽ xuất hiện |
| Main Color | Red | Đặt màu chính cho hiệu ứng |
| Main Color Brightness | 200.0 | Đặt độ sáng của màu chính |

#### Sử dụng VFX Spawner Device
VFX Spawner Device có thể được sử dụng để tạo ra các hiệu ứng hình ảnh tại vị trí cụ thể, ví dụ như hiệu ứng hồi máu:

```verse
# Tham chiếu đến VFX Spawner
@editable
VFXSpawner : vfx_spawner_device = vfx_spawner_device{}

# Sử dụng VFX Spawner trong hàm hồi máu
HealCharacter(AgentToHeal : agent, Navigatable : navigatable, Focusable : focus_interface)<suspends> : void =
    # Chỉ hồi máu cho character nếu họ ở trong HealVolume
    if:
        HealVolume.IsInVolume[AgentToHeal]
        CharacterToHeal := AgentToHeal.GetFortCharacter[]
    then:
        Print("Character is in volume, starting healing")
        NavigationTarget := MakeNavigationTarget(AgentToHeal)
        branch:
            Navigatable.NavigateTo(NavigationTarget)
            Focusable.MaintainFocus(AgentToHeal)
        VFXSpawner.Enable()
        defer:
            VFXSpawner.Disable()
```

### 4. Kết hợp Audio và Visual Effects với hành vi AI

#### Tạo hệ thống cảnh báo
Bạn có thể tạo một hệ thống cảnh báo kết hợp âm thanh và hiệu ứng hình ảnh để phản ánh trạng thái của NPCs:

```verse
# Lớp quản lý cảnh báo
stronghold_alert_manager := class(creative_device):
    # Tham chiếu đến Game Manager để theo dõi các sự kiện nhận thức
    @editable
    StrongholdGameManager : stronghold_game_manager := stronghold_game_manager{}
    
    # Tham chiếu đến Radio phát nhạc chiến đấu
    @editable
    RadioCombat : radio_device := radio_device{}
    
    # Tham chiếu đến Radio phát nhạc cảnh giác
    @editable
    RadioAlerted : radio_device := radio_device{}
    
    # VFX để phát khi báo động/pháo hiệu được bắn
    @editable
    FlareAlarmVFXCreator : vfx_creator_device := vfx_creator_device{}
    
    # Dữ liệu lớp
    var<private> CustomizableLightDevicesAlerted : []customizable_light_device = array{}
    var<private> CustomizableLightDevicesCombat : []customizable_light_device = array{}
    
    # Thay đổi trại sang trạng thái cảnh giác khi người chơi bị mất dấu / bị giết
    WaitForAlerted()<suspends> : void =
        # không quay lại cảnh giác sau khi rút lui
        if (StrongholdGameManager.FallbackTriggered?):
            Sleep(Inf)
        StrongholdGameManager.GuardsUnawareEvent.Await()
        Sleep(3.0)
        SetAlertedMood()
    
    # Thay đổi trại sang trạng thái chiến đấu khi người chơi bị phát hiện
    WaitForCombat()<suspends> : void =
        race:
            StrongholdGameManager.PlayerDetectedEvent.Await()
            StrongholdGameManager.FallbackEvent.Await()
        Sleep(2.0)
        SetCombatMood()
```

#### Thiết lập trạng thái chiến đấu
```verse
# Thiết lập Base sang Combat bằng cách bật đèn đỏ và phát nhạc cường độ cao
SetCombatMood() : void =
    # Lặp qua Combat Lights và bật chúng
    for (LightsToTurnOn : CustomizableLightDevicesCombat):
        LightsToTurnOn.TurnOn()
    
    # Lặp qua Alert Lights và tắt chúng
    for (LightsToTurnOff : CustomizableLightDevicesAlerted):
        LightsToTurnOff.TurnOff()
    
    # Bật âm thanh chiến đấu và tắt âm thanh cảnh giác
    RadioCombat.Play()
    RadioAlerted.Stop()
    FlareAlarmVFXCreator.Toggle()
```

#### Thiết lập trạng thái cảnh giác
```verse
# Thiết lập Base sang Alerted bằng cách bật đèn vàng và phát nhạc căng thẳng
SetAlertedMood() : void =
    for (LightsToTurnOn : CustomizableLightDevicesAlerted):
        LightsToTurnOn.TurnOn()
    
    for (LightsToTurnOff : CustomizableLightDevicesCombat):
        LightsToTurnOff.TurnOff()
    
    RadioCombat.Stop()
    RadioAlerted.Play()
```

### 5. Ứng dụng thực tế: Tạo NPC Medic với hiệu ứng hồi máu

#### Thiết lập NPC Medic
```verse
# Một NPC Behavior được tạo bằng Verse có thể được sử dụng trong NPC Definition hoặc Character Spawner device's Behavior Script Override.
medic_example<public> := class(npc_behavior):
    # Ngưỡng HP mà một character phải đạt được trước khi hồi máu cho họ.
    @editable
    HealingThreshold : float = 50.0
 
    # Thời gian chờ trước khi hồi máu cho characters
    @editable
    HealingDelay : float = 1.5
 
    # Lượng máu hồi cho characters mỗi lần hồi máu
    @editable
    HealingAmount : float = 5.0
 
    # Volume mà characters vào để nhận hồi máu.
    @editable
    HealVolume : mutator_zone_device = mutator_zone_device{}
 
    # VFX spawner để phát VFX khi characters đang được hồi máu.
    @editable
    VFXSpawner : vfx_spawner_device = vfx_spawner_device{}
```

#### Hàm hồi máu với hiệu ứng
```verse
# Hồi máu cho character, sau đó chờ một khoảng thời gian HealingDelayAmount.
# Kết thúc khi máu của character đạt đến HealingThreshold
# hoặc character rời khỏi HealVolume.
HealCharacter(AgentToHeal : agent, Navigatable : navigatable, Focusable : focus_interface)<suspends> : void =
    # Chỉ hồi máu cho character nếu họ ở trong HealVolume
    if:
        HealVolume.IsInVolume[AgentToHeal]
        CharacterToHeal := AgentToHeal.GetFortCharacter[]
    then:
        PrintNPCB("Character is in volume, starting healing")
        NavigationTarget := MakeNavigationTarget(AgentToHeal)
        branch:
            Navigatable.NavigateTo(NavigationTarget)
            Focusable.MaintainFocus(AgentToHeal)
        VFXSpawner.Enable()
        defer:
            VFXSpawner.Disable()
        race:
            loop:
                CurrentHealth := CharacterToHeal.GetHealth()
                if (CurrentHealth + HealingAmount > HealingThreshold):
                    if (CurrentHealth < HealingThreshold):
                        CharacterToHeal.SetHealth(HealingThreshold)
                    PrintNPCB("Character has reached HealingThreshold, stopping healing")
                    break
                else:
                    CharacterToHeal.SetHealth(CurrentHealth + HealingAmount)
                Sleep(HealingDelay)
```

#### Xử lý khi agent vào vùng hồi máu
```verse
# Khi một agent vào HealVolume, thêm họ vào
# hàng đợi AgentsToHeal nếu họ không phải là NPC Character.
OnAgentEnters(EnteredAgent : agent) : void =
    PrintNPCB("Agent entered the heal volume")
    if (EnteredAgent <> GetAgent[]):
        set AgentsToHeal = AgentsToHeal.Enqueue(EnteredAgent)

# Khi một agent rời khỏi HealVolume, PrintNPCB vào log
OnAgentExits(ExitAgent : agent) : void =
    PrintNPCB("Agent exited the heal volume")
```

## Tóm tắt

- **Audio Player Device** được sử dụng để phát âm thanh cho NPCs, bao gồm các "barks" khi NPCs phản ứng với các sự kiện.
- **Radio Device** được sử dụng để phát nhạc nền phù hợp với trạng thái của game.
- **Customizable Light Device** được sử dụng để tạo ra các hiệu ứng ánh sáng phản ánh trạng thái của NPCs.
- **VFX Creator Device** được sử dụng để tạo ra các hiệu ứng hình ảnh đặc biệt như pháo hiệu.
- **VFX Spawner Device** được sử dụng để tạo ra các hiệu ứng hình ảnh tại vị trí cụ thể.
- Kết hợp âm thanh và hiệu ứng hình ảnh với hành vi AI tạo ra trải nghiệm game sống động và hấp dẫn.

## Câu hỏi biện luận
1. Làm thế nào để thiết kế một hệ thống âm thanh và hiệu ứng hình ảnh hiệu quả mà không gây ra quá tải thông tin cho người chơi?
2. So sánh ưu và nhược điểm của việc sử dụng âm thanh so với hiệu ứng hình ảnh để truyền đạt thông tin về trạng thái của NPCs.
3. Làm thế nào để sử dụng âm thanh và hiệu ứng hình ảnh để tạo ra các tình huống căng thẳng hoặc bất ngờ trong game?

## Bài tập thực hành
1. Tạo một hệ thống barks đơn giản cho NPCs phản ứng với các sự kiện khác nhau (phát hiện người chơi, bị tấn công, v.v.).
2. Thiết kế một hệ thống cảnh báo sử dụng đèn và âm thanh để phản ánh trạng thái của NPCs.
3. Tạo một NPC Medic với hiệu ứng hồi máu sử dụng VFX Spawner Device.
