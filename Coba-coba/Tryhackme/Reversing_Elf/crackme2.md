# CRACKME 2
### DIKET
Find the super-secret password! and use it to obtain the flag

### JAWAB
Terdapat 2 buah jawaban untuk soal ini, yakni super passwordnya dan flagnya, maka kita coba analisa dengan menggunakan radare2, ketika fungsi main dibuka hasilnya sebagai berikut
```
main (int32_t arg_4h);
|           ; var int32_t var_4h @ ebp-0x4
|           ; arg int32_t arg_4h @ esp+0x4
|           ; DATA XREF from entry0 @ 0x80483b7
|           0x0804849b      8d4c2404       lea ecx, dword [arg_4h]
|           0x0804849f      83e4f0         and esp, 0xfffffff0
|           0x080484a2      ff71fc         push dword [ecx - 4]
|           0x080484a5      55             push ebp
|           0x080484a6      89e5           mov ebp, esp
|           0x080484a8      51             push ecx
|           0x080484a9      83ec04         sub esp, 4
|           0x080484ac      89c8           mov eax, ecx
|           0x080484ae      833802         cmp dword [eax], 2
|       ,=< 0x080484b1      741d           je 0x80484d0
|       |   0x080484b3      8b4004         mov eax, dword [eax + 4]
|       |   0x080484b6      8b00           mov eax, dword [eax]
|       |   0x080484b8      83ec08         sub esp, 8
|       |   0x080484bb      50             push eax
|       |   0x080484bc      6860860408     push str.Usage:__s_password ; 0x8048660 ; "Usage: %s password\n"
|       |   0x080484c1      e88afeffff     call sym.imp.printf
|       |   0x080484c6      83c410         add esp, 0x10
|       |   0x080484c9      b801000000     mov eax, 1
|      ,==< 0x080484ce      eb4e           jmp 0x804851e
|      |`-> 0x080484d0      8b4004         mov eax, dword [eax + 4]
|      |    0x080484d3      83c004         add eax, 4
|      |    0x080484d6      8b00           mov eax, dword [eax]
|      |    0x080484d8      83ec08         sub esp, 8
|      |    0x080484db      6874860408     push str.super_secret_password ; 0x8048674 ; "super_secret_password"
|      |    0x080484e0      50             push eax
|      |    0x080484e1      e85afeffff     call sym.imp.strcmp
|      |    0x080484e6      83c410         add esp, 0x10
|      |    0x080484e9      85c0           test eax, eax
|      |,=< 0x080484eb      7417           je 0x8048504
|      ||   0x080484ed      83ec0c         sub esp, 0xc
|      ||   0x080484f0      688a860408     push str.Access_denied.     ; 0x804868a ; "Access denied."
|      ||   0x080484f5      e866feffff     call sym.imp.puts
|      ||   0x080484fa      83c410         add esp, 0x10
|      ||   0x080484fd      b801000000     mov eax, 1
|     ,===< 0x08048502      eb1a           jmp 0x804851e
|     ||`-> 0x08048504      83ec0c         sub esp, 0xc
|     ||    0x08048507      6899860408     push str.Access_granted.    ; 0x8048699 ; "Access granted."
|     ||    0x0804850c      e84ffeffff     call sym.imp.puts
|     ||    0x08048511      83c410         add esp, 0x10
|     ||    0x08048514      e80d000000     call sym.giveFlag
|     ||    0x08048519      b800000000     mov eax, 0
|     ||    ; CODE XREFS from main @ 0x80484ce, 0x8048502
|     ``--> 0x0804851e      8b4dfc         mov ecx, dword [var_4h]
|           0x08048521      c9             leave
|           0x08048522      8d61fc         lea esp, dword [ecx - 4]
\           0x08048525      c3             ret
```
Terdapat string yang tidak diperoleh ketika crackme2 dijalankan yakni "super_secret_password", jadi ini sebetulnya coba-coba awalnya tapi ternyata berhasil, yaitu dengan menjalankan kode berikut
```
./crackme2 super_secret_password
```
dan diperoleh flag sebagai berikut
```
flag{if_i_submit_this_flag_then_i_will_get_points}
```
<details>
  <summary>Super Secret Password</summary>
  
  ```
  super_secret_password
  ```
  <summary>Flag</summary>
  
  ```
  flag{if_i_submit_this_flag_then_i_will_get_points}
  ```
</details>

