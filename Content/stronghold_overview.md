# Tổng quan về Stronghold Template

## Giới thiệu
Stronghold Template là một mẫu dự án trong UEFN cho phép bạn tạo một trò chơi stealth, nơi người chơi phải tiêu diệt các lính canh AI. Dự án này sử dụng nhiều tính năng của Verse như Arrays, Events, Agents và Characters để tạo ra một trải nghiệm chơi game phong phú.

## Gameplay
- Người chơi có thể chọn cách chơi của mình bằng cách lẻn qua hoặc chiến đấu trực tiếp với các lính canh AI
- Các lính canh AI sẽ tuần tra các khu vực được chỉ định và phản ứng khi phát hiện người chơi
- Gameplay hỗ trợ chơi đơn hoặc đội gồm bốn người chơi

## Tính năng chính
1. **AI Guards**: Lính canh AI với hành vi tuần tra và phản ứng thông minh
2. **Leash System**: Hệ thống giới hạn khu vực hoạt động của AI
3. **Alert System**: Hệ thống cảnh báo khi người chơi bị phát hiện
4. **Audio & Visual Feedback**: Phản hồi âm thanh và hình ảnh để tăng trải nghiệm
5. **Verse Integration**: Sử dụng Verse để tạo logic gameplay phức tạp

## Cấu trúc dự án
Dự án Stronghold Template bao gồm các thành phần chính sau:
1. **Game Manager**: Quản lý trạng thái trò chơi tổng thể
2. **Leash Position**: Quản lý khu vực tuần tra của lính canh
3. **Alert Manager**: Quản lý âm nhạc và hiệu ứng khi lính canh phát hiện người chơi
4. **Bark Manager**: Quản lý âm thanh phát ra từ lính canh
5. **Billboard Cinematic**: Quản lý hiệu ứng hình ảnh
6. **Intro Explosion**: Quản lý hiệu ứng nổ khi bắt đầu trò chơi
7. **Log System**: Hệ thống ghi log để debug

## Tính năng Verse được sử dụng
- Arrays: Quản lý nhiều NPCs
- Events: Xử lý các sự kiện trong game
- Agents: Đại diện cho các nhân vật trong game
- Characters: Quản lý các nhân vật người chơi và AI