Xử lý khi OpenVPN không kết nối tới được
------

# Trường hợp server VPN đều bthuong, không thay đổi gì config hoặc IP

## Step 1: Cần chú ý tới TH rule trên pfSense đang chặn connect của OpenVPN
![image](https://github.com/user-attachments/assets/b405802c-a22f-43fc-83b2-588ea0061ba3)

<a href="http://192.168.80.1/firewall_nat.php">http://192.168.80.1/firewall_nat.php</a> </br>
Do đó phải tạo lại rule này (nếu như bị xoá) </br>
Chi tiết vào FIrewall NAT: Forward Port: </br>

![image](https://github.com/user-attachments/assets/428c4abe-491b-4325-b36b-8860be640e04)

## Step 2: Attach rule này vào: 
![image](https://github.com/user-attachments/assets/40423887-245e-4bdc-9c95-f5f8ad35b1ba)
