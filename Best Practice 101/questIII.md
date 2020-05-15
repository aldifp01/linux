1. Forensic
 - Steganography
 
	-> untuk melihat file dengan menggunakan command file dan exiftool
		 
     -> untuk melihat string yang terkandung dapat menggunakan command strings, untuk lebih akurat dalam pencarian bisa     menambahkan command grep
		 
     -> untuk mencek suatu file mengandung apa saja bisa menggunakan command binwalk
		 
     -> untuk mencari flag pada audio dapat menggunakan tool audacity ataupun software lain seperti wavepad
		 
     -> untuk melihat whitespace dapat menggunakan tool snow
		 
     -> untuk beberapa soal, melihat dengan menggunakan aplikasi manipulasi gambar mungkin cukup untuk melihat flagnya
		 
     -> untuk mencari flag pada gambar dapat menggunakan beberapa tools berikut
        => dengan menggunakan program zsteg, dimana program ini akan menampilkan lsb dan msb (?) pada file yang kita masukan, lalu kita cek pada bagian ini flagnya
        => stegosuite, mirip seperti zsteg namun dalam bentuk aplikasi java
        => untuk menyembunyikan flag pada gambar maupun audio secara simple, dapat menggunakan tool steghide

- File Archive

     -> unzip dapat digunakan untuk mengekstrak file
		 
     -> zipdetails -v akan memberikan informasi detail mengenai archive yang kita buka
		 
     -> zipinfo akan memberikan semua informasi mengenai file zip
		 
     -> zip -F input.zip --out output.zip dan zip -FF input.zip --out output.zip akan memperbaiki file corrupt (tidak tau apakah benar-benar bisa dilakukan)
		 
     -> fcrackzip brute-force digunakan untuk menerka password dengan syarat kurang dari 7 huruf
		 
 - Lainnya
 
     -> untuk melihat packet traffic ataupun melihat file pcapng dapat menggunakan tool wireshark
     
     
 Contoh soal
 
    1. misalnya pada soal unzip di picoCTF, untuk menyelesaikannya kita tinggal memasukan command
       unzip flag.zip	
       maka nanti akan muncul flagnya yakni "unz1pp1ng_1s_3a5y"
       
    2. misalnya untuk soal glory in the garden di picoCTF, ada gambar taman bunga, apabila dicoba langsung dengan 
       menggunakan  semua tools untuk stegano, maka tidak memunculkan flag sama sekali, hal ini karena flag 
       terdapat di dalam string file tersebut sehingga kita tinggal memasukan command berikut
	 strings garden.jpg
       
       
   	nanti akan muncul flag berikut di akhir string nya

	Here is a flag "picoCTF{more_than_m33ts_the_3y3b7FBD20b}"

   	maka kita memperoleh flagnya, agar tidak mengeluarkan string lain yang tidak penting kita bisa menggunakan 
	 command grep -i ditambah dengan kalimat pico (karena format flagnya adalah picoCTF) 
	 
	 maka nanti akan memunculkan 1 baris string saja yakni string bagian flagnya yakni
	 
	 "picoCTF{more_than_m33ts_the_3y3b7FBD20b}"
     
     
     
     
