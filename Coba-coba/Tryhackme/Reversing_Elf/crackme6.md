# CRACKME 6
### DIKET
Analyze the binary for the easy password

### JAWAB
Sama seperti soal-soal sebelumnya, kita debug program crackme6 ini dengan r2, berikut adalah list fungsi yang ada
```
0x00400490    1 42           entry0
0x00400470    1 6            sym.imp.__libc_start_main
0x004004c0    4 41           sym.deregister_tm_clones
0x004004f0    4 57           sym.register_tm_clones
0x00400530    3 28           entry.fini0
0x00400550    4 45   -> 42   entry.init0
0x004007d0    1 2            sym.__libc_csu_fini
0x004007d4    1 9            sym._fini
0x004006d1    4 64           sym.compare_pwd
0x00400760    4 101          sym.__libc_csu_init
0x00400711    4 74           main
0x0040057d   28 340          sym.my_secure_test
0x00400418    3 26           sym._init
0x00400480    1 6            loc.imp.__gmon_start
0x00400450    1 6            sym.imp.puts
0x00400460    1 6            sym.imp.printf
```
maka kita coba cek di fungsi main dulu
```
 main ();
|           ; var int32_t var_10h @ rbp-0x10
|           ; var int32_t var_4h @ rbp-0x4
|           ; DATA XREF from entry0 @ 0x4004ad
|           0x00400711      55             push rbp
|           0x00400712      4889e5         mov rbp, rsp
|           0x00400715      4883ec10       sub rsp, 0x10
|           0x00400719      897dfc         mov dword [var_4h], edi
|           0x0040071c      488975f0       mov qword [var_10h], rsi
|           0x00400720      837dfc02       cmp dword [var_4h], 2
|       ,=< 0x00400724      741b           je 0x400741
|       |   0x00400726      488b45f0       mov rax, qword [var_10h]
|       |   0x0040072a      488b00         mov rax, qword [rax]
|       |   0x0040072d      4889c6         mov rsi, rax
|       |   0x00400730      bf10084000     mov edi, str.Usage_:__s_password__Good_luck__read_the_source ; 0x400810 ; "Usage : %s password\nGood luck, read the source\n"
|       |   0x00400735      b800000000     mov eax, 0
|       |   0x0040073a      e821fdffff     call sym.imp.printf
|      ,==< 0x0040073f      eb13           jmp 0x400754
|      |`-> 0x00400741      488b45f0       mov rax, qword [var_10h]
|      |    0x00400745      4883c008       add rax, 8
|      |    0x00400749      488b00         mov rax, qword [rax]
|      |    0x0040074c      4889c7         mov rdi, rax
|      |    0x0040074f      e87dffffff     call sym.compare_pwd
|      |    ; CODE XREF from main @ 0x40073f
|      `--> 0x00400754      b800000000     mov eax, 0
|           0x00400759      c9             leave
\           0x0040075a      c3             ret
```
Pada fungsi main, terdapat pemanggilan fungsi lain yakni terdapat pada address 0x0040073a dan 0x0040074f, karena kita sekarang mencoba masuk ke programnya, sehingga kita coba cek fungsi sym.compare_pwd saja untuk mencari stringnya, setelah dibuka terdapat source code berikut pada fungsi sym.compare_pwd
```
sym.compare_pwd ();
|           ; var int32_t var_8h @ rbp-0x8
|           ; CALL XREF from main @ 0x40074f
|           0x004006d1      55             push rbp
|           0x004006d2      4889e5         mov rbp, rsp
|           0x004006d5      4883ec10       sub rsp, 0x10
|           0x004006d9      48897df8       mov qword [var_8h], rdi
|           0x004006dd      488b45f8       mov rax, qword [var_8h]
|           0x004006e1      4889c7         mov rdi, rax
|           0x004006e4      e894feffff     call sym.my_secure_test
|           0x004006e9      85c0           test eax, eax
|       ,=< 0x004006eb      750c           jne 0x4006f9
|       |   0x004006ed      bfe8074000     mov edi, str.password_OK    ; 0x4007e8 ; "password OK"
|       |   0x004006f2      e859fdffff     call sym.imp.puts
|      ,==< 0x004006f7      eb16           jmp 0x40070f
|      |`-> 0x004006f9      488b45f8       mov rax, qword [var_8h]
|      |    0x004006fd      4889c6         mov rsi, rax
|      |    0x00400700      bff4074000     mov edi, str.password___s__not_OK ; 0x4007f4 ; "password \"%s\" not OK\n"
|      |    0x00400705      b800000000     mov eax, 0
|      |    0x0040070a      e851fdffff     call sym.imp.printf
|      |    ; CODE XREF from sym.compare_pwd @ 0x4006f7
|      `--> 0x0040070f      c9             leave
\           0x00400710      c3             ret
```
fungsi ini kembali memanggil fungsi lain yakni fungsi sym.my_secure_test, maka kita buka juga fungsi ini
```
|   sym.my_secure_test ();
|           ; var int32_t var_8h @ rbp-0x8
|           ; CALL XREF from sym.compare_pwd @ 0x4006e4
|           0x0040057d      55             push rbp
|           0x0040057e      4889e5         mov rbp, rsp
|           0x00400581      48897df8       mov qword [var_8h], rdi
|           0x00400585      488b45f8       mov rax, qword [var_8h]
|           0x00400589      0fb600         movzx eax, byte [rax]
|           0x0040058c      84c0           test al, al
|       ,=< 0x0040058e      740b           je 0x40059b
|       |   0x00400590      488b45f8       mov rax, qword [var_8h]
|       |   0x00400594      0fb600         movzx eax, byte [rax]
|       |   0x00400597      3c31           cmp al, 0x31                ; 49
|      ,==< 0x00400599      740a           je 0x4005a5
|      |`-> 0x0040059b      b8ffffffff     mov eax, 0xffffffff         ; -1
|      |,=< 0x004005a0      e92a010000     jmp 0x4006cf
|      `--> 0x004005a5      488b45f8       mov rax, qword [var_8h]
|       |   0x004005a9      4883c001       add rax, 1
|       |   0x004005ad      0fb600         movzx eax, byte [rax]
|       |   0x004005b0      84c0           test al, al
|      ,==< 0x004005b2      740f           je 0x4005c3
|      ||   0x004005b4      488b45f8       mov rax, qword [var_8h]
|      ||   0x004005b8      4883c001       add rax, 1
|      ||   0x004005bc      0fb600         movzx eax, byte [rax]
|      ||   0x004005bf      3c33           cmp al, 0x33                ; 51
|     ,===< 0x004005c1      740a           je 0x4005cd
|     |`--> 0x004005c3      b8ffffffff     mov eax, 0xffffffff         ; -1
|     |,==< 0x004005c8      e902010000     jmp 0x4006cf
|     `---> 0x004005cd      488b45f8       mov rax, qword [var_8h]
|      ||   0x004005d1      4883c002       add rax, 2
|      ||   0x004005d5      0fb600         movzx eax, byte [rax]
|      ||   0x004005d8      84c0           test al, al
|     ,===< 0x004005da      740f           je 0x4005eb
|     |||   0x004005dc      488b45f8       mov rax, qword [var_8h]
|     |||   0x004005e0      4883c002       add rax, 2
|     |||   0x004005e4      0fb600         movzx eax, byte [rax]
|     |||   0x004005e7      3c33           cmp al, 0x33                ; 51
|    ,====< 0x004005e9      740a           je 0x4005f5
|    |`---> 0x004005eb      b8ffffffff     mov eax, 0xffffffff         ; -1
|    |,===< 0x004005f0      e9da000000     jmp 0x4006cf
|    `----> 0x004005f5      488b45f8       mov rax, qword [var_8h]
|     |||   0x004005f9      4883c003       add rax, 3
|     |||   0x004005fd      0fb600         movzx eax, byte [rax]
|     |||   0x00400600      84c0           test al, al
|    ,====< 0x00400602      740f           je 0x400613
|    ||||   0x00400604      488b45f8       mov rax, qword [var_8h]
|    ||||   0x00400608      4883c003       add rax, 3
|    ||||   0x0040060c      0fb600         movzx eax, byte [rax]
|    ||||   0x0040060f      3c37           cmp al, 0x37                ; 55
|   ,=====< 0x00400611      740a           je 0x40061d
|   |`----> 0x00400613      b8ffffffff     mov eax, 0xffffffff         ; -1
|   |,====< 0x00400618      e9b2000000     jmp 0x4006cf
|   `-----> 0x0040061d      488b45f8       mov rax, qword [var_8h]
|    ||||   0x00400621      4883c004       add rax, 4
|    ||||   0x00400625      0fb600         movzx eax, byte [rax]
|    ||||   0x00400628      84c0           test al, al
|   ,=====< 0x0040062a      740f           je 0x40063b
|   |||||   0x0040062c      488b45f8       mov rax, qword [var_8h]
|   |||||   0x00400630      4883c004       add rax, 4
|   |||||   0x00400634      0fb600         movzx eax, byte [rax]
|   |||||   0x00400637      3c5f           cmp al, 0x5f                ; 95
|  ,======< 0x00400639      740a           je 0x400645
|  |`-----> 0x0040063b      b8ffffffff     mov eax, 0xffffffff         ; -1
|  |,=====< 0x00400640      e98a000000     jmp 0x4006cf
|  `------> 0x00400645      488b45f8       mov rax, qword [var_8h]
|   |||||   0x00400649      4883c005       add rax, 5
|   |||||   0x0040064d      0fb600         movzx eax, byte [rax]
|   |||||   0x00400650      84c0           test al, al
|  ,======< 0x00400652      740f           je 0x400663
|  ||||||   0x00400654      488b45f8       mov rax, qword [var_8h]
|  ||||||   0x00400658      4883c005       add rax, 5
|  ||||||   0x0040065c      0fb600         movzx eax, byte [rax]
|  ||||||   0x0040065f      3c70           cmp al, 0x70                ; 112
| ,=======< 0x00400661      7407           je 0x40066a
| |`------> 0x00400663      b8ffffffff     mov eax, 0xffffffff         ; -1
| |,======< 0x00400668      eb65           jmp 0x4006cf
| `-------> 0x0040066a      488b45f8       mov rax, qword [var_8h]
|  ||||||   0x0040066e      4883c006       add rax, 6
|  ||||||   0x00400672      0fb600         movzx eax, byte [rax]
|  ||||||   0x00400675      84c0           test al, al
| ,=======< 0x00400677      740f           je 0x400688
| |||||||   0x00400679      488b45f8       mov rax, qword [var_8h]
| |||||||   0x0040067d      4883c006       add rax, 6
| |||||||   0x00400681      0fb600         movzx eax, byte [rax]
| |||||||   0x00400684      3c77           cmp al, 0x77                ; 119
| ========< 0x00400686      7407           je 0x40068f
| `-------> 0x00400688      b8ffffffff     mov eax, 0xffffffff         ; -1
| ,=======< 0x0040068d      eb40           jmp 0x4006cf
| --------> 0x0040068f      488b45f8       mov rax, qword [var_8h]
| |||||||   0x00400693      4883c007       add rax, 7
| |||||||   0x00400697      0fb600         movzx eax, byte [rax]
| |||||||   0x0040069a      84c0           test al, al
| ========< 0x0040069c      740f           je 0x4006ad
| |||||||   0x0040069e      488b45f8       mov rax, qword [var_8h]
| |||||||   0x004006a2      4883c007       add rax, 7
| |||||||   0x004006a6      0fb600         movzx eax, byte [rax]
| |||||||   0x004006a9      3c64           cmp al, 0x64                ; 100
| ========< 0x004006ab      7407           je 0x4006b4
| --------> 0x004006ad      b8ffffffff     mov eax, 0xffffffff         ; -1
| ========< 0x004006b2      eb1b           jmp 0x4006cf
| --------> 0x004006b4      488b45f8       mov rax, qword [var_8h]
| |||||||   0x004006b8      4883c008       add rax, 8
| |||||||   0x004006bc      0fb600         movzx eax, byte [rax]
| |||||||   0x004006bf      84c0           test al, al
| ========< 0x004006c1      7407           je 0x4006ca
| |||||||   0x004006c3      b8ffffffff     mov eax, 0xffffffff         ; -1
| ========< 0x004006c8      eb05           jmp 0x4006cf
| --------> 0x004006ca      b800000000     mov eax, 0
| |||||||   ; XREFS: CODE 0x004005a0  CODE 0x004005c8  CODE 0x004005f0  CODE 0x00400618  CODE 0x00400640  
| |||||||   ; XREFS: CODE 0x00400668  CODE 0x0040068d  CODE 0x004006b2  CODE 0x004006c8  
| ```````-> 0x004006cf      5d             pop rbp
\           0x004006d0      c3             ret
```
karena sulit melihatnya karena kode begitu banyak, buka dalam mode graph viewer dengan command berikut
```
VV @sym.my_secure_test
```
Lalu, kita ambil saja karakter hexadecimal terlebih dahulu
0x31 0x33 0x33 0x37 0x5f 0x70 0x77 0x64
ketika dikonversi ke desimal menjadi 4951515595112119100, tetapi apabila dicoba dijalankan dengan password tersebut menghasilkan output salah
```
aldifp@yeet:~/Downloads$ ./crackme6 4951515595112119100
password "4951515595112119100" not OK
```
sehingga kita coba cara lain yaitu dengan menghapus semua 0x dan menghapus spasinya
dan diperoleh angka berikut yakni 3545233644588136292 dan kita coba jalankan dengan password menggunakan angka ini
```
aldifp@yeet:~/Downloads$ ./crackme6 3545233644588136292
password "3545233644588136292" not OK
```
karena masih salah, maka kita coba mengkonversi ke format ascii diperoleh string "1337_pwd" dan apabila dijalankan dengan inputan tersebut tidak salah sehingga diperoleh flagnya
```
aldifp@yeet:~/Downloads$ ./crackme6 1337_pwd
password OK
```
<details>
  <summary>Flag</summary>
  
  ```
  1337_pwd
  ```
</details>