# Phân tích file stronghold_bark_manager.verse

## Mục đích
`stronghold_bark_manager` là lớp quản lý các "barks" (âm thanh thoại ngắn) từ lính canh AI. Nó giúp tạo phản hồi âm thanh khi lính canh phản ứng với các sự kiện trong game, làm tăng tính chân thực và cung cấp thông tin cho người chơi.

## Khái niệm Bark
Trong game design, "bark" là thuật ngữ chỉ các đoạn thoại ngắn mà NPC phát ra để phản ứng với môi trường hoặc sự kiện. Ví dụ: "Man down!" khi một đồng đội bị hạ gục, hoặc "Need backup!" khi phát hiện kẻ thù.

## Cấu trúc lớp

### Thuộc tính chính
- **StrongholdGameManager**: Tham chiếu đến Game Manager để theo dõi các sự kiện
- **Các Audio NPC Bark Devices**:
  - **BarkNPCDown**: "Man Down" - Phát khi một lính canh bị tiêu diệt
  - **BarkFallback**: "Fallback" - Phát khi lính canh rút lui
  - **BarkNeedBackup**: "Need Backup" - Phát khi lính canh cần tiếp viện
  - **BarkGoToLeash**: "Reinforcements En Route" - Phát khi tiếp viện đang trên đường đến

### Cấu trúc audio_npc_bark
Mỗi bark được định nghĩa với các thuộc tính:
- **BarkID**: ID của bark, dùng để xác định bark cụ thể
- **Delay**: Thời gian trễ trước khi phát bark
- **CanRepeat**: Có thể lặp lại bark hay không

```verse
BarkNPCDown:audio_npc_bark = audio_npc_bark{BarkID := "Man Down", Delay := 0.3}
BarkFallback:audio_npc_bark = audio_npc_bark{BarkID := "Fallback", CanRepeat := false, Delay := 3.0}
```

## Các phương thức chính

### OnBegin
Phương thức này được gọi khi trò chơi bắt đầu. Nó thiết lập các sự kiện lắng nghe từ Game Manager để phát các bark tương ứng.

### OnGuardEliminated
Được gọi khi một lính canh bị tiêu diệt. Nó phát bark "Man Down" để thông báo cho các lính canh khác.

### OnPlayerDetected
Được gọi khi người chơi bị phát hiện. Nó phát bark "Need Backup" để yêu cầu tiếp viện.

### OnReinforcementsSpawned
Được gọi khi tiếp viện được tạo ra. Nó phát bark "Reinforcements En Route" để thông báo rằng tiếp viện đang trên đường đến.

### OnAllGuardsUnalerted
Được gọi khi tất cả lính canh trở về trạng thái không cảnh giác. Nó phát bark "Fallback" để thông báo rằng tình huống đã an toàn.

## Cách hoạt động của Bark Manager

1. Khi trò chơi bắt đầu, Bark Manager đăng ký lắng nghe các sự kiện từ Game Manager
2. Khi một sự kiện xảy ra (ví dụ: lính canh bị tiêu diệt), Game Manager kích hoạt sự kiện tương ứng
3. Bark Manager nhận sự kiện và phát bark phù hợp
4. Audio Player Device phát âm thanh tương ứng trong game

## Tầm quan trọng của Barks trong gameplay
- **Thông tin**: Cung cấp thông tin về trạng thái game cho người chơi
- **Không khí**: Tạo không khí căng thẳng và chân thực
- **Phản hồi**: Cung cấp phản hồi về hành động của người chơi
- **Chiến thuật**: Giúp người chơi hiểu được trạng thái của lính canh và điều chỉnh chiến thuật

## Tương tác với các thành phần khác
- Nhận sự kiện từ `stronghold_game_manager` để biết khi nào phát bark
- Sử dụng Audio Player Devices để phát âm thanh trong game