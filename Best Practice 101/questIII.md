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
   menggunakan  semua tools untuk stegano, maka tidak memunculkan flag sama sekali, hal ini karena flag terdapat di dalam string file tersebut sehingga kita tinggal memasukan command berikut

	 strings garden.jpg
	
   nanti akan muncul flag berikut di akhir string nya

   Here is a flag "picoCTF{more_than_m33ts_the_3y3b7FBD20b}"

   maka kita memperoleh flagnya, agar tidak mengeluarkan string lain yang tidak penting kita bisa menggunakan 
	 command grep -i ditambah dengan kalimat pico (karena format flagnya adalah picoCTF) 
	 
	 maka nanti akan memunculkan 1 baris string saja yakni string bagian flagnya yakni
	 
	 "picoCTF{more_than_m33ts_the_3y3b7FBD20b}"
     
     
     












Referensi
forensic
https://trailofbits.github.io/ctf/forensics/
https://bitvijays.github.io/LFC-Forensics.html
https://github.com/apsdehal/awesome-ctf
