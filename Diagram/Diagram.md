app/code/
├── Packt/
    ├── HelloWorld/
    │   ├── registration.php
    │   ├── Block/
    │   │   ├── Landingspage.php
    │   │   └── Newproducts.php
    │   ├── Console/
    │   │   └── Command/
    │   ├── Controller/
    │   │   └── Index/
    │   │       ├── Index.php
    │   │       ├── Redirect.php
    │   │       ├── Subscription.php
    │   │       └── Collection.php
    │   ├── etc/
    │   │   ├── di.xml
    │   │   ├── module.xml
    │   │   └── frontend/
    │   │       ├── routes.xml
    │   │       └── page_type.xml
    │   ├── i18n/
    │   │   ├── en_US.csv
    │   │   ├── fr_FR.csv
    │   │   └── ja_JP.csv
    │   ├── Model/
    │   │   ├── Subscription.php
    │   │   └── ResourceModel/
    │   │       ├── Subscription.php
    │   │       └── Collection.php
    │   ├── Plugin/
    │   │   └── Catalog/
    │   │       └── ProductAround.php
    │   ├── Setup/
    │   │   ├── UpgradeSchema.php
    │   │   └── InstallData.php
    │   └── view/
    │       └── frontend/
    │           ├── layout/
    │           │   ├── default.xml
    │           │   └── helloworld_index_index.xml
    │           └── templates/
    │               ├── landingspage.phtml
    │               └── newproducts.phtml
    └── SEO/
        ├── registration.php
        ├── etc/
        │   └── module.xml
        └── Setup/
            ├── InstallData.php
            └── UpgradeData.php



# Cấu Trúc và Chức Năng Các Tệp Module

Tài liệu này mô tả chi tiết chức năng của từng tệp trong các module Magento 2: `MyVendor_MyModule`, `Packt_HelloWorld` và `Packt_SEO`.

## 1. MyVendor/MyModule

### 1.1. Cấu trúc thư mục: `MyVendor/MyModule`

- **`registration.php`**
  - Đăng ký module `MyVendor_MyModule` với Magento.
  - Đảm bảo hệ thống Magento nhận diện module.

- **`Block/MyCustomBlock.php`**
  - Tạo một block tùy chỉnh để hiển thị thông tin trên giao diện người dùng.
  - Chứa phương thức `getCustomMessage()` trả về một thông báo tùy chỉnh.

- **`etc/module.xml`**
  - Khai báo module `MyVendor_MyModule` và phiên bản của nó.
  - Chỉ định các module phụ thuộc (nếu có).

## 2. Packt/HelloWorld

### 2.1. Tệp cốt lõi

- **`registration.php`**
  - Đăng ký module `Packt_HelloWorld` với Magento.

- **`etc/module.xml`**
  - Khai báo module `Packt_HelloWorld` và phiên bản của nó.
  - Chỉ định phụ thuộc vào module `Magento_Catalog`.

### 2.2. Block

- **`Block/Landingspage.php`**
  - Tạo block để xử lý logic cho trang đích (landing page).
  - Bao gồm:
    - `getLandingsUrl()`: Trả về URL của trang đích.
    - `getRedirectUrl()`: Trả về URL để chuyển hướng.

- **`Block/Newproducts.php`**
  - Lấy danh sách sản phẩm mới từ cơ sở dữ liệu.
  - Sử dụng `CollectionFactory` để truy vấn sản phẩm.

### 2.3. Controller

- **`Controller/Index/Index.php`**
  - Hiển thị trang đích bằng cách trả về đối tượng `ResultPage`.

- **`Controller/Index/Redirect.php`**
  - Chuyển hướng người dùng đến một URL được chỉ định.

- **`Controller/Index/Subscription.php`**
  - Tạo bản ghi mới trong bảng `packt_helloworld_subscription`.
  - Trả về thông báo dạng raw.

- **`Controller/Index/Collection.php`**
  - Lấy danh sách sản phẩm từ cơ sở dữ liệu và cập nhật giá.

### 2.4. Model

- **`Model/Subscription.php`**
  - Đại diện cho một bản ghi trong bảng `packt_helloworld_subscription`.
  - Định nghĩa các trạng thái: `pending`, `approved`, `declined`.

- **`Model/ResourceModel/Subscription.php`**
  - Kết nối với bảng `packt_helloworld_subscription` trong cơ sở dữ liệu.

- **`Model/ResourceModel/Subscription/Collection.php`**
  - Xử lý các truy vấn liên quan đến tập hợp bản ghi trong bảng `packt_helloworld_subscription`.

### 2.5. Plugin

- **`Plugin/Catalog/ProductAround.php`**
  - Ghi đè phương thức `getName()` của sản phẩm để trả về một tên cố định.

### 2.6. Setup

- **`Setup/UpgradeSchema.php`**
  - Tạo bảng `packt_helloworld_subscription` trong cơ sở dữ liệu.
  - Định nghĩa các cột như `firstname`, `lastname`, `email`, `status`, v.v.

- **`Setup/InstallData.php`**
  - Cài đặt dữ liệu mặc định cho module (nếu cần).

### 2.7. View

- **`view/frontend/layout/default.xml`**
  - Thêm liên kết "Helloworldlanding" vào footer.

- **`view/frontend/layout/helloworld_index_index.xml`**
  - Định nghĩa layout cho trang đích.
  - Thêm block `Landingspage` và `Newproducts` vào container content.

- **`view/frontend/templates/landingspage.phtml`**
  - Hiển thị nội dung của trang đích.
  - Bao gồm các liên kết đến URL đích và URL chuyển hướng.

- **`view/frontend/templates/newproducts.phtml`**
  - Hiển thị danh sách sản phẩm mới.

### 2.8. i18n

- **`i18n/*.csv`**
  - Chứa các bản dịch cho module `Packt_HelloWorld` (ví dụ: tiếng Anh, Pháp, Nhật).

### 2.9. etc

- **`etc/di.xml`**
  - Đăng ký plugin `ProductAround` để ghi đè phương thức `getName()` của sản phẩm.
  - Đăng ký các lệnh console tùy chỉnh.

- **`etc/frontend/routes.xml`**
  - Định nghĩa route `helloworld` với frontName là `helloworld`.

- **`etc/frontend/page_type.xml`**
  - Khai báo loại trang `helloworld_index_index`.

## 3. Packt/SEO

### 3.1. Tệp cốt lõi

- **`registration.php`**
  - Đăng ký module `Packt_SEO` với Magento.

- **`etc/module.xml`**
  - Khai báo module `Packt_SEO` và phiên bản của nó.
  - Chỉ định phụ thuộc vào module `Magento_Backend`.

### 3.2. Setup

- **`Setup/InstallData.php`**
  - Cấu hình các giá manslaughter trị SEO mặc định (ví dụ: `category_canonical_tag`, `product_canonical_tag`).

- **`Setup/UpgradeData.php`**
  - Cập nhật dữ liệu liên quan đến SEO trong quá trình nâng cấp module.

---

## Lưu ý

- Đảm bảo tất cả các phụ thuộc được khai báo chính xác trong `module.xml` để tránh xung đột.
- Chạy các lệnh sau sau khi chỉnh sửa tệp module:
  ```bash
  bin/magento setup:upgrade
  bin/magento cache:clean