Bài cho ta hint là tương tác với Header

<img src="https://github.com/user-attachments/assets/dffff1ae-6c9b-4b7d-8bf1-08dad259703b" width="400">

Ở đây, dùng đươc luôn extension ModHeader, ta lần lượt thay đổi các thông số 
  - User_Agent: đây là một chuỗi kí tự mà trình duyệt gửi đến máy chủ Web khi thực hiện yêu cầu HTTP. Cho phép máy chủ nhận diện thông tin về trình duyệt, hệ điều hành, thiết bị người dùng.... Ta sửa thành EHC_CHORME là qua step đầu.

<img src="https://github.com/user-attachments/assets/21b2d5cd-8e95-4e65-ba52-e28552d08807" width="400">

  - Host: đây là địa chỉ sever mà bạn muốn gửi đến, ở đây ta sửa theo yêu cầu là IP 127.0.0.1

<img src="https://github.com/user-attachments/assets/6418d6c7-f4c6-46a1-804c-d369746c3cd5" width="400">

  - X-Forwarded-for: đây là một HTTP header dùng để xác định địa chỉ IP client khi request qua proxy...., ta set thành IP 194.54.23.12
  - Date: Bài yêu cầu ta set thứ ngày tháng về năm 2023, ta chọn một mốc thời gian bất kỳ với format:  Thứ, ngày tháng năm 00:00:00 GMT
  - Accepted-Language: ỏe đây ta chỉnh về tiếng pháp, cú pháp là "fr".

  
EHCTF{H3adeR_iS_CRAzy_R1gH777T_262c7963c349}
