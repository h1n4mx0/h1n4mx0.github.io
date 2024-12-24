---
title: 'OSINT CHALLENGE MSEC 2024'
date: 2024-12-22
permalink: /posts/2024/12/msec-osint/
tags:
  - osint
---

Introduction
=====
<div style="text-align: center; size:50px">
  <img src="/images/msec-osint/intro.png" alt="" />
</div>
<br>
Nhân dịp 80 năm thành lập Quân đội nhân dân Việt Nam và 35 năm Ngày hội Quốc phòng Toàn dân, MSEC có một thử thách Osint, và đây là wu của mình

Description:
=====

> Xylya Noreena là một thành viên trong tổ chức tội phạm chuyên nhắm vào thông tin cá nhân của người dân Việt Nam. Hãy vận dụng kỹ năng OSINT của bạn để tìm kiếm thông tin về cô ta và khám phá những bí mật mà tổ chức này đang nắm giữ! (Lưu ý: Tất cả thông tin chỉ mang tính chất tái tạo cho thử thách).

Ta dễ dàng tìm thấy tài khoản X của `Xylya Noreena`

<div style="text-align: center; size:50px">
<img src="/images/msec-osint/X.png" alt="" />
</div>
<br>
Nhưng không có gì ở đây ngoài 2 thông tin sau:
* Alias: `X_n0r33n4`
* Birthday: `December 25, 2000`

Dùng alias thì sẽ tìm được 2 social account khác:

<div style="text-align: center; size:50px">
      <img src="/images/msec-osint/igthread.png" alt="" />
</div>
<br>

Trong IG thì không có gì, còn thread thì sẽ có một số thông tin, trong đó có 1 post có ảnh

<div style="text-align: center; size:50px">
<img src="/images/msec-osint/anh.png" alt="" />
</div>
<br>
Để ý kỹ thì sẽ thấy góc trên bên trái bức ảnh có một tab telegram

<div style="text-align: center; size:50px">
    <img src="/images/msec-osint/cluetele.png" alt="" />
</div>
<br>
Chỗ này sẽ hơi brute một chút, mọi người có thể đoán được `@Xylya_...` có thể là user, channel, group hoặc bot để tìm ra sau dấu _ là gì. Ngoài ra có thể dựa vào chính bức ảnh để dễ dàng hơn trong việc đoán ra đây là một con bot telegram tên là `@Xylya_bot`. Khi tìm thấy con bot trên tele, mọi người sẽ thấy có một nút `Bot Privacy Policy`
<div style="text-align: center; size:50px">
    <img src="/images/msec-osint/bot.png" alt="" />
</div>
<br>
Ấn vào sẽ được chuyển sang một channel khác có tên là `1337Signal`
<div style="text-align: center; size:50px">
    <img src="/images/msec-osint/signal.png" alt="" />
</div>
<br>
Bỏ qua các chi tiết gây nhiễu, tập trung vào 2 file zip được gửi
<div style="text-align: center; size:50px">
    <img src="/images/msec-osint/zip.png" alt="" />
</div>
<br>
Ở file zip đầu tiên ta sẽ dễ dàng tìm được part 1 của flag theo đường dẫn `StealerLog_25-11-2024.zip\1337.1337.1337.1\Accounts\credencial`
<div style="text-align: center; size:50px">
    <img src="/images/msec-osint/part1.png" alt="" />
</div>
<br>
> FLAG_PART1: MSEC{m3rRy_cH1s

Quay trở lại thread ta sẽ thấy ở post đầu tiên có một comment khá lạ, nhưng với những CTFer tài năng thì dễ dàng nhận ra ngay đây là Ecoji, việc cần làm là tìm [tool](https://ecoji.io/) để giải mã
<div style="text-align: center; size:50px">
    <img src="/images/msec-osint/post1.png" alt="" />
</div>
<br>
<div style="text-align: center; size:50px">
    <img src="/images/msec-osint/ecoji.png" alt="" />
</div>
<br>
Đây là một link pastebin nhưng đã bị khóa bằng mật khẩu, bây giờ ta phải tìm mật khẩu để mở nó. Đến bước này ta còn 1 dữ kiện chưa sử dụng là file zip thứ 2. Để ý thì tin nhắn có đề cập tới một người khác là `luk45`
<div style="text-align: center; size:50px">
    <img src="/images/msec-osint/zip2.png" alt="" />
</div>
<br>
Dựa vào nội dung tin nhắn thì có thể đoán được trong file zip log kia, mật khẩu của `luk45` đã bị lộ
<div style="text-align: center; size:50px">
    <img src="/images/msec-osint/pass.png" alt="" />
</div>
<br>
> Password của luk45: `SIGNALluk4512072001`

Nhưng chú ý rằng, đây là mật khẩu của luk45, dĩ nhiên không thể mở được pastebin của noreena. Lúc này cần phải tổng hợp lại tất cả những thông tin từ đầu tới giờ để đoán ra mật khẩu thực sự của noreena. Dựa vào post mới nhất của noreena trên thread cùng với lời nhắc nhở đổi mật khẩu ta dự đoán luk45 và noreena thuộc cùng một tổ chức. Để ý kỹ vào password bị lộ: 

`SIGNALluk4512072001`

Ta thấy password này được tạo nên từ 3 thành phần `SIGNAL` + `luk45` + `12072001`. Vậy đây chính là mật khẩu mặc định tổ chức cấp cho thành viên, được tạo thành từ `tên tổ chức` + `alias` + `DOB` => noreena có thể cũng sử dụng định dạng mật khẩu này

Tái tạo mật khẩu của noreena từ những thông tin ở X: `SIGNALX_n0r33n425122000`

Bingo!! vậy ta đã mở được pastebin và lấy được part 2 của flag
<div style="text-align: center; size:50px">
    <img src="/images/msec-osint/part2.png" alt="" />
</div>
<br>
> FLAG: `MSEC{m3rRy_cH1sm4s_0r_merry_chrismas!!!}`