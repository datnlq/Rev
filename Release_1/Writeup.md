# WriteUp Release One

## Es Crack

Đầu tiên dùng câu lệnh file để kiểm tra xem file này là file thực thi bao nhiêu bit thì chúng ta sẽ sử dụng IDA phù hợp để phân tích, sau khi check mới phát hiện ra rằng đây là file thực thi trên LINUX.
Sau khi dùng IDA phân tích và đọc code ASM theo flow hoạt động của chương trình ta nhận thấy chuỗi đưa vào sẽ được so sánh với biến *password* và sau đó sẽ in ra chuỗi được xác định trước. Ta nhận thấy giá trị mà biến *password* = P455w0rd :<
Sau đó chúng ta qua LINUX chạy và check thử đáp án !
```
Code inhere
```

Và xong

## crack_nasm

Check file thì thấy đây là 1 filt ELF 32-bit điều đó có nghĩa là chúng ta sẽ dùng IDA 32bits để phân tích hoặc có thể dùng dbg để phân tích.\
Flow của chương trình đó chính là nhận input nhập vào , sau đó khởi tạo flag rồi so sánh input == flag đúng thì sẽ in ra dòng *you are correct!*

```
0x08048080 <+0>:	mov    eax,0x4
   0x08048085 <+5>:	mov    ebx,0x1
   0x0804808a <+10>:	mov    ecx,0x8049170
   0x0804808f <+15>:	mov    edx,0x7
   0x08048094 <+20>:	int    0x80
   0x08048096 <+22>:	mov    eax,0x3
   0x0804809b <+27>:	mov    ebx,0x0
   0x080480a0 <+32>:	mov    ecx,0x80491a8
   0x080480a5 <+37>:	mov    edx,0xb
   0x080480aa <+42>:	int    0x80
   0x080480ac <+44>:	mov    eax,0x80491b3
   0x080480b1 <+49>:	mov    BYTE PTR [eax],0x53
   0x080480b4 <+52>:	add    eax,0x1
   0x080480b7 <+55>:	mov    BYTE PTR [eax],0x33
   0x080480ba <+58>:	add    eax,0x1
   0x080480bd <+61>:	mov    BYTE PTR [eax],0x43
   0x080480c0 <+64>:	add    eax,0x1
   0x080480c3 <+67>:	mov    BYTE PTR [eax],0x72
   0x080480c6 <+70>:	add    eax,0x1
   0x080480c9 <+73>:	mov    BYTE PTR [eax],0x45
   0x080480cc <+76>:	add    eax,0x1
   0x080480cf <+79>:	mov    BYTE PTR [eax],0x2b
   0x080480d2 <+82>:	add    eax,0x1
   0x080480d5 <+85>:	mov    BYTE PTR [eax],0x46
   0x080480d8 <+88>:	add    eax,0x1
   0x080480db <+91>:	mov    BYTE PTR [eax],0x6c
   0x080480de <+94>:	add    eax,0x1
   0x080480e1 <+97>:	mov    BYTE PTR [eax],0x34
   0x080480e4 <+100>:	add    eax,0x1
   0x080480e7 <+103>:	mov    BYTE PTR [eax],0x47
   0x080480ea <+106>:	add    eax,0x1
   0x080480ed <+109>:	mov    BYTE PTR [eax],0x21
   0x080480f0 <+112>:	xor    ebx,ebx
   0x080480f2 <+114>:	xor    ecx,ecx
   0x080480f4 <+116>:	mov    ecx,DWORD PTR ds:0x80491b3
   0x080480fa <+122>:	mov    ebx,DWORD PTR ds:0x80491a8
   0x08048100 <+128>:	cmp    ecx,ebx
   0x08048102 <+130>:	jne    0x8048112 <failure>
   0x08048104 <+132>:	jmp    0x8048132 <success>
   0x08048106 <+134>:	call   0x804814f <ClearTerminal>
   0x0804810b <+139>:	mov    eax,0x1
   0x08048110 <+144>:	int    0x80

```

Ta tìm được flag = S3CrE+Fl4G!

## S_Crackme1

Check file ta được  PE32 có nghĩa đây là file thực thi trên WINDOW nên chúng ta dùng IDA Pro 32 bit để phân tích và tìm ra flow của chương trình !

