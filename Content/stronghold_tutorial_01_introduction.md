# Bài 1: Giới thiệu về Stronghold Template

## Tổng quan
Stronghold Template là một mẫu dự án trong UEFN cho phép tạo trò chơi stealth, nơi người chơi phải xâm nhập vào pháo đài được bảo vệ bởi AI. Dự án này sử dụng nhiều tính năng Verse như Arrays, Events, Agents và Characters.

## Đặc điểm chính
- **Hệ thống AI lính canh**: Lính canh tuần tra theo đường định sẵn và phản ứng với người chơi
- **Hệ thống phát hiện**: Lính canh có thể phát hiện người chơi qua thị giác và âm thanh
- **Hệ thống cảnh báo**: Khi phát hiện người chơi, lính canh sẽ báo động và gọi tiếp viện
- **Hệ thống âm thanh**: Lính canh phát ra "barks" (đoạn thoại ngắn) khi phản ứng với sự kiện
- **Hệ thống leash**: Giới hạn khu vực hoạt động của lính canh

## Cấu trúc dự án
Dự án bao gồm các thành phần chính:
1. **Game Manager**: Quản lý trạng thái trò chơi tổng thể
2. **Leash Position**: Quản lý khu vực tuần tra của lính canh
3. **Alert Manager**: Quản lý âm nhạc và hiệu ứng khi lính canh phát hiện người chơi
4. **Bark Manager**: Quản lý âm thanh phát ra từ lính canh
5. **Billboard Cinematic**: Quản lý hiệu ứng hình ảnh
6. **Intro Explosion**: Quản lý hiệu ứng nổ khi bắt đầu trò chơi
7. **Log System**: Hệ thống ghi log để debug

## Mục tiêu bài học
Trong loạt bài này, chúng ta sẽ tạo một phiên bản đơn giản của Stronghold Template, tập trung vào việc thiết lập AI và NPCs, theo hướng dẫn từ video của Epic Games.