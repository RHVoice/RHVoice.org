---
title: "Sử dụng RHVoice trên Linux"
---

Có ba cách để cài đặt RHVoice trên Linux:

1. Sử dụng gói cài đặt mới nhất được phân phối qua Snap Store. Dưới đây là hướng dẫn chi tiết cách cài đặt.
2. Sử dụng các gói được xây dựng riêng cho từng bản phân phối Linux cụ thể. Tuy nhiên, không phải tất cả các gói này đều được cập nhật thường xuyên và cung cấp đầy đủ các giọng nói. Xem [trang này](https://github.com/RHVoice/RHVoice/blob/master/doc/en/Packaging-status.md) để biết thêm thông tin.
3. Biên dịch từ mã nguồn: Truy cập [kho lưu trữ mã nguồn RHVoice](https://github.com/RHVoice/RHVoice) để tìm hiểu thêm.

Việc phân phối qua hệ thống đóng gói Snap được các nhà phát triển công cụ RHVoice cốt lõi khuyến khích sử dụng, vì nó cho phép chúng tôi dễ dàng phát hành một tệp nhị phân duy nhất luôn được cập nhật. Nếu bạn chưa quen với Snap, vui lòng truy cập [trang web này](https://snapcraft.io/) để tìm hiểu thêm. Bản phân phối Linux bạn đang dùng có thể đã được cài đặt sẵn hệ thống này, hoặc bạn có thể cài đặt nó dưới dạng một gói từ kho lưu trữ của hệ thống.

Snap chỉ cài đặt bộ công cụ RHVoice TTS, bao gồm cả mô-đun kết nối RHVoice với Speech Dispatcher. Các giọng nói cần được cài đặt thông qua trình quản lý giọng nói bằng dòng lệnh mới được triển khai.

Hầu hết các lệnh mô tả dưới đây cần được thực hiện với quyền root. Chúng tôi giả định rằng bạn đang sử dụng lệnh sudo.

Để cài đặt snap, hãy chạy lệnh sau:
```
sudo snap install rhvoice
```

Tiếp theo, bạn cần cài đặt một giọng nói. Trình quản lý giọng nói phải được chạy với quyền root. Về lý thuyết, một số lệnh của nó không yêu cầu quyền này, nhưng chúng tôi chưa triển khai chức năng đó.

Để liệt kê các giọng nói có sẵn, hãy chạy:
```
sudo rhvoice.vm -a
```

Giả sử chúng ta muốn cài đặt giọng nói tiếng Anh có tên là Alan:
```
sudo rhvoice.vm -i alan
```

Để liệt kê các giọng nói đã cài đặt, hãy chạy:
```
sudo rhvoice.vm -l
```

Bây giờ, hãy kiểm tra xem nó có hoạt động không:
```
echo hello|rhvoice.test
```

Nếu bạn sử dụng trình đọc màn hình Orca, bạn sẽ cần kết nối RHVoice với Speech Dispatcher theo cách thủ công. Đây là phần mềm mà Orca sử dụng để làm việc với các bộ công cụ TTS. Thật không may, hiện chưa có cách nào để tự động đăng ký RHVoice với Speech Dispatcher.

Phương pháp mô tả dưới đây đã được thử nghiệm trên Ubuntu. Nếu nó không hoạt động trên bản phân phối Linux của bạn, vui lòng cho chúng tôi biết.

1. Mở terminal và chuyển đến thư mục `/usr/lib/speech-dispatcher-modules`.
2. Tạo một liên kết tượng trưng (symbolic link) đến mô-đun của RHVoice cho Speech Dispatcher:
```
sudo ln -s /snap/rhvoice/current/bin/sd_rhvoice
```
3. Khởi động lại máy. Bây giờ bạn đã có thể chọn RHVoice và giọng nói yêu thích của mình trong Orca.

