Hướng dẫn mở rộng dung lượng bộ nhớ máy ảo trên ESXI
-----------

Login vào vSphere Client. </br>
Tắt VM. </br>
Chuột phải → Edit virtual machine settings </br>
Tuỳ chọn tăng giảm  Memory/CPUs/Hard disk </br>
Riêng với phần disk: </br>

Sau khi chỉnh lên con số phù hợp, cần bật VM lên vào chỉnh phân vùng và apply. </br>
![image](https://github.com/user-attachments/assets/46dd26af-92a1-4703-b25d-d7c099be37ca)

→ Start VM → SSH vào → Check hiện đã có phân vùng mới chưa, nếu chưa:  </br>
![image](https://github.com/user-attachments/assets/29623b70-80b9-45d3-8e0e-09d174c60ea5)

Run command sau:
```
fdisk -l
fdisk /dev/sda    (sda/sdb phù thuộc vào kết quả trả về từ fdisk -l)
```
chọn 'n' → 'p' → 'w'  </br>

Trong TH nó bắt chọn/tự check lại type cùng loại với ổ cứng mà VM đã sử dụng hay chưa (esxt4 tương đương với 8e - không rõ thì cứ -m để --help) </br>

Xong khởi động lại VM, và check df -Th (đã lên /dev/sda vừa tạo mới 'n' đấy hay chưa) </br>

Tiếp theo attach vào volume group và logical group (nếu chưa có phải khởi tạo, check bằng command vgdisplay và lvdisplay): </br>

```
sudo vgcreate <tên-volume-group> /dev/sdXY
 
sudo lvcreate -L <kích-thước> -n <tên-logical-volume> <tên-volume-group>
```
Tiếp theo format lại logical volume và mount:
```
sudo mkfs.ext4 /dev/<tên-volume-group>/<tên-logical-volume>
 
sudo mkdir /dev/sda5
 
sudo mount /dev/<tên-volume-group>/<tên-logical-volume> /dev/sda5
```

Restart VM và check kết quả.

<a href="https://kc.jetpatch.com/hc/en-us/articles/360058505711-How-To-Expand-Linux-VM-Partition">Tài liệu tham khảo</a>





