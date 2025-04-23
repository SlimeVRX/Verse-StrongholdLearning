# Phân tích file stronghold_billboard_cinematic.verse

## Mục đích
`stronghold_billboard_cinematic` là lớp quản lý trải nghiệm điện ảnh (cinematic) trong game Stronghold Template. Nó đặt người chơi vào chế độ xem phim, ẩn họ khỏi màn hình, và hiển thị các billboard thông tin trong quá trình chiếu.

## Cấu trúc lớp

### Thuộc tính chính
- **CinematicSequenceDeviceToPlay**: Thiết bị chứa trình tự điện ảnh cần phát
- **HudController**: Thiết bị điều khiển hiển thị/ẩn HUD
- **ShowSkipIntroButton**: Cho phép hiển thị nút bỏ qua intro
- **BillboardsToShow**: Danh sách các billboard hiển thị trong quá trình chiếu
- **DevicesToHide**: Danh sách các thiết bị sẽ bị ẩn sau khi chiếu xong
- **StrongholdGameManager**: Tham chiếu đến Game Manager để bắt đầu gameplay

### Các phương thức chính

#### OnBegin
Phương thức này được gọi khi trò chơi bắt đầu. Nó thực hiện các nhiệm vụ sau:
- Đặt người chơi vào trạng thái đứng yên (frozen)
- Ẩn người chơi khỏi màn hình
- Hiển thị các billboard thông tin
- Hiển thị các thiết bị cần thiết
- Phát trình tự điện ảnh
- Tạo nút bỏ qua intro (nếu được cấu hình)

```verse
OnBegin<override>():void=
    # Freeze and hide all players
    for (Player : GetPlayspace().GetPlayers()):
        Player.FreezeMovement(true)
        Player.Hide()
    
    # Show billboards and play cinematic
    for (Billboard : BillboardsToShow):
        if (BillboardDevice := billboard_device[Billboard]):
            BillboardDevice.Show()
    
    # Hide HUD during cinematic
    HudController.HideHUD()
    
    # Play cinematic sequence
    CinematicSequenceDeviceToPlay.Play()
    
    # Create skip button if enabled
    if (ShowSkipIntroButton):
        CreateSkipButton()
    
    Log("Cinematic Mode Engaged - Players should be frozen and invisible")
```

#### HandleCinematicEnd
Phương thức này được gọi khi trình tự điện ảnh kết thúc. Nó thực hiện các nhiệm vụ sau:
- Giải phóng người chơi khỏi trạng thái đứng yên
- Hiển thị người chơi trở lại
- Ẩn các billboard thông tin
- Ẩn các thiết bị không cần thiết
- Hiển thị HUD
- Bắt đầu gameplay chính thông qua Game Manager

```verse
HandleCinematicEnd():void=
    # Unfreeze and show all players
    for (Player : GetPlayspace().GetPlayers()):
        Player.FreezeMovement(false)
        Player.Show()
    
    # Hide billboards
    for (Billboard : BillboardsToShow):
        if (BillboardDevice := billboard_device[Billboard]):
            BillboardDevice.Hide()
    
    # Hide devices
    for (Device : DevicesToHide):
        if (PropDevice := prop_device[Device]):
            PropDevice.Hide()
    
    # Show HUD
    HudController.ShowHUD()
    
    # Start gameplay
    StrongholdGameManager.StartGameplay()
    
    Log("Cinematic Mode Disengaged - Players should be unfrozen and visible")
```

#### CreateSkipButton
Phương thức này tạo nút bỏ qua intro cho người chơi, cho phép họ bỏ qua phần giới thiệu nếu muốn.

## Luồng hoạt động
1. Khi trò chơi bắt đầu, người chơi được đặt vào trạng thái đứng yên và ẩn
2. Các billboard và thiết bị được hiển thị (tùy thuộc vào cài đặt)
3. Trình tự điện ảnh được phát
4. Người chơi có thể bỏ qua intro bằng nút Skip
5. Khi trình tự kết thúc, người chơi được giải phóng và hiển thị trở lại
6. Các billboard và thiết bị được ẩn
7. Gameplay chính bắt đầu thông qua Game Manager

## Vai trò trong AI và NPCs
Mặc dù `stronghold_billboard_cinematic` không trực tiếp quản lý AI hay NPCs, nó đóng vai trò quan trọng trong việc thiết lập bối cảnh cho trò chơi trước khi AI và NPCs bắt đầu hoạt động. Nó tạo ra một trải nghiệm mở đầu mượt mà, giới thiệu người chơi vào thế giới game và chuẩn bị họ cho các tương tác sắp tới với AI.

Sau khi phần cinematic kết thúc, `stronghold_billboard_cinematic` gọi `StrongholdGameManager.StartGameplay()`, kích hoạt hệ thống AI và NPCs bắt đầu hoạt động theo kịch bản đã được lập trình.