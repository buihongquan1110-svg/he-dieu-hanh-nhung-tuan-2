# Bài tập Hệ Điều Hành Nhúng – Cross Compilation cho ARM
Biên dịch và cài đặt UBoot
1. Biên dịch thành công UBoot sử dụng Toolchain đã tạo (MLO + Uboot.img)
2. Tạo phân vùng Thẻ nhớ phù hợp và cài đặt Uboot thành công lên BBB (Black BeagleBone)
3. UBoot khởi tạo thành công (Sử dụng UART - Terminal để Debug)
Hiển thị phiên bản Uboot
Hiển thị thông tin phần cứng
Sử dụng các lệnh Uboot có phản hồ

Biên dịch và cài đặt Kernel
1. Biên dịch thành công Kernel cho BBB sử dụng Toolchain đồng nhất với với Uboot (ZImage + dtb file)
2. Đưa được 2 file vào thẻ nhớ
3. Truy cập Uboot, gõ lệnh khởi động được kernel thông qua lệnh bootz
Load được file ZImage và DTB vào phân vùng RAM tương ướng với địa chỉ vật lý của BBB
Gõ lệnh Load được Kernel vào BBB
4. Kernel khởi động thành công:
Hiển thị thông tin Kernel
Chờ nạp rootfs  

Link video thực hiện trên BBB: https://drive.google.com/drive/folders/17RH8gHqSrV-o-5OysdLAjEZQAFoqVZwK

## 1. Giới thiệu

Bài tập này nhằm mục đích tìm hiểu và thực hành quá trình **biên dịch chéo (cross-compilation)** cho vi xử lý ARM bằng cách:

- Sử dụng **crosstool-NG** để tạo một **Cross Toolchain** cho kiến trúc ARM.
- Viết một chương trình C đơn giản.
- Dùng toolchain vừa tạo để biên dịch chéo chương trình đó.
- Kiểm tra file thực thi bằng lệnh `file` hoặc `readelf` để xác nhận đây là file dành cho ARM.

Qua bài tập này, sinh viên hiểu được:
- Khái niệm biên dịch chéo.
- Quy trình tạo toolchain cho hệ nhúng.
- Cách kiểm tra định dạng file thực thi.


## 2. Môi trường thực hiện

- Hệ điều hành: Ubuntu 20.04 (chạy trên máy ảo VirtualBox)
- Công cụ:
  - crosstool-NG
  - gcc, make, git
- Kiến trúc target: ARM (arm-linux-gnueabi)



## 3. Tạo Cross Toolchain bằng crosstool-NG

### 3.1 Cài đặt các gói cần thiết


`sudo apt update`


`sudo apt install -y build-essential git libncurses5-dev libncursesw5-dev bison flex texinfo help2man`

### 3.2 Tạo cấu hình toolchain cho ARM

`ct-ng menuconfig` 

Trong menu cấu hình, chọn:

- Target Architecture: ARM
- Target OS: Linux
- C library: glibc (hoặc musl tùy chọn)

## 4. Biên dịch chéo chương trình C

Giả sử toochain tạo ra có tên:


`arm-linux-gnueabihf-gcc`



Tiến hành biên dịch:


`arm-linux-gnueabihf-gcc hello.c -o hello_arm`


Sau khi biên dịch thành công, thu được file thực thi:


`hello_arm`


## 5. Kết luận
Qua bài tập này, đã thực hiện thành công:

- Xây dựng cross toolchain cho kiến trúc ARM bằng Crosstool-NG.

- Viết và biên dịch chéo một chương trình C đơn giản.


Bài tập giúp hiểu rõ hơn về:

- Khái niệm biên dịch chéo

- Quy trình xây dựng toolchain

- Cách kiểm tra file nhị phân cho hệ nhúng







