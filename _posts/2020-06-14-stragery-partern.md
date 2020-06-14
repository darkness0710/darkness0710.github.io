# Strategy pattern và câu chuyện cuộc đời lập trình viên Núi?
## Giới thiệu về nhân vật Núi 
- Núi một cậu sinh viên học đại học bách khoa, một người vui vẻ hoà đồng, có ước mơ trở thành một lập trình viên vĩ đại như **Mark Zuckerberg** và đặc biệt là nhiệt tình dù không thông minh. (Hay nói cách khác nhiệt tình + ngu dốt = ... phá hoại)
- Không thông minh như bạn bè cùng trang lứa, nhưng với châm ngôn "cần cù thì bù thông minh", ngày ngày "dậy sớm hơn gà, ngủ muộn hơn chó" cuối cùng sau bao cố gắng núi cũng tốt nghiệp đại học và theo đuổi ước mơ của mình.
- Núi thử phỏng vấn thực tập ở nhiều công ty nhưng đều thất bại, có lẽ là vì cố gắng học tập quá nhiều nên gương mặt của cậu sinh viên ngày nào giờ trông giống một ông chú 40t nên đi phỏng vấn cho thực tập toàn bị tạch. 
- Buồn, chán nản, stress trong một  và vì cuộc sống mưu sinh núi chuyển qua chạy grab, và rồi cậu gặp một người. Người đó là một
- Núi thử phỏng vấn thực tập ở nhiều công ty nhưng đều thất bại, có lẽ là vì cố gắng học tập quá nhiều nên gương mặt của cậu sinh viên ngày nào giờ trông giống một ông chú 40t nên đi phỏng vấn cho thực tập toàn bị tạch. 
- Buồn, chán nản, stress trong một khoảng thời gian dài và vì cuộc sống mưu sinh núi chuyển qua chạy grab, và rồi cậu gặp một người. Người đó là một
giám đốc của 1 start up về IT tên là Q. Với nghị lực, ý chí của tuổi trẻ, Núi đã thuyết phục được anh Q và được nhận thực tập vào công ty **the heaven**. Giống như gặp được định mệnh của đời mình, cuộc đời của núi bước sang một trang mới!
## Dự án FileDB
- Mặc dù chỉ là một thực tập sinh, nhưng núi đã chứng minh năng lực cũng như những phẩm chất của 1 cậu sinh viên "tuổi trẻ chưa trải sự đời".
- Một thời gian sau đó, núi được giao thực hiện 1 dự án vô cùng quan trọng của công ty đó là dự án "FileDB", dự án cho phép người sử dụng upload file lên các dịch vụ lưu trữ như như GoogleDrive, Azure, AmazonS3, ... và tiến hành gửi email cho user và admin.
- Với kinh nghiệm nhiều năm thi lại môn phân tích thiết kế hệ thống và hiểu biết về OOP, cùng với sologan học từ người bạn "H đẹp trai dân chơi đất cảng":
 > "Một ngày nào đó code cũng trờ về với cát bụi vậy chúng ta cố gắng viết code sạch để làm gì?" 

Núi đã tiến hành phân tích, thiết kế hệ thống và thấy rằng chỉ tận tạo một class BaseService rồi sử dụng kế thừa thì coi như là xong, quá là ez luôn:

```
<?php

class BaseService
{
    public function sendFile($file)
    {
    
    }

    public function sendMail()
    {
        echo '[logic send mail for user and admin]';
    }
}

class AmazonS3 extends BaseService
{
    public function sendFile($file)
    {
        echo '[logic send file api s3]' . $file;
    }
}

class Azure extends BaseService
{
    public function sendFile($file)
    {
        echo '[logic send file api azure]' . $file;
    }
}

class GoogleDriver extends BaseService
{
    public function sendFile($file)
    {
        echo '[logic send file api google driver]' . $file . "\r";
    }
}

$googleDrive = new GoogleDriver();
$googleDrive->sendFile('jav.png'); // [logic send file api google driver]jav.png
$googleDrive->sendMail(); // [logic send mail for user and admin]

```