2. Reverse Engineering
   untuk reverse engineering, hal yang dibutuhkan adalah tools untuk decompile file yang sudah tercompile, misalnya untuk 
   program java mungkin beberapa IDE ada yang sudah bisa mendecompile file java sedangkan bahasa lain mungkin membutuhkan
   tool sendiri
   
   untuk java
   	-> untuk program java beberapa IDE bisa langsung mendecompile file class, seperti intellij idea bisa langsung
	   mendecompile file class menjadi java kembali
   
   untuk python
   	-> untuk decompile hasil compile python, kita bisa menggunakan tool uncompyle6 untuk merubahnya kembali menjadi
	   format py
	   
   untuk c++
   	-> untuk c++ mungkin agak sulit, karena nantinya akan berformat ELF, oleh karena itu untuk membuka file ini 
	   dapat menggunakan software IDA yang nantinya akan menampilkan kode assembly dari file ELF tersebut
	   
   Contoh Soal
   
       1. Untuk soal vault-door-training pada picoCTF, nanti kita diberikan file java, kita cukup tinggal membukanya dan berikut
      	adalah source codenya
      
      	import java.util.*;

		class VaultDoorTraining {
 	 		public static void main(String args[]) {
   			 VaultDoorTraining vaultDoor = new VaultDoorTraining();
   			 Scanner scanner = new Scanner(System.in); 
   	 		 System.out.print("Enter vault password: ");
   	 		 String userInput = scanner.next();
   	 		 String input = userInput.substring("picoCTF{".length(),userInput.length()-1);
    
    			if (vaultDoor.checkPassword(input)) {
   			   System.out.println("Access granted.");
    			} else {
    			  System.out.println("Access denied!");
    			}
  			}
  
 		 public boolean checkPassword(String password) {
      			return password.equals("w4rm1ng_Up_w1tH_jAv4_fcb79c48f5b");
  			}
		}

        Untuk ini kita tinggal  menjalankan program ini dan memasukan input yang sama dengan checkPassword, yakni
      
        picoCTF{w4rm1ng_Up_w1tH_jAv4_fcb79c48f5b}
     
        apabila menghasilkan output Access granted maka flag yang kita masukan adalah benar sehingga flag untuk soal ini adalah
     
        picoCTF{w4rm1ng_Up_w1tH_jAv4_fcb79c48f5b}

       2. Untuk soal vault-door-1 pada picoCTF, nanti kita diberikan file java, kita cukup tinggal membukanya dan berikut
      	adalah source codenya
		import java.util.*;

  		class VaultDoor1 {
    		public static void main(String args[]) {
       		 VaultDoor1 vaultDoor = new VaultDoor1();
       		 Scanner scanner = new Scanner(System.in);
       		 System.out.print("Enter vault password: ");
		 String userInput = scanner.next();
		 String input = userInput.substring("picoCTF{".length(),userInput.length()-1);
		 if (vaultDoor.checkPassword(input)) {
	    	 System.out.println("Access granted.");
			} else {
			    System.out.println("Access denied!");
			}
   		 }

    		// I came up with a more secure way to check the password without putting
    		// the password itself in the source code. I think this is going to be
    		// UNHACKABLE!! I hope Dr. Evil agrees...
   		 //
    		// -Minion #8728
    		public boolean checkPassword(String password) {
      		  return password.length() == 32 &&
         		      password.charAt(0)  == 'd' &&
         		      password.charAt(29) == '3' &&
         		      password.charAt(4)  == 'r' &&
         		      password.charAt(2)  == '5' &&
         		      password.charAt(23) == 'r' &&
         		      password.charAt(3)  == 'c' &&
         		      password.charAt(17) == '4' &&
         		      password.charAt(1)  == '3' &&
         		      password.charAt(7)  == 'b' &&
         		      password.charAt(10) == '_' &&
         		      password.charAt(5)  == '4' &&
         		      password.charAt(9)  == '3' &&
         		      password.charAt(11) == 't' &&
         		      password.charAt(15) == 'c' &&
         		      password.charAt(8)  == 'l' &&
         		      password.charAt(12) == 'H' &&
         		      password.charAt(20) == 'c' &&
         		      password.charAt(14) == '_' &&
         		      password.charAt(6)  == 'm' &&
         		      password.charAt(24) == '5' &&
         		      password.charAt(18) == 'r' &&
         		      password.charAt(13) == '3' &&
         		      password.charAt(19) == '4' &&
         		      password.charAt(21) == 'T' &&
        		       password.charAt(16) == 'H' &&
         		      password.charAt(27) == 'd' &&
         		      password.charAt(30) == '8' &&
         		      password.charAt(25) == '_' &&
         		      password.charAt(22) == '3' &&
         		      password.charAt(28) == '0' &&
         		      password.charAt(26) == '9' &&
         		      password.charAt(31) == 'f';
    			}
		}
		maka kita tinggal urutkan saja hurufnya sesuai dengan char 0 - 31 sehingga diperoleh flag berikut
		
		picoCTF{d35cr4mbl3_tH3_cH4r4cT3r5_9d038f}











Referensi
forensic
https://trailofbits.github.io/ctf/forensics/
https://bitvijays.github.io/LFC-Forensics.html
https://github.com/apsdehal/awesome-ctf
