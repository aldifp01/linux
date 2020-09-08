# CRACKME 2
### DIKET
This is the second crackme file - Unlike the first file, this will involve examining registers, how and where values are compared

### JAWAB
Pada soal ini, jawaban kita debug dengan radare2, pertama jalankan radare dengan kode berikut
```
r2 -d ./crackme2.bin
```
lalu kita analisa semua kodenya dengan command "aaa" dan "afl" untuk langsung menampilkan fungsi yang ada, yakni sebagai berikut
```
0x55e14f9ae610    1 43           entry0
0x55e14fbaefe0    1 4124         reloc.__libc_start_main
0x55e14f9ae640    4 50   -> 40   sym.deregister_tm_clones
0x55e14f9ae680    4 66   -> 57   sym.register_tm_clones
0x55e14f9ae6d0    5 58   -> 51   entry.fini0
0x55e14f9ae600    1 6            sym..plt.got
0x55e14f9ae710    1 10           entry.init0
0x55e14f9ae810    1 2            sym.__libc_csu_fini
0x55e14f9ae814    1 9            sym._fini
0x55e14f9ae7a0    4 101          sym.__libc_csu_init
0x55e14f9ae71a    6 122          main
0x55e14f9ae5a0    3 23           sym._init
0x55e14f9ae5d0    1 6            sym.imp.puts
0x55e14f9ae5e0    1 6            sym.imp.__stack_chk_fail
0x55e14f9ae000    2 25           map.home_aldifp_Downloads_crackme2.bin.r_x
0x55e14f9ae5f0    1 6            sym.imp.__isoc99_scanf
```
kita langsung buka method main karena pasti proses terjadi pada method ini, untuk membukanya kita menggunakan comman "pdf @main". berdasarkan hint, "Check the format string of the input and what the value is compared against" maka pasti ada angka atau variabel yang menjadi pembandingnya
```
main ();
|           ; var int32_t var_ch @ rbp-0xc
|           ; var int32_t var_8h @ rbp-0x8
|           ; DATA XREF from entry0 @ 0x55e14f9ae62d
|           0x55e14f9ae71a      55             push rbp
|           0x55e14f9ae71b      4889e5         mov rbp, rsp
|           0x55e14f9ae71e      4883ec10       sub rsp, 0x10
|           0x55e14f9ae722      64488b042528.  mov rax, qword fs:[0x28]
|           0x55e14f9ae72b      488945f8       mov qword [var_8h], rax
|           0x55e14f9ae72f      31c0           xor eax, eax
|           0x55e14f9ae731      488d3dec0000.  lea rdi, qword str.enter_your_password ; 0x55e14f9ae824 ; "enter your password"                                                                                            
|           0x55e14f9ae738      e893feffff     call sym.imp.puts
|           0x55e14f9ae73d      488d45f4       lea rax, qword [var_ch]
|           0x55e14f9ae741      4889c6         mov rsi, rax
|           0x55e14f9ae744      488d3ded0000.  lea rdi, qword [0x55e14f9ae838] ; "%d"
|           0x55e14f9ae74b      b800000000     mov eax, 0
|           0x55e14f9ae750      e89bfeffff     call sym.imp.__isoc99_scanf
|           0x55e14f9ae755      8b45f4         mov eax, dword [var_ch]
|           0x55e14f9ae758      3d7c130000     cmp eax, 0x137c
|       ,=< 0x55e14f9ae75d      750e           jne 0x55e14f9ae76d
|       |   0x55e14f9ae75f      488d3dd50000.  lea rdi, qword str.password_is_valid ; 0x55e14f9ae83b ; "password is valid"                                                                                                
|       |   0x55e14f9ae766      e865feffff     call sym.imp.puts
|      ,==< 0x55e14f9ae76b      eb0c           jmp 0x55e14f9ae779
|      |`-> 0x55e14f9ae76d      488d3dd90000.  lea rdi, qword str.password_is_incorrect ; 0x55e14f9ae84d ; "password is incorrect"                                                                                        
|      |    0x55e14f9ae774      e857feffff     call sym.imp.puts
|      |    ; CODE XREF from main @ 0x55e14f9ae76b
|      `--> 0x55e14f9ae779      b800000000     mov eax, 0
|           0x55e14f9ae77e      488b55f8       mov rdx, qword [var_8h]
|           0x55e14f9ae782      644833142528.  xor rdx, qword fs:[0x28]
|       ,=< 0x55e14f9ae78b      7405           je 0x55e14f9ae792
|       |   0x55e14f9ae78d      e84efeffff     call sym.imp.__stack_chk_fail
|       `-> 0x55e14f9ae792      c9             leave
\           0x55e14f9ae793      c3             ret
```
pada baris
```
0x55e14f9ae758      3d7c130000     cmp eax, 0x137c
```
terdapat method assembly cmp, yakni compare yang berguna untuk membandingkan inputan dengan 0x137c, maka kita tinggal konversi 0x137c menjadi desimal dan diperoleh 4988. Apabila diinputkan pada program akan menghasilkan output berikut
```
root@yeet:/home/aldifp/Downloads# ./crackme2.bin 
enter your password
4988
password is valid
```

