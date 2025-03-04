Bài cho ta một trang log in và yêu cầu ta tìm admin, đồng thời cũng cho gợi ý là file.txt

<img src="https://github.com/user-attachments/assets/0e80ff71-5453-4a22-ac1b-4de2859123f6" width="400">

Ta tải src index.php về để check.
                
                if(!is_dir('user')){   
                    mkdir('user', 0777, true);
                    echo '<script>alert("Folder created successfully")</script>';
                }
                
                if(!file_exists('user/admin.txt')){
                    $file=fopen('user/admin.txt', 'w');
                    $password='';
                    for ($i=0; $i<=$ADMIN_PASS_LEN; $i++){
                        $password.=dechex(rand(1,255));
                    }
                    fwrite($file, $password);
                    fclose($file);
                    echo "<script>alert('Admin created')</script>";
                }

                if ($_SERVER['REQUEST_METHOD'] === 'POST') {
                    $username = $_POST["username"];
                    $password = $_POST["password"];

                    if(!file_exists("user/".$username.".txt")){
                        die("<p class='title'>User not exist</p>");
                    }

                    try{
                        $true_password=file_get_contents("user/".$username.".txt");
                    }
                    catch(Exception $e){
                        die("<p class='title'>There is something wrong: ".$e."</p>");
                    }

                    if (!isset($username)) {
                        $error = "User not found!!!";
                        die("<p class='title'>".$error."</p>");
                        exit;
                    } elseif ($password == $true_password) {
                        $_SESSION['user'] = $username; 
                        header("Location: /dashboard.php");
                        exit;
                    } else {
                        $error = "Incorrect password!!!";
                        die("<p class='title'>".$error."</p>");
                        exit;
                    }
                }
                ob_end_flush();
Thông qua đoạn code, ta thấy mỗi khi khởi tạo trang web, sever sẽ tạo ra một file có đường dẫn user/admin.txt với password là một đoạn text random trong file. 

Tiếp đến đoạn check username và password bên dưới, ta thấy sever sẽ đọc username là tên file, nghĩ là admin. Việc còn lại là đọc được password trong file, thì ta truy cập đường dẫn của file.

Flag: EHCTF{50mETlM35_EvERY7H1N9_is_ea5y_7han_YOU_7hInK_:v_065acc982221}
