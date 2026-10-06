## Phần 1: Phân tích tài nguyên máy tính & Mô hình IPO
1. Chẩn đoán hiện tượng lag qua Task Manager
Khi bạn mở đồng thời 20 tab Chrome và phần mềm VS Code trên một cỗ máy có cấu hình RAM 8GB và SSD 256GB, Task Manager sẽ hiển thị các dấu hiệu quá tải rõ rệt:

%RAM (Gần hoặc đạt 100%): 20 tab Chrome nổi tiếng là "kẻ ngốn RAM" vì mỗi tab chạy một tiến trình độc lập, kết hợp với môi trường lập trình VS Code khiến dung lượng 8GB bị cạn kiệt nhanh chóng.

%CPU (Tăng cao đột biến hoặc đạt ngưỡng giới hạn): Khi RAM không còn đủ chỗ chứa, CPU phải liên tục xử lý các tác vụ dọn dẹp bộ nhớ, đồng thời gánh thêm công việc điều phối dữ liệu qua lại do thiếu không gian đệm.

2. Sự khác biệt về vai trò giữa RAM và Storage trong tình huống này
RAM (Ví von như "Bàn làm việc"): Là bộ nhớ tạm thời, tốc độ cực cao, nơi CPU trực tiếp lấy dữ liệu để đọc/ghi các ứng dụng đang chạy ngay lúc đó (các tab Chrome đang mở, mã nguồn đang gõ trong VS Code). Khi "bàn làm việc" (8GB RAM) đầy ắp, bạn không còn chỗ để bày biện thêm tài liệu.

Storage / SSD (Ví von như "Ngăn tủ lưu trữ"): Là nơi lưu giữ dữ liệu lâu dài (chứa hệ điều hành, trình duyệt, mã nguồn Python).

Hiện tượng Swap File (Bộ nhớ ảo): Khi RAM đầy, hệ điều hành buộc phải dùng một phần ổ cứng SSD làm RAM tạm (swap/pagefile). Do tốc độ đọc/ghi của SSD chậm hơn RAM rất nhiều, việc máy phải liên tục "chạy ra mở ngăn tủ lấy tài liệu thay vì với tay trên bàn" gây ra hiện tượng nghẽn cổ chai, dẫn đến máy bị đứng hình (lag).

## Phần 2: Thiết kế hệ thống lưu trữ trên ổ đĩa D: (Chuẩn Kebab-case)
Để khắc phục hoàn toàn hai bẫy dữ liệu (lưu nhầm vào phân vùng hệ thống C:\Windows\System32\ và quá tải RAM/Storage), chúng ta sẽ chuyển toàn bộ mã nguồn sang ổ D:\ theo nguyên tắc phân cấp khoa học và quy chuẩn đặt tên kebab-case (các chữ viết thường ngăn cách bằng dấu gạch ngang -).

Sơ đồ Cây thư mục (File Tree) mới trên ổ D:
Plaintext
D:\
├── university-workspace\
│   ├── ptit-courses\
│   │   ├── it108-intro-to-it\
│   │   │   ├── assignments\
│   │   │   └── lectures\
│   │   └── ssk101-soft-skills\
│   └── python-projects\
│       └── first-python-project\
│           ├── src\
│           ├── tests\
│           └── README.md
├── personal-archives\
│   ├── documents\
│   └── media\
└── software-installers\
    ├── development-tools\
    └── drivers\
Giải thích cấu trúc 4 trụ cột áp dụng:
university-workspace/: Quản lý toàn bộ tài liệu và mã nguồn học tập tại trường đại học (chia nhỏ theo môn học và dự án thực hành Python đầu tay).

personal-archives/: Nơi chứa hồ sơ cá nhân, tài liệu nghiên cứu ngoài giờ và hình ảnh/video cá nhân.

software-installers/: Lưu trữ các bộ cài đặt phần mềm, công cụ lập trình và driver sạch sẽ, tránh xa phân vùng hệ thống C:\.
