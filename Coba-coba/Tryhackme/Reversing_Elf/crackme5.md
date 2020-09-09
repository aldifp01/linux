# CRACKME 5
### DIKET
What will be the input of the file to get output "Good game" ?

### JAWAB
Karena menggunakan command strings tidak menampilkan flag, maka kita debug dengan gdb ataupun r2. Untuk soal ini saya memakai r2.
pertama, kita buka file crackme5 dengan r2 lalu kita analisa dengan command "aaa" dan melihat semua fungsinya dengan command "afl", hal serupa bisa juga dilakukan di gdb dengan command "info functions", ketika sudah terlihat semua fungsinya maka kita buka fungsi main dan diperoleh source code berikut
```
 main ();
|           ; var int32_t var_70h @ rbp-0x70
|           ; var int32_t var_64h @ rbp-0x64
|           ; var int32_t var_54h @ rbp-0x54
|           ; var int32_t var_50h @ rbp-0x50
|           ; var int32_t var_30h @ rbp-0x30
|           ; var int32_t var_2fh @ rbp-0x2f
|           ; var int32_t var_2eh @ rbp-0x2e
|           ; var int32_t var_2dh @ rbp-0x2d
|           ; var int32_t var_2ch @ rbp-0x2c
|           ; var int32_t var_2bh @ rbp-0x2b
|           ; var int32_t var_2ah @ rbp-0x2a
|           ; var int32_t var_29h @ rbp-0x29
|           ; var int32_t var_28h @ rbp-0x28
|           ; var int32_t var_27h @ rbp-0x27
|           ; var int32_t var_26h @ rbp-0x26
|           ; var int32_t var_25h @ rbp-0x25
|           ; var int32_t var_24h @ rbp-0x24
|           ; var int32_t var_23h @ rbp-0x23
|           ; var int32_t var_22h @ rbp-0x22
|           ; var int32_t var_21h @ rbp-0x21
|           ; var int32_t var_20h @ rbp-0x20
|           ; var int32_t var_1fh @ rbp-0x1f
|           ; var int32_t var_1eh @ rbp-0x1e
|           ; var int32_t var_1dh @ rbp-0x1d
|           ; var int32_t var_1ch @ rbp-0x1c
|           ; var int32_t var_1bh @ rbp-0x1b
|           ; var int32_t var_1ah @ rbp-0x1a
|           ; var int32_t var_19h @ rbp-0x19
|           ; var int32_t var_18h @ rbp-0x18
|           ; var int32_t var_17h @ rbp-0x17
|           ; var int32_t var_16h @ rbp-0x16
|           ; var int32_t var_15h @ rbp-0x15
|           ; var int32_t var_8h @ rbp-0x8
|           ; DATA XREF from entry0 @ 0x4005fd
|           ; CALL XREF from sym.check @ 0x4008c3
|           0x00400773      55             push rbp
|           0x00400774      4889e5         mov rbp, rsp
|           0x00400777      4883ec70       sub rsp, 0x70
|           0x0040077b      897d9c         mov dword [var_64h], edi
|           0x0040077e      48897590       mov qword [var_70h], rsi
|           0x00400782      64488b042528.  mov rax, qword fs:[0x28]
|           0x0040078b      488945f8       mov qword [var_8h], rax
|           0x0040078f      31c0           xor eax, eax
|           0x00400791      c645d04f       mov byte [var_30h], 0x4f    ; 'O' ; 79
|           0x00400795      c645d166       mov byte [var_2fh], 0x66    ; 'f' ; 102
|           0x00400799      c645d264       mov byte [var_2eh], 0x64    ; 'd' ; 100
|           0x0040079d      c645d36c       mov byte [var_2dh], 0x6c    ; 'l' ; 108
|           0x004007a1      c645d444       mov byte [var_2ch], 0x44    ; 'D' ; 68
|           0x004007a5      c645d553       mov byte [var_2bh], 0x53    ; 'S' ; 83
|           0x004007a9      c645d641       mov byte [var_2ah], 0x41    ; 'A' ; 65
|           0x004007ad      c645d77c       mov byte [var_29h], 0x7c    ; '|' ; 124
|           0x004007b1      c645d833       mov byte [var_28h], 0x33    ; '3' ; 51
|           0x004007b5      c645d974       mov byte [var_27h], 0x74    ; 't' ; 116
|           0x004007b9      c645da58       mov byte [var_26h], 0x58    ; 'X' ; 88
|           0x004007bd      c645db62       mov byte [var_25h], 0x62    ; 'b' ; 98
|           0x004007c1      c645dc33       mov byte [var_24h], 0x33    ; '3' ; 51
|           0x004007c5      c645dd32       mov byte [var_23h], 0x32    ; '2' ; 50
|           0x004007c9      c645de7e       mov byte [var_22h], 0x7e    ; '~' ; 126
|           0x004007cd      c645df58       mov byte [var_21h], 0x58    ; 'X' ; 88
|           0x004007d1      c645e033       mov byte [var_20h], 0x33    ; '3' ; 51
|           0x004007d5      c645e174       mov byte [var_1fh], 0x74    ; 't' ; 116
|           0x004007d9      c645e258       mov byte [var_1eh], 0x58    ; 'X' ; 88
|           0x004007dd      c645e340       mov byte [var_1dh], 0x40    ; '@' ; 64
|           0x004007e1      c645e473       mov byte [var_1ch], 0x73    ; 's' ; 115
|           0x004007e5      c645e558       mov byte [var_1bh], 0x58    ; 'X' ; 88
|           0x004007e9      c645e660       mov byte [var_1ah], 0x60    ; '`' ; 96
|           0x004007ed      c645e734       mov byte [var_19h], 0x34    ; '4' ; 52
|           0x004007f1      c645e874       mov byte [var_18h], 0x74    ; 't' ; 116
|           0x004007f5      c645e958       mov byte [var_17h], 0x58    ; 'X' ; 88
|           0x004007f9      c645ea74       mov byte [var_16h], 0x74    ; 't' ; 116
|           0x004007fd      c645eb7a       mov byte [var_15h], 0x7a    ; 'z' ; 122
|           0x00400801      bf54094000     mov edi, str.Enter_your_input: ; 0x400954 ; "Enter your input:"
|           0x00400806      e865fdffff     call sym.imp.puts
|           0x0040080b      488d45b0       lea rax, qword [var_50h]
|           0x0040080f      4889c6         mov rsi, rax
|           0x00400812      bf66094000     mov edi, 0x400966
|           0x00400817      b800000000     mov eax, 0
|           0x0040081c      e89ffdffff     call sym.imp.__isoc99_scanf
|           0x00400821      488d55d0       lea rdx, qword [var_30h]
|           0x00400825      488d45b0       lea rax, qword [var_50h]
|           0x00400829      4889d6         mov rsi, rdx
|           0x0040082c      4889c7         mov rdi, rax
|           0x0040082f      e8a2feffff     call sym.strcmp
|           0x00400834      8945ac         mov dword [var_54h], eax
|           0x00400837      837dac00       cmp dword [var_54h], 0
|       ,=< 0x0040083b      750c           jne 0x400849
|       |   0x0040083d      bf69094000     mov edi, str.Good_game      ; 0x400969 ; "Good game"
|       |   0x00400842      e829fdffff     call sym.imp.puts
|      ,==< 0x00400847      eb0a           jmp 0x400853
|      |`-> 0x00400849      bf73094000     mov edi, str.Always_dig_deeper ; 0x400973 ; "Always dig deeper"
|      |    0x0040084e      e81dfdffff     call sym.imp.puts
|      |    ; CODE XREF from main @ 0x400847
|      `--> 0x00400853      b800000000     mov eax, 0
|           0x00400858      488b4df8       mov rcx, qword [var_8h]
|           0x0040085c      6448330c2528.  xor rcx, qword fs:[0x28]
|       ,=< 0x00400865      7405           je 0x40086c
|       |   0x00400867      e824fdffff     call sym.imp.__stack_chk_fail
|       `-> 0x0040086c      c9             leave
\           0x0040086d      c3             ret
```
Apabila dianalisa dengan melihat saja, pada address 0x00400791 sampai 0x004007fd terdapat char yang dapat dipastikan itu adalah bagian dari karakter dari string untuk perbandingan dengan input.
Pada assembly, terdapat beberapa variabel. Pada ELF 32-bit diawali dengan esi, edi dan seterusnya, sedangkan eax,ebx,ecx,edx adalah register. Sedangkan untuk ELF 64-bit registernya adalah rax,rbx,rcx, dan rdx, variabelnya sendiri dimulai dari rsi, rdi dan seterusnya.
Sehingga, kita buat breakpoint terlebih dahulu pada address 0x0040082f.
Ketika sudah dibuat breakpoint, kita lihat isi konten dari address tersebut dengan menjalankan command "dc" dan menginputkan sembarang string, setelah itu kita lihat isi konten dari masing-masing variabel dan berikut hasilnya
```
[0x7f4f48153090]> db 0x0040082f
[0x7f4f48153090]> dc
Enter your input:
testing
hit breakpoint at: 40082f
[0x0040082f]> px @rsi
- offset -       0 1  2 3  4 5  6 7  8 9  A B  C D  E F  0123456789ABCDEF
0x7ffd654d7f30  4f66 646c 4453 417c 3374 5862 3332 7e58  OfdlDSA|3tXb32~X
0x7ffd654d7f40  3374 5840 7358 6034 7458 747a 0000 0000  3tX@sX`4tXtz....
0x7ffd654d7f50  4080 4d65 fd7f 0000 00d9 8bee 13f5 9bdd  @.Me............
0x7ffd654d7f60  d008 4000 0000 0000 0b6e f947 4f7f 0000  ..@......n.GO...
0x7ffd654d7f70  0000 0000 0000 0000 4880 4d65 fd7f 0000  ........H.Me....
0x7ffd654d7f80  0000 0000 0100 0000 7307 4000 0000 0000  ........s.@.....
0x7ffd654d7f90  0000 0000 0000 0000 6c11 c9fe 30ef 0355  ........l...0..U
0x7ffd654d7fa0  e005 4000 0000 0000 4080 4d65 fd7f 0000  ..@.....@.Me....
0x7ffd654d7fb0  0000 0000 0000 0000 0000 0000 0000 0000  ................
0x7ffd654d7fc0  6c11 8911 2a25 f9aa 6c11 ef34 4260 9dab  l...*%..l..4B`..
0x7ffd654d7fd0  0000 0000 0000 0000 0000 0000 0000 0000  ................
0x7ffd654d7fe0  0000 0000 0000 0000 0000 0000 0000 0000  ................
0x7ffd654d7ff0  0000 0000 0000 0000 0000 0000 0000 0000  ................
0x7ffd654d8000  0000 0000 0000 0000 0000 0000 0000 0000  ................
0x7ffd654d8010  e005 4000 0000 0000 4080 4d65 fd7f 0000  ..@.....@.Me....
0x7ffd654d8020  0000 0000 0000 0000 0906 4000 0000 0000  ..........@.....
[0x0040082f]> px @rdi
- offset -       0 1  2 3  4 5  6 7  8 9  A B  C D  E F  0123456789ABCDEF
0x7ffd654d7f10  7465 7374 696e 6700 0000 0000 0000 0000  testing.........
0x7ffd654d7f20  0100 0000 0000 0000 1d09 4000 0000 0000  ..........@.....
0x7ffd654d7f30  4f66 646c 4453 417c 3374 5862 3332 7e58  OfdlDSA|3tXb32~X
0x7ffd654d7f40  3374 5840 7358 6034 7458 747a 0000 0000  3tX@sX`4tXtz....
0x7ffd654d7f50  4080 4d65 fd7f 0000 00d9 8bee 13f5 9bdd  @.Me............
0x7ffd654d7f60  d008 4000 0000 0000 0b6e f947 4f7f 0000  ..@......n.GO...
0x7ffd654d7f70  0000 0000 0000 0000 4880 4d65 fd7f 0000  ........H.Me....
0x7ffd654d7f80  0000 0000 0100 0000 7307 4000 0000 0000  ........s.@.....
0x7ffd654d7f90  0000 0000 0000 0000 6c11 c9fe 30ef 0355  ........l...0..U
0x7ffd654d7fa0  e005 4000 0000 0000 4080 4d65 fd7f 0000  ..@.....@.Me....
0x7ffd654d7fb0  0000 0000 0000 0000 0000 0000 0000 0000  ................
0x7ffd654d7fc0  6c11 8911 2a25 f9aa 6c11 ef34 4260 9dab  l...*%..l..4B`..
0x7ffd654d7fd0  0000 0000 0000 0000 0000 0000 0000 0000  ................
0x7ffd654d7fe0  0000 0000 0000 0000 0000 0000 0000 0000  ................
0x7ffd654d7ff0  0000 0000 0000 0000 0000 0000 0000 0000  ................
0x7ffd654d8000  0000 0000 0000 0000 0000 0000 0000 0000  ................
```
karena variabel rsi berisi string yang unik dan variabel rdi berisi string yang sama persis seperti inputan kita, sehingga dapat disimpulkan bahwa rsi ini memang berisi string yang digunakan untuk membandingkan inputan kita yang berada pada variabel rdi sehingga kita tinggal menginputkan isi dari variabel rsi ke dalam program crackme5 dan diperoleh hasil berikut
```
root@yeet:/home/aldifp/Downloads# ./crackme5
Enter your input:
OfdlDSA|3tXb32~X3tX@sX`4tXtz
Good game
root@yeet:/home/aldifp/Downloads# 
```
<details>
  <summary>Flag</summary>
  
  ```
  OfdlDSA|3tXb32~X3tX@sX`4tXtz
  ```
</details>