# CRACKME 8
### DIKET
Analyze the binary and obtain the flag

### JAWAB
Mirip dengan crackme7, kita tinggal buka programnya dengan ghidra, diperoleh source code berikut
```
undefined4 main(int param_1,undefined4 *param_2)

{
  undefined4 uVar1;
  int iVar2;
  
  if (param_1 == 2) {
    iVar2 = atoi((char *)param_2[1]);
    if (iVar2 == -0x35010ff3) {
      puts("Access granted.");
      giveFlag();
      uVar1 = 0;
    }
    else {
      puts("Access denied.");
      uVar1 = 1;
    }
  }
  else {
    printf("Usage: %s password\n",*param_2);
    uVar1 = 1;
  }
  return uVar1;
}
```
Dan juga sama seperti pada crackme7, terdapat percabangan yang menyaratkan agar menginputkan -0x35010ff3 atau sama dengan -889262067 untuk menampilkan method giveFlag() sehingga kita tinggal input -889262067 ke program crackme8 sehingga diperoleh flag
```
root@yeet:/home/aldifp/Downloads# ./crackme8 -889262067
Access granted.
flag{at_least_this_cafe_wont_leak_your_credit_card_numbers}
```
<details>
  <summary>Flag</summary>
  
  ```
  flag{at_least_this_cafe_wont_leak_your_credit_card_numbers}
  ```
</details>
