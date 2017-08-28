---
title: PHP | Vấn đề bảo mật (security) khi làm việc PHP với Ajax.
description: Hẳn có nhiều dev đang găpj phải vấn đề này. Một khi bạn hoặc một ai trong team chủ quan thì có thể trả giá đắt.
header: PHP | Vấn đề bảo mật (security) khi làm việc PHP với Ajax.
---
Đầu tiên với một dev mới vào nghề, họ chỉ biết chạy được câu lệnh hay một chức năng nào đó. Nhưng đối với một dev nhiều kinh nghiệm thì vấn đề này không thể bỏ qua bời vì họ biết nếu bỏ qua Security cho một request thì đồng nghĩa với việc họ tiếp tay cho hackers.

Bài này chúng ta sẽ đi tìm một phương án tích cực trong việc post data sử dụng ```Ajax đến php or một language nào đó.

Để trả lời cho câu hỏi này , ####oldprogrammersneverdie tìm hiểu rất nhiều trên google và cho kết qủa chung;

### Hãy sử dụng token..

###### ? How to? 

## Step1: - Tạo một token trên toàn server + client;

{% highlight php linenos %}

<?php
  session_start();
  $token = md5(rand(1000,9999)); //Có thể tạo nhiều dạng  khác nhau..
  $_SESSION['token'] = $token; //tạo session cho token này
?>

{% endhighlight %}

## Step-2 : Sử dụng token vừa tạo khi gửi ajax lên server.

{% highlight php linenos %}

var form_data = {
  data: $("#data").val(), //data 
  token:'<?php echo $token; ?>', //token ở đây
  is_ajax: 1
};

$.ajax({
  type: "POST",
  url: 'yourajax_url_here',
  data: form_data,
  success: function(response)
  {
    // code của bạn ở đây khi có response
  }
});

{% endhighlight %}


## Step-3 : Bậy giờ làm việc với file php

{% highlight php linenos %}

session_start(); 
if($_SERVER['HTTP_X_REQUESTED_WITH'] == 'XMLHttpRequest') {

	//check đúng domain của mình thì mới cho vào
  if(@isset($_SERVER['HTTP_REFERER']) && $_SERVER['HTTP_REFERER']=="http://yourdomain/ajaxurl")
  {
  	// nếu token client === token server 
    if($_POST['token'] == $_SESSION['token']) {
      // làm việc ở đâynếu mọi thứ cho phép.
    }
    else {
      header('Location: http://yourdomain.com');
    }
  }
  else {
    header('Location: http://yourdomain.com');
  }
}
else {
  header('Location: http://yourdomain.com');
}


{% endhighlight %}


``` Done! Bạn nào có phương án nào tốt hơn thì phát biêyr nhé. Và cũng còn một cách mà tôi đã được học qua khi làm việc với paymentwall.com.Một trong những parner tốt nhất về thanh toán thế giới.