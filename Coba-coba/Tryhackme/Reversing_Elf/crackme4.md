# CRACKME 4
### DIKET
Analyze and find the password for the binary?

### JAWAB
Kita coba analisa menggunakan r2, dan diperoleh sebagai berikut
```
main ();
|           ; var int32_t var_10h @ rbp-0x10
|           ; var int32_t var_4h @ rbp-0x4
|           ; DATA XREF from entry0 @ 0x40055d
|           0x00400716      55             push rbp
|           0x00400717      4889e5         mov rbp, rsp
|           0x0040071a      4883ec10       sub rsp, 0x10
|           0x0040071e      897dfc         mov dword [var_4h], edi
|           0x00400721      488975f0       mov qword [var_10h], rsi
|           0x00400725      837dfc02       cmp dword [var_4h], 2
|       ,=< 0x00400729      741b           je 0x400746
|       |   0x0040072b      488b45f0       mov rax, qword [var_10h]
|       |   0x0040072f      488b00         mov rax, qword [rax]
|       |   0x00400732      4889c6         mov rsi, rax
|       |   0x00400735      bf10084000     mov edi, str.Usage_:__s_password__This_time_the_string_is_hidden_and_we_used_strcmp ; 0x400810 ; "Usage : %s password\nThis time the string is hidden and we used strcmp\n"
|       |   0x0040073a      b800000000     mov eax, 0
|       |   0x0040073f      e8bcfdffff     call sym.imp.printf
|      ,==< 0x00400744      eb13           jmp 0x400759
|      |`-> 0x00400746      488b45f0       mov rax, qword [var_10h]
|      |    0x0040074a      4883c008       add rax, 8
|      |    0x0040074e      488b00         mov rax, qword [rax]
|      |    0x00400751      4889c7         mov rdi, rax
|      |    0x00400754      e821ffffff     call sym.compare_pwd
|      |    ; CODE XREF from main @ 0x400744
|      `--> 0x00400759      b800000000     mov eax, 0
|           0x0040075e      c9             leave
\           0x0040075f      c3             ret
```
karena dengan radare2 kita tidak menemukan perintah strcmp, maka kita coba debugger lain yakni gdb, ketika sudah masuk ke gdb, kita coba lihat fungsi yang ada dengan command "info functions" dan diperoleh fungsi sebagai berikut
```
0x00000000004004b0  _init
0x00000000004004e0  puts@plt
0x00000000004004f0  __stack_chk_fail@plt
0x0000000000400500  printf@plt
0x0000000000400510  __libc_start_main@plt
0x0000000000400520  strcmp@plt
0x0000000000400530  __gmon_start__@plt
0x0000000000400540  _start
0x0000000000400570  deregister_tm_clones
0x00000000004005a0  register_tm_clones
0x00000000004005e0  __do_global_dtors_aux
0x0000000000400600  frame_dummy
0x000000000040062d  get_pwd
0x000000000040067a  compare_pwd
0x0000000000400716  main
0x0000000000400760  __libc_csu_init
0x00000000004007d0  __libc_csu_fini
0x00000000004007d4  _fini
```
berdasarkan clue, maka kita buat breakpoint pada fungsi strcmp@plt ini dengan command berikut
```
b *0x0000000000400520   
```
lalu kita jalankan dengan sembarang string sebagai password, dan diperoleh output berikut
```
Starting program: /home/aldifp/Downloads/crackme4 password

Breakpoint 1, 0x0000000000400520 in strcmp@plt ()
```
Karena ketika menginputkan password, string kita pasti dibandingkan dengan string yang ada pada program ini, maka kita bisa menganalisa register yang ada pada program ini dengan command "info registers" dan diperoleh output berikut
```
(gdb) info registers
rax            0x7fffffffdef0      140737488346864
rbx            0x0                 0
rcx            0x11                17
rdx            0x7fffffffe39c      140737488348060
rsi            0x7fffffffe39c      140737488348060
rdi            0x7fffffffdef0      140737488346864
rbp            0x7fffffffdf10      0x7fffffffdf10
rsp            0x7fffffffded8      0x7fffffffded8
r8             0x0                 0
r9             0x7ffff7fe3530      140737354020144
r10            0xfffffffffffff3cf  -3121
r11            0x7ffff7e14d20      140737352125728
r12            0x400540            4195648
r13            0x7fffffffe010      140737488347152
r14            0x0                 0
r15            0x0                 0
rip            0x400520            0x400520 <strcmp@plt>
eflags         0x246               [ PF ZF IF ]
cs             0x33                51
ss             0x2b                43
ds             0x0                 0
es             0x0                 0
fs             0x0                 0
gs             0x0                 0
```
terdapat beberapa variabel yakni rax,rdx,rsi,rdi,rbp dan rsp yang kemungkinan menyembunyikan passwordnya, kita bisa lihat isi masing-masing variabel ini dengan menggunakan command x/s, ketika dicoba diperoleh output sebagai berikut
```
(gdb) x/s 0x7fffffffdef0
0x7fffffffdef0: "my_m0r3_secur3_pwd"
(gdb) x/s 0x7fffffffe39c
0x7fffffffe39c: "password"
(gdb) x/s 0x7fffffffdf10
0x7fffffffdf10: "0\337\377\377\377\177"
(gdb) x/s 0x7fffffffded8
0x7fffffffded8: "\332\006@"
```
ketika sudah variabel rbp (beberapa variabel lain di skip karena memiliki pointer yang sama sehingga isinya pasti juga sama), outputnya sudah mulai tidak jelas, hanya pointer dari rax dan rdx yang menghasilkan string yang bisa dibaca, tetapi pointer dari rax menghasilkan string yang sangat mirip dengan gaya-gaya penulisan kebanyakan flag, sehingga kita coba saja jalankan lagi program crackme4 dengan password my_m0r3_secur3_pwd dan diperoleh output berikut
```
aldifp@yeet:~/Downloads$ ./crackme4 my_m0r3_secur3_pwd
password OK
```
sehingga diperoleh flag sebagai berikut
<details>
  <summary>Flag</summary>
  
  ```
  my_m0r3_secur3_pwd
  ```
</details>
