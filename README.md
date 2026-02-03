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

## 1. Biên dịch và cài đặt U-boot 

Chuẩn bị 
<img width="889" height="310" alt="image" src="https://github.com/user-attachments/assets/864a766b-a8d7-4584-9373-8e1555c7349b" />

Clone U-boot
"git clone https://github.com/u-boot/u-boot.git"

"cd u-boot"

"git checkout v2020.10"

## 2. Build U-boot cho Beaglebone

"make ARCH=arm CROSS_COMPILE=arm-linux-gnueabihf- distclean"

"make ARCH=arm CROSS_COMPILE=arm-linux-gnueabihf- am335x_evm_defconfig"

"make ARCH=arm CROSS_COMPILE=arm-linux-gnueabihf- -j$(nproc)"

Kết quả cần có:
"ls MLO u-boot.img"



