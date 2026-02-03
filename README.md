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

# I. Biên dịch và cài đặt U-boot 

## 1. Chuẩn bị 
<img width="889" height="310" alt="image" src="https://github.com/user-attachments/assets/864a766b-a8d7-4584-9373-8e1555c7349b" />

Clone U-boot: 
- "git clone https://github.com/u-boot/u-boot.git"

- "cd u-boot"

- "git checkout v2020.10"

## 2. Build U-boot cho Beaglebone

- "make ARCH=arm CROSS_COMPILE=arm-linux-gnueabihf- distclean"

- "make ARCH=arm CROSS_COMPILE=arm-linux-gnueabihf- am335x_evm_defconfig"

- "make ARCH=arm CROSS_COMPILE=arm-linux-gnueabihf- -j$(nproc)"

Kết quả cần có:


- "ls MLO u-boot.img"


## 3. Ghi U-boot vào SD card 

### 3.1 Chia phân vùng

<img width="684" height="60" alt="image" src="https://github.com/user-attachments/assets/28bbbc2e-5df9-4cee-b530-0663f9a8dcba" />

- Xóa hết

- Tạo 1 phân vùng FAT32

- Set bootable

<img width="605" height="72" alt="image" src="https://github.com/user-attachments/assets/ec04a095-390d-4040-b624-a3964275e2a8" />

### 3.2 Copy U-boot
<img width="699" height="177" alt="image" src="https://github.com/user-attachments/assets/999d60e1-6c86-4034-b907-b8eadc7cdfc4" />

## 4. Boot U-boot & debug UART
- Gắn SD vào BBB

- Cắm UART → PC

- Mở minicom / putty (115200)

- Kết quả thu được:

# II BIÊN DỊCH & CÀI ĐẶT KERNEL (ZImage + DTB)
## 1. Build Kernel
"cd ~/embedded-linux"

"git clone https://github.com/torvalds/linux.git" 

"cd linux"

"git checkout v5.10"

- Cấu hình cho BBB

"make ARCH=arm CROSS_COMPILE=arm-linux-gnueabihf- distclean"

"make ARCH=arm CROSS_COMPILE=arm-linux-gnueabihf- multi_v7_defconfig"

"make ARCH=arm CROSS_COMPILE=arm-linux-gnueabihf- menuconfig"

BẮT BUỘC CHECK
General Setup  --->
[*] Initial RAM filesystem and RAM disk (initramfs/initrd) support

## 2. Build kernel & dtb
"make ARCH=arm CROSS_COMPILE=arm-linux-gnueabihf- zImage -j$(nproc)"

"make ARCH=arm CROSS_COMPILE=arm-linux-gnueabihf- dtbs"

- File cần có:
"arch/arm/boot/zImage"

"arch/arm/boot/dts/am335x-boneblack.dtb"

## 3. Copy Kernel vào SD card
"sudo mount /dev/sdb1 /mnt"

"sudo cp arch/arm/boot/zImage /mnt"

"sudo cp arch/arm/boot/dts/am335x-boneblack.dtb /mnt"

"sync"

"sudo umount /mnt"

## 4. Boot kernel từ U-Boot

Trong U-Boot:

<img width="699" height="103" alt="image" src="https://github.com/user-attachments/assets/35812d0b-eb65-40b7-a880-8853c3133c07" />





