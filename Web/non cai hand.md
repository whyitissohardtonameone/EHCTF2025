Bài cho ta một đường dẫn đến trang web trắng tinh kèm src code.

Mở src lên xem index.php kkk

    <?php
    include 'flag.php';
    error_reporting(0);
    if ($_GET['debug']) {
    highlight_file(__FILE__);
    }

    $SALT = 'co_salt_thi_cung_vo_dung_thui';
    if (isset($_GET['param1']) && isset($_GET['param2']) && isset($_GET['param3']) && isset($_GET['param4']) && isset($_GET['param5'])) {
        $param1 = $_GET['param1'];
        $param2 = $_GET['param2'];
        $param3 = $_GET['param3'];
        $param4 = $_GET['param4'];
        $param5 = $_GET['param5'];
        if (!($param1 == md5($param1))) {
            die('Try harder!');
            } 
        if (!($param2 !== $param3 && hash('md5', $SALT . $param2) == hash('md5', $SALT . $param3))) {
            die('Try more harder!');
        }
        if (!(strstr($param4, 'fromehcwithlove') && strlen($param4) == 30)) {
            die('Try much more harder!');
        }
        if (!strcmp(FLAG, $param5)) {
            echo 'Here is your flag: ' . FLAG;
        } else {
            die('One more!!!!!');
        }
    }

Đọc đoạn code đầu tiên ta thấy, trang web sẽ nhận 5 tham số thông qua phương thức GET, và lần lượt nếu ta đáp ứng từng điều kiện của hàm điều kiện thì sẽ có flag.

1. Param 1. 
 - Đề yêu cầu ta tìm một tham số có giá hashing bằng chính nó. Để ý thấy đề dùng "==", ta có thể lợi dụng lỗ hổng type junggling. Đồng thời search về mã MD5 php trên gg.
   
 https://www.mo4tech.com/%e3%80%90-the-ctf-php-code-audit-%e3%80%91-md5-summarize-relevant-points.html
 - Vì php sẽ tự động ép kiểu tham số để có thể so sánh, nên ta cần tìm một chuỗi có bắt đầu bằng 0e.... vì khi đó php sẽ tự động đưa về thành 0. Ta tham khảo một chuỗi trong bài blog khớp với yêu cầu ==> 0e215962017

2. Param 2 & Param 3
  - Ở đây, đề yêu cầu ta tìm 2 chuỗi không giống nhau nhưng giá trị md5 của chúng phải bằng nhau. Ở đây ta tham khảo An array of Bypass, vì md5 hashing sẽ trả về giá trị NULL cho mảng.
  - Ta chỉ cần set cho 2 tham số param2 và param3 một mảng bất kỳ là có thể bypass

3. Param 4
  - Tham số này chỉ yêu cầu có chuỗi fromehcwithlove và độ dài là 30, ta chỉ việc thêm sau vào chuỗi ký tự bất kỳ cho đến khi độ dài đạt 30.

4. Param 5
  - Tham số này được đối chiếu với FLAG, được truyền sang từ flag.php
  - Vì flag.php là một file có thể thực thi, nên giá trị của FLAG trong đó là dynamic. Tương tự với cách làm với param2 và param3. Ta truyền vào mảng, vì khi đó strcmp sẽ báo lỗi, mà vì chương trình tắt error_reporting nên nó tự động bỏ qua.

==> ta được flag: EHCTF{juS7_An_EasY_chaLlENG3_rlGhT?_ddc7a2c5561c}

full url: http://challenge.ctf.ehc-fptu.club:25758/?param1=0e215962017&param2[]=0&param3[]=3&param4=fromehcwithlove123451234512345&param5[]=0