* Núi thấy rằng dự án thật là đơn giản, chưa thể sánh được với năng lực của bản thân, dự án này còn dễ hơn bài tập lớn trên trường, từ đó núi không còn chăm chỉ học tập nữa. 
* Ngày ngày tới công ty đọc báo, sống ảo trên facebook và bán hàng online ...
Thời gian như chó chạy ngoài đồng, một thời gian sau trong một cuộc họp, giám đốc Q muốn dự án này có một bước đột phá vì có sự cạnh tranh khốc liệt tới từ các công ty IT khác, và yêu cầu Núi trong vòng 1 tuần thêm vào dự án các tính năng:
  * Một số nền tảng chỉ cần gửi email cho người dùng.
  * Một số nền tảng chỉ cần gửi email cho admin.
  * Một số nền tảng có thể tuỳ chọn gửi mail cho người dùng hoặc admin hoặc cả hai.

* Ngay tập tức, núi vắt tay lên chán và suy nghĩ và cách giải quyết:
  * Núi nghĩ ngay tới việc override lên các hàm sendMail() ở các class kế thừa và khi nhìn lại dự án thì ... dự án đã phát triển
có tới hàng trăm class được thêm vào và kế thừa lớp BaseService. Nếu như sửa tất cả, cộng thêm thời gian test lại nữa thì 1 tuần là không thể nào và sau này nếu
phát sinh thêm các sửa đổi khác thì làm thế nào? 
  * Giờ núi mới nhận ra câu nói:
  > "Thứ duy nhất không thay đổi trong việc phát triển phần mềm là “sự thay đổi”" ... sự thay đổi có thể tới bất cứ lúc nào ...

## Lựa chọn của núi
* Lựa chọn 1:
  * Núi quyết định override lên hàm sendMail() và implement một loạt các logic khác để đáp ứng lại sự thay đổi của hệ thống. Một thời gian sau, để chạy theo sự thay đổi của người dùng, hệ thống FileDb ngày càng trì trệ, bug bắt đầu xuất hiện, và mọi thứ như nằm ngoài tầm kiểm soát của Núi... Và cuối cùng khi không thể đáp ứng được sự thay đổi nữa, công ty the heaven phá sản, núi thất nghiệp, và trên fb núi để lại 1 dòng tinh nhắn:
"Còn gì nữa đâu mà khóc với sầu ..."
* Lựa chọn 2:
  * Núi thấy dự án giờ giống như một con tàu đắm, núi gặp a Q và quyết định xin nghỉ việc. Ngay lập tức a Q tuyển dung dev mới để khoả lấp khoảng trống, và dev mới khi thấy đống hỗn độn trong đống code của núi để lại và thời gian lại quá ngắn. Công ty the heaven vẫn không tránh khỏi kết cục phá sản, và trên fb của a Q chỉ để lại 1 dòng tin nhắn:
"Sai lầm lớn nhất a mang trong cuộc đời là tuyển thằng núi ..."
* Lựa chọn 3:
  * Núi sử dụng quyền trợ giúp gọi điện thoại người thân, núi ngay lập gọi cho "H đẹp trai" một dân chơi đất cảng. Vừa khóc lóc, vừa kể lể, cuối cùng người bạn của núi trả lời rằng "Ngu thì chết khóc lóc cái ..." à đương nhiên là không phải thế rồi =)) Người bạn đó gửi cho Núi một cuốn sách "Head First Design Pattern" và khuyên núi nên đọc cuốn đó , và núi đã thức 3 ngày 3 đêm không ăn không ngủ để tìm hiểu cuốn sách đó. Trời không phụ lòng người núi đã tìm thấy một giải pháp cho phần thiết kế hệ thống là "Strategy Pattern". Ngay lập tức núi tiến hành refactor lại toàn bộ dự án.
## Áp dụng Strategy Pattern
Triết lý của stategy pattern:
```
Identify the aspects of your application that vary and separate them from what stays the same
(Có thể hiểu là tách những thứ thay đổi ra khỏi những thứ không thay đổi)
```
Núi thấy rằng việc sendEmail và sendFile có thể thay đổi giữa các dịch vụ, và sẽ tách sendEmail, sendFile ra khỏi class BaseService. Núi sẽ tiến hành thiết kế lại hệ thống:

