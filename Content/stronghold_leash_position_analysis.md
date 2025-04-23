# Phân tích file stronghold_leash_position.verse

## Mục đích
`stronghold_leash_position` là lớp quản lý khu vực hoạt động (leash) của lính canh AI. Nó định nghĩa một khu vực mà lính canh có thể di chuyển trong đó và không thể đi ra ngoài.

## Khái niệm Leash
Trong AI, "leash" là một cơ chế giới hạn khu vực hoạt động của NPC. Nó giống như một sợi dây vô hình buộc NPC vào một vị trí cụ thể, cho phép NPC di chuyển trong một phạm vi nhất định từ vị trí đó.

## Cấu trúc lớp

### Thuộc tính chính
- **InnerRadius**: Bán kính trong của leash, khu vực mà lính canh sẽ tuần tra bình thường
- **OuterRadius**: Bán kính ngoài của leash, khu vực tối đa mà lính canh có thể di chuyển đến
- **LeashPosition**: Vị trí trung tâm của leash, thường là vị trí của device này trong thế giới game

## Các phương thức chính

### ApplyLeashOnGuard
Phương thức này áp dụng leash lên một lính canh cụ thể. Nó thiết lập khu vực hoạt động của lính canh dựa trên vị trí trung tâm và bán kính của leash.

```verse
ApplyLeashOnGuard(Guard:agent):void=
    if (GuardCharacter := character[Guard]):
        GuardCharacter.SetLeashPosition(LeashPosition)
        GuardCharacter.SetLeashInnerRadius(InnerRadius)
        GuardCharacter.SetLeashOuterRadius(OuterRadius)
```

### ApplyLeashOnGuards
Phương thức này áp dụng leash lên nhiều lính canh cùng một lúc. Nó lặp qua mảng lính canh và gọi `ApplyLeashOnGuard` cho từng lính canh.

```verse
ApplyLeashOnGuards(Guards:[]agent):void=
    for (Guard : Guards):
        ApplyLeashOnGuard(Guard)
```

## Cách hoạt động của Leash

### Inner Radius (Bán kính trong)
- Khu vực mà lính canh sẽ tuần tra bình thường
- Lính canh sẽ cố gắng ở trong khu vực này khi không có mục tiêu
- Thường nhỏ hơn Outer Radius

### Outer Radius (Bán kính ngoài)
- Khu vực tối đa mà lính canh có thể di chuyển đến
- Lính canh có thể đi ra ngoài Inner Radius nhưng không thể đi ra ngoài Outer Radius
- Khi lính canh đi ra ngoài Inner Radius, nó sẽ cố gắng quay trở lại Inner Radius sau một khoảng thời gian

## Ứng dụng trong Stronghold Template
Trong Stronghold Template, có hai loại leash chính:
1. **Stronghold Leash**: Áp dụng cho lính canh ban đầu tại pháo đài
2. **Fallback Leash**: Áp dụng cho lính canh khi họ rút lui sau khi phát hiện người chơi

Khi người chơi bị phát hiện và sau đó thoát khỏi tầm nhìn của lính canh, lính canh có thể được chuyển từ Stronghold Leash sang Fallback Leash để tạo ra hành vi rút lui.

## Tương tác với Game Manager
`stronghold_leash_position` tương tác chặt chẽ với `stronghold_game_manager`. Game Manager sẽ gọi các phương thức của Leash Position để áp dụng leash lên lính canh khi cần thiết.