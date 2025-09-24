---
title: "Sử dụng RHVoice trên Linux"
---

Có ba tùy chọn khả thi để cài đặt RHVoice trên Linux:

* 1. Một gói cập nhật được phân phối qua Snap Store. Dưới đây chúng tôi mô tả cách cài đặt nó.
* 2. Một trong các gói được xây dựng cho các bản phân phối Linux cụ thể. Không phải tất cả chúng đều được cập nhật và cung cấp tất cả các giọng nói. Xem [trang này](https://github.com/RHVoice/RHVoice/blob/master/doc/en/Packaging-status.md) để biết thêm thông tin.
* 3. Biên dịch từ mã nguồn: truy cập [kho mã nguồn RHVoice](https://github.com/RHVoice/RHVoice) để tìm hiểu thêm.

Việc phân phối thông qua hệ thống đóng gói Snap được các nhà phát triển công cụ RHVoice cốt lõi ưa thích, vì nó cho phép chúng tôi dễ dàng xuất bản một tệp nhị phân cập nhật duy nhất. Nếu bạn không quen thuộc với snap, vui lòng truy cập [trang web này](https://snapcraft.io/) để tìm hiểu về chúng. Bản phân phối Linux ưa thích của bạn có thể đã được cài đặt sẵn hệ thống này hoặc nó có thể có sẵn dưới dạng một gói trong kho của nó.

The snap chỉ cài đặt chính công cụ TTS RHVoice, bao gồm cả mô-đun kết nối RHVoice với Speech Dispatcher. Giọng nói cần được cài đặt thông qua trình quản lý giọng nói dòng lệnh tích hợp mới được triển khai.

Hầu hết các lệnh được mô tả dưới đây cần được chạy với quyền root. Chúng tôi sẽ giả định bạn sử dụng lệnh sudo.

Để cài đặt snap, hãy chạy lệnh này:
```
sudo snap install rhvoice
```

Bây giờ bạn cần cài đặt một giọng nói. Trình quản lý giọng nói phải được chạy với quyền root. Về lý thuyết, một số lệnh của nó không yêu cầu nó, nhưng chúng tôi chưa triển khai chức năng như vậy.

Để liệt kê các giọng nói có sẵn, hãy chạy:
```
sudo rhvoice.vm -a
```

Giả sử chúng ta muốn cài đặt giọng nói tiếng Anh có tên Alan:
```
sudo rhvoice.vm -i alan
```

Để liệt kê các giọng nói đã cài đặt, hãy chạy:
```
sudo rhvoice.vm -l
```

Bây giờ hãy kiểm tra xem nó có nói không:
```
echo hello|rhvoice.test
```

Nếu bạn sử dụng trình đọc màn hình Orca, bạn sẽ cần kết nối thủ công RHVoice với Speech Dispatcher, đây là phần mềm mà Orca dựa vào để hoạt động với các công cụ TTS. Thật không may, chúng tôi không biết bất kỳ cách nào chúng tôi có thể đăng ký RHVoice với Speech Dispatcher một cách tự động.

Phương pháp được mô tả dưới đây đã được thử nghiệm trên Ubuntu. Nếu nó không hoạt động trên bản phân phối Linux của bạn, vui lòng cho chúng tôi biết.

1. Mở terminal và thay đổi thư mục thành `/usr/lib/speech-dispatcher-modules`.
2. Tạo một liên kết tượng trưng đến mô-un của RHVoice cho Speech Dispatcher:
```
sudo ln -s /snap/rhvoice/current/bin/sd_rhvoice
```
3. Khởi động lại. Bây giờ bạn sẽ có thể chọn RHVoice và giọng nói yêu thích của mình trong Orca.