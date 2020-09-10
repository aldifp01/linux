# CRACKME7
### DIKET


### JAWAB
kita coba buka dengan ghidra karena dengan radare2 hanya menampilkan assemblynya saja dan tidak begitu mudah dimengerti, berikut source codenya
```

undefined4 main(void)

{
  int iVar1;
  undefined4 *puVar2;
  byte bVar3;
  undefined4 local_80 [25];
  int local_1c;
  int local_18;
  int local_14;
  undefined *local_10;
  
  bVar3 = 0;
  local_10 = &stack0x00000004;
  while( true ) {
    while( true ) {
      puts("Menu:\n\n[1] Say hello\n[2] Add numbers\n[3] Quit");
      printf("\n[>] ");
      iVar1 = __isoc99_scanf(&DAT_08048814,&local_14);
      if (iVar1 != 1) {
        puts("Unknown input!");
        return 1;
      }
      if (local_14 != 1) break;
      printf("What is your name? ");
      iVar1 = 0x19;
      puVar2 = local_80;
      while (iVar1 != 0) {
        iVar1 = iVar1 + -1;
        *puVar2 = 0;
        puVar2 = puVar2 + (uint)bVar3 * 0x3ffffffe + 1;
      }
      iVar1 = __isoc99_scanf(&DAT_0804883a,local_80);
      if (iVar1 != 1) {
        puts("Unable to read name!");
        return 1;
      }
      printf("Hello, %s!\n",local_80);
    }
    if (local_14 != 2) {
      if (local_14 == 3) {
        puts("Goodbye!");
      }
      else {
        if (local_14 == 0x7a69) {
          puts("Wow such h4x0r!");
          giveFlag();
        }
        else {
          printf("Unknown choice: %d\n",local_14);
        }
      }
      return 0;
    }
    printf("Enter first number: ");
    iVar1 = __isoc99_scanf(&DAT_08048875,&local_18);
    if (iVar1 != 1) break;
    printf("Enter second number: ");
    iVar1 = __isoc99_scanf(&DAT_08048875,&local_1c);
    if (iVar1 != 1) {
      puts("Unable to read number!");
      return 1;
    }
    printf("%d + %d = %d\n",local_18,local_1c,local_18 + local_1c);
  }
  puts("Unable to read number!");
  return 1;
}
```
Terdapat sebuah percabangan yakni yang nantinya akan menampilkan string "Wow such h4x0r!", string tersebut muncul apabila input kita sama dengan 0x7a69 atau dalam desimal sama dengan 31337 sehingga tinggal kita inputkan ke program crackme7 sehingga diperoleh output berikut
```
[1] Say hello
[2] Add numbers
[3] Quit

[>] 1
What is your name? Aldi
Hello, Aldi!
Menu:

[1] Say hello
[2] Add numbers
[3] Quit

[>] 2
Enter first number: 31337
Enter second number: 31337
31337 + 31337 = 62674
Menu:

[1] Say hello
[2] Add numbers
[3] Quit

[>] 
```
Tidak diperoleh output, tetapi apabila dimasukan 31337 tersebut ke fungsi nomor 1 maka diperoleh output berikut sehingga diperoleh flagnya
```
Menu:

[1] Say hello
[2] Add numbers
[3] Quit

[>] 31337            
Wow such h4x0r!
flag{much_reversing_very_ida_wow}
```
<details>
  <summary>Flag</summary>
  
  ```
  flag{much_reversing_very_ida_wow}
  ```
</details>
