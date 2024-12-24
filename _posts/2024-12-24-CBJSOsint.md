---
title: 'OSINT CHALLENGE CYBERJUTSU 2024'
date: 2024-12-22
permalink: /posts/2024/12/cbjs-osint/
tags:
  - osint
---

Introduction
=====
<div style="text-align: center; size:50px">
  <img src="/images/cbjs-osint/intro.png" alt="" />
</div>
<br>
Vừa rồi mình có tham gia giải một challenge osint của CBJS, hôm nay có thời gian mình sẽ tranh thủ write-up lại challenge này cho mọi người cùng đọc

Description:
=====

##### 🎄🎅 THÔNG ĐIỆP BÍ ẨN GIỮA ĐÊM GIÁNG SINH

> Này các thành viên thân mến của đại gia đình CyberJutsu,
Giáng sinh đang đến gần, không khí lễ hội đã tràn ngập khắp nơi. Và năm nay còn đặc biệt hơn nữa khi chúng ta chạm mốc 2000 CyberJutsuers - một con số đáng tự hào biết bao! 🥳
Với tư cách là thành viên mới nhất của team, tôi đã âm thầm chuẩn bị những món quà bất ngờ, hy vọng mang đến niềm vui cho tất cả anh em trong đêm Noel ấm áp. 
NHƯNG KHÔNG THỂ NGỜ, kế hoạch đã bị một hacker táo tợn với nickname "solo_levelling" phá hoại! 😱
Không những lấy trộm toàn bộ quà, mà hắn ta còn xóa sạch source code lẫn backup, như thể muốn thách thức khả năng OSINT của chúng ta. Nhưng hắn đã quên mất một điều: Cộng đồng CyberJutsu luôn biết cách để vượt qua thử thách bằng sức mạnh tập thể! 💪
Vì thế, tôi kêu gọi 2000 hacker mũ trắng cùng chung tay truy tìm 3 món quà đặc biệt và tóm gọn tên tội phạm trước khi đồng hồ điểm 12 giờ đêm. Mỗi món quà đều chứa một thông điệp ý nghĩa mà team CyberJutsu dành tặng các bạn.
Nào, bắt tay vào "truy tìm kho báu" thôi! Mong rằng chúng ta sẽ cùng hoàn thành nhiệm vụ trước khi ông già Noel ghé thăm. Tin chắc rằng các ninja sẽ trổ tài và không bỏ sót bất kỳ flag nào nhé!

Như bao challenge osint khác, mình sẽ tìm kiếm các social account bằng cái username kia trước, mình sử dụng `sherlock` và dựa trên kinh nghiệm thì ra được 2 account này:

<div style="text-align: center; size:50px">
<img src="/images/cbjs-osint/github.png" alt="" />
</div>
<br>
<div style="text-align: center; size:50px">
<img src="/images/cbjs-osint/mastodon.png" alt="" />
</div>
<br>
Tìm kiếm một lúc trong github thì mình dễ dàng tìm được flag thứ nhất trong comment của commit trong repo duy nhất. 

<div style="text-align: center; size:50px">
<img src="/images/cbjs-osint/flag1.png" alt="" />
</div>
<br>
Chuyển sang khai thác thêm thông tin ở mastodon, lướt qua các bài post của tài khoản này thì mình thấy có một link drive (post này đã được modified, là một link drive khác nhưng đã bị xóa, mình có thử tải về xem thử nhưng không thấy khác mấy so với bản được sửa nên bỏ qua)

<div style="text-align: center; size:50px">
    <img src="/images/cbjs-osint/post-mas.png" alt="" />
</div>
<br>

Xem thử link drive thì nó là một video tự quay, xem đi xem lại thì mình phát hiện có một profile X bị lộ trên url của màn hình máy tính
<div style="text-align: center; size:50px">
    <img src="/images/cbjs-osint/drive.png" alt="" />
</div>
<br>
Bằng thị giác 10/10 ở tốc độ 0.2, độ phân giải 1080 thì mình đoán ngay được tài khoản X đó mà không cần bất kì công cụ hỗ trợ nào
<div style="text-align: center; size:50px">
    <img src="/images/cbjs-osint/X.png" alt="" />
</div>
<br>
Quét mã QR kia mình có được flag thứ hai.
Sau khoảng 15' stuck không biết tìm flag cuối ở đâu, mình quay lại đọc đề xem có sót thông tin nào không đồng thời cũng xem xem có ai solved chưa. Thì có một comment không liên quan đến challenge lắm (mình đã để ý tới comment này lúc đầu khi chưa ai comment nhưng do mải làm nên miss mất :(( )
<div style="text-align: center; size:50px">
    <img src="/images/cbjs-osint/comment.png" alt="" />
</div>
<br>
Thử vào xem tài khoản `Lê Trọng Quý` thì là một acc clone và chỉ có một post duy nhất và post này đã bị modified
<div style="text-align: center; size:50px">
    <img src="/images/cbjs-osint/facebook.png" alt="" />
</div>
<br>
<div style="text-align: center; size:50px">
    <img src="/images/cbjs-osint/link.png" alt="" />
</div>
<br>
Truy cập vào link shopee gốc thì dễ dàng mình tìm thấy flag cuối cùng đã bị Whitespace Encode ở phần mô tả :))))
<div style="text-align: center; size:50px">
    <img src="/images/cbjs-osint/shopee.png" alt="" />
</div>
<br>
<div style="text-align: center; size:50px">
    shopee
</div>
<div style="text-align: center; size:50px">
    <img src="/images/cbjs-osint/encode.png" alt="" />
</div>
<br>
<div style="text-align: center; size:50px">
    flag bị mã hóa
</div>
<div style="text-align: center; size:50px">
    <img src="/images/cbjs-osint/dcode.png" alt="" />
</div>
<br>
<div style="text-align: center; size:50px">
    flag cuối cùng
</div>