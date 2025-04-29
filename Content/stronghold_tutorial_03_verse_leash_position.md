# Bài 3: Thiết lập Stronghold Leash Position

## Giới thiệu về Leash Position
Trong Stronghold Template, Leash Position là một thành phần quan trọng giúp quản lý khu vực hoạt động của lính canh AI. Nó định nghĩa một khu vực mà lính canh có thể di chuyển trong đó và không thể đi ra ngoài, giống như một sợi dây vô hình buộc NPC vào một vị trí cụ thể.

## Tạo file Verse cho Leash Position
1. Mở Verse Explorer từ menu "Verse" hoặc "Tools > Verse Explorer"
2. Nhấp chuột phải vào tên dự án trong Verse Explorer
3. Chọn "Add new verse file to project"
4. Đặt tên file là "stronghold_leash_position" và chọn "Create empty"

## Thêm mã Verse cho Leash Position
1. Mở file Verse vừa tạo bằng cách nhấp đúp vào nó
2. Thêm các namespace cần thiết:
   ```verse
   using { /Fortnite.com/Devices }
   using { /Verse.org/Simulation }
   using { /UnrealEngine.com/Temporary/Diagnostics }
   ```
3. Tạo lớp stronghold_leash_position:
   ```verse
   stronghold_leash_position := class(creative_device):
       # Thuộc tính
       @editable var LeashRadius : float = 10.0
       @editable var FallbackRadius : float = 5.0
       @editable var IsFallbackPosition : logic = false
       
       # Phương thức
       GetLeashRadius() : float = LeashRadius
       GetFallbackRadius() : float = FallbackRadius
       IsFallback() : logic = IsFallbackPosition
   ```
4. Lưu file và quay lại UEFN

## Biên dịch mã Verse
1. Trong UEFN, nhấp vào menu "Verse"
2. Chọn "Build Verse Code" hoặc nhấn F8
3. Đợi quá trình biên dịch hoàn tất

## Thêm Leash Position Devices vào map
1. Mở Content Browser và tìm "Stronghold Leash Position" trong Creative Devices
2. Kéo thiết bị vào map tại vị trí bạn muốn đặt trung tâm khu vực tuần tra
3. Trong Details panel, thiết lập các thông số:
   - Leash Radius: 10.0 (hoặc giá trị phù hợp với kích thước khu vực)
   - Fallback Radius: 5.0
   - Is Fallback Position: False
   - Visible In Game: False (để thiết bị không hiển thị trong game)

## Tạo Fallback Position
1. Nhân bản Leash Position bằng cách giữ Alt và kéo
2. Đặt thiết bị mới ở vị trí an toàn trong pháo đài
3. Trong Details panel, thiết lập:
   - Is Fallback Position: True
   - Các thông số khác tùy chỉnh phù hợp

## Vai trò của Leash Position trong hệ thống AI
- **Giới hạn khu vực**: Giúp lính canh không đi quá xa khỏi vị trí được giao
- **Vị trí rút lui**: Khi bị tấn công, lính canh có thể rút về vị trí Fallback an toàn
- **Tối ưu hóa**: Giúp tối ưu hóa hiệu suất bằng cách giới hạn phạm vi hoạt động của AI