```
<?php

interface EmailInterface
{
    public function sendEmail();
}

interface FileInterface
{
    public function sendFile($file);
}

class SendUserEmail implements EmailInterface
{
    public function sendEmail()
    {
        echo '[send mail for user]';
    }
}

class SendAdminUser implements EmailInterface
{
    public function sendEmail()
    {
        echo '[send mail for admin]';
    }
}

class AmazonS3 implements FileInterface
{
    public function sendFile($file)
    {
        echo '[logic send file api s3]' . $file . "\r";
    }
}

class Azure implements FileInterface
{
    public function sendFile($file)
    {
        echo '[logic send file api azure]' . $file . "\r";
    }
}

class GoogleDriver implements FileInterface
{
    public function sendFile($file)
    {
        echo '[logic send file api google driver]' . $file . "\r";
    }
}

class FileUpload
{
    private $mailService;
    private $fileService;

    public function setMailService(EmailInterface $mailService)
    {
        $this->mailService = $mailService;
    }

    public function setFileService(FileInterface $fileService)
    {
        $this->fileService = $fileService;
    }

    public function sendMail()
    {
        return $this->mailService->sendEmail();
    }

    public function sendFile($file)
    {
        return $this->fileService->sendFile($file);
    }
}

$file = 'jav.png';
$fileUpload = new FileUpload();
$fileUpload->setFileService(new GoogleDriver());
$fileUpload->setMailService(new SendUserEmail());
$fileUpload->sendFile($file); // [logic send file api google driver]jav.png
$fileUpload->sendMail(); // [send mail for user]
```

Bây giờ lớp dẫn xuất không còn phụ thuộc vào lớp kế thừa, dễ dang mở rộng bảo trì và thêm các phương thức khác mà không sợ bới tung cả dự án lên nữa.
Dù có thêm bao nhiêu service, hay khách hàng có thay đổi phần gửi email, núi cũng không còn sợ hãi như trước nữa, hệ thống bây giờ đã sẵn sàng đáp ứng những yêu cầu cho sự thay đổi.

## Bài học rút ra
- Việc thiết kế hệ thống quá vội vàng, hoặc không có chiều sâu giống như một căn bệnh ung thư vậy. Nó sẽ không đánh sập dự án của bạn ngay lập tức mà từ từ mài mòn hệ thống, tới một thời điểm nào đó dự án phình to ngoài tầm kiểm soát thì ... may mắn thì chúng ta sẽ được làm dự án mới, còn đen thì là công ty mới =))
- Đừng để người khác quyết định cuộc đời bạn, nếu như không có sự giúp sức của "H dân chơi đất cảng" thì số phận của Núi sẽ ra sao? Vì thế để quyết định vận mệnh của mình hãy tìm đọc "Head First Design Pattern".
- Đừng ngồi một chỗ quá lâu, đừng ngồi yên trong vòng an toàn. Thế giới tiến bộ không ngừng, tại sao bạn lại ngồi yên và tận hưởng vòng an toàn. Ngôn ngữ lập trình chỉ là công cụ, mô hình và kiến trúc hệ thống mới là "chân ái".
- Và cuối cùng núi đã có đáp án cho câu hỏi "Một ngày nào đó code cũng trờ về với cát bụi vậy chúng ta cố gắng viết code sạch để làm gì?".

## Happy ending
- Sau đó công ty the heaven với dự án FileDb đã vươn tầm thế giới, Núi sau này trở thành một techleader mẫu mực, lấy được một cô vợ xinh đẹp và giàu có, nhà lầu xe hơi mà không cần phải bán hàng online nữa. 
- Núi đã rút ra bài học cho bản thân "Tuổi trẻ đã trải sự đời", núi biết rằng thời gian rảnh mình cần phải học rất nhiều, đọc thật nhiều sách, đừng để thời gian trôi qua vô ích.

> Will Smith: “Đừng theo đuổi ai cả. Hãy là chính mình thôi. Hãy làm công việc của mình và làm chăm chỉ nhé. Người ấy sẽ xuất hiện thôi. Và người ấy sẽ ở lại bên bạn.”
