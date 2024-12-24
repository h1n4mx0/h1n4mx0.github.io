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

Vừa rồi mình có tham gia giải một challenge osint của CBJS, hôm nay có thời gian mình sẽ tranh thủ write-up lại challenge này cho mọi người cùng đọc

Description:
=====
*
    ##### 🎄🎅 THÔNG ĐIỆP BÍ ẨN GIỮA ĐÊM GIÁNG SINH

    > Này các thành viên thân mến của đại gia đình CyberJutsu,
    Giáng sinh đang đến gần, không khí lễ hội đã tràn ngập khắp nơi. Và năm nay còn đặc biệt hơn nữa khi chúng ta chạm mốc 2000 CyberJutsuers - một con số đáng tự hào biết bao! 🥳
    Với tư cách là thành viên mới nhất của team, tôi đã âm thầm chuẩn bị những món quà bất ngờ, hy vọng mang đến niềm vui cho tất cả anh em trong đêm Noel ấm áp. 
    NHƯNG KHÔNG THỂ NGỜ, kế hoạch đã bị một hacker táo tợn với nickname `"solo_levelling"` phá hoại! 😱
    Không những lấy trộm toàn bộ quà, mà hắn ta còn xóa sạch source code lẫn backup, như thể muốn thách thức khả năng OSINT của chúng ta. Nhưng hắn đã quên mất một điều: Cộng đồng CyberJutsu luôn biết cách để vượt qua thử thách bằng sức mạnh tập thể! 💪
    Vì thế, tôi kêu gọi 2000 hacker mũ trắng cùng chung tay truy tìm 3 món quà đặc biệt và tóm gọn tên tội phạm trước khi đồng hồ điểm 12 giờ đêm. Mỗi món quà đều chứa một thông điệp ý nghĩa mà team CyberJutsu dành tặng các bạn.
    Nào, bắt tay vào "truy tìm kho báu" thôi! Mong rằng chúng ta sẽ cùng hoàn thành nhiệm vụ trước khi ông già Noel ghé thăm. Tin chắc rằng các ninja sẽ trổ tài và không bỏ sót bất kỳ flag nào nhé!

    Như bao challenge osint khác, mình sẽ tìm kiếm các social account bằng cái username kia trước, mình sử dụng `sherlock` và dựa trên kinh nghiệm thì ra được 2 account này:

    <div style="text-align: center; size:50px">
    <img src="/images/cbjs-osint/github.png" alt="" />
    </div>

    <div style="text-align: center; size:50px">
    <img src="/images/cbjs-osint/mastodon.png" alt="" />
    </div>

    Tìm kiếm một lúc trong github thì mình dễ dàng tìm được flag thứ nhất trong comment của commit trong repo duy nhất. 

    <div style="text-align: center; size:50px">
    <img src="/images/cbjs-osint/flag1.png" alt="" />
    </div>

