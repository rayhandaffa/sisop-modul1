# Sistem Operasi D-06 (2021)
Praktikum Sistem Operasi Modul 1 - Shell Script, Cron dan AWK 
Kelompok : 
1. Ramadhan Arif - 05111940000162
2. Zulfayanti Sofia Solichin - 05111940000189
3. Rayhan Daffa Alhafish - 05111940000227

## Penjelasan dan Penyelesaian Soal 1
 - **Penjelasan dan Penyelesaian Soal 1a**<br>
 
 - **Penjelasan dan Penyelesaian Soal 1b**<br>
 
 - **Penjelasan dan Penyelesaian Soal 1c**<br>
 
 - **Penjelasan dan Penyelesaian Soal 1d**<br>
 
## Penjelasan dan Penyelesaian Soal 2
Pada soal ini terdapat sebuah file TokoShisop.tsv yang berisi data-data yang dapat kita ambil datanya berdasarkan beberapa kondisi antara lain akan dijelaskan dalam penjelasan soal<br>
 - **Penjelasan dan Penyelesaian Soal 2a**<br> 
   Pada soal 2a terdapat sebuah kondisi dimana kita diminta untuk menampilkan Row ID dan profit persentase sesuai dengan rumus profit yang di sediakan yaitu dengan cara membagi profit dan cost price lalu dikalikan dengan 100, untuk cost proce dapat diperoleh dengan cara mengurangkan sales dan profit. <br>
   ```
   export LC_ALL=C
   awk '
   BEGIN{FS="\t"}
   ```
   Berdasarkan syntax diatas terdapat sebuah `export LC_ALL_LC=C` yang digunakan untuk memberi tahu mesin membaca tanda baca titik (.) jadi tanda baca (,). dan `{FS="\t"}` dapat diartikan untuk memberitahu bahwa *Field Separator*-nya adalah tab. <br>
   
   Hal pertama yang perlu lakukan adalah dengan menghitung nilai profit persentase sesuai rumus yang disediakan. Perhitungan dapat dilakukan dengan cara memasukkan value yang ada di dalam kolom. Kolom profit berada di posisi kolom 21 oleh karena itu kita dapat menulisnya dengan `$21` dan kolom sales berada di posisi kolom 18 (`$18`). Sesuai dengan rumus `Profit Percentage = (Profit / Cost Price) *100 ` maka dapat ditulis dalam terminal ubuntu seperti `persentaseprofit=$21/($18-$21)*100`. Lalu, setelah mendapatkan hasil dari perhitungan dapat melakukan perbandingan dengan if dan membuat variable baru bernama "maks" yang berguna untuk menyimpan nilai percent terbesar. Berikut syntax yang dapat dilihat di bawah ini: <br> 
   
   ```
   { 
    if (maks<=persentaseprofit)
      {maks=presentasiprofit;barisID=$ID}
   }
   ```
   Sesuai syntax diatas dapat diartikan apabila kondisi value percent terbesar lebih kecil dibanding value persentaseprofit (Percentage Profit) maka, value yang menyimpan nilai perhitungan persentaseprofit akan disimpan di dalam sebuah variable "maks" lalu akan menyimpan IDnya. lalu pada bagian `END { }' /home/rayhandaffa/Downloads/Laporan-TokoShisop.tsv`akan memprintf-kan hasil perhitungan dengan persentase maksimalnya. Serta `Laporan-TokoShisop.tsv` merupakan nama file yang akan menjadi input pada soal ini.<br>
   
- **Penjelasan dan Penyelesaian Soal 2b**<br>
  Pada soal 2b ini terdapat sebuah kondisi dimana kita diminta untuk menampilkan nama customer yang melakukan transaksi pada tahun 2017 di Albuquerque. Untuk mendapatkan `nama customer` dapat dilihat syntax nya di bawah ini : 
  ```
  {
    if($2~"2017" && $10=="Albuquerque")
     {listCustomer[$7]++}
  }
  ```
  Berdasarkan potongan *coding*an, pada soal 2b menggunakan *`if`(condition)* untuk memeriksa dan menemukan data-data dari tabel data `Laporan-TokoShisop.tsv`. Untuk `$2~"2017"` artinya pada tabel data tersebut ada sebuah kolom bernama `Order ID` dan berisi tanggal dimana order itu dibuat dan pada soal ini hanya menampilkan data-data pada tahun 2017. Selanjutnya, untuk `$10=="Albuquerque"` dimana artinya terdapat sebuat kolom `City` dan hanya menampilkan kota bernama Albuquerque. Lalu, ketika `nama customer` yang sesuai dengan ketentuan udah di dapatkan lalu nama-nama tesebut akan simpan di sebuah array bernama `listCustomer{$7}++` dimana `$7` ini merupakan sebuah kolom bernama `Customer Name` dan terdapat sebuah iterasi digunakan untuk menampilkan semua nama pada array sesuai format atau ketentuan. <br>
  
- **Penjelasan dan Penyelesaian Soal 2c**<br>
   Pada kondisi soal 2c kita diminta untuk menampilkan data dengan ketentuan segment dengan jumlah transaksi paling sedikit. Cara pertama untuk dapat menyelesaikannya yaitu pertama menghitung jumlah transaksi pada masing-masing segment customer. 
   ```
       {
          if(NR>1)
           {
             listSeg[$8]++
           }
       }
   ```
   `NR>1` dapat dijelaskan sebuah *number of records* atau dapat diartikan baris keberapa pada tabel file `Laporan-TokoShisop.tsv` tersebut, menggunakan `NR>1` agar dapat dimulainya pembacaan baris dimulai pada baris ke-2. Dan menggunakan sebuah array `listSeg[$8]++` guna untuk menghitung jumlah transaksi pada tabel Segment atau `$8` dan array tersebut berfungsi untuk menjadi index dan counter transaksi sebagi value-nya. Kemudian, setelah didapatkan jumlah transaksi tiap segmentnya maka selanjutnya kita menggunakan potongan codingan di bawah ini guna untuk mencari segment yang memiliki jumlah transaksi paling kecil
   
  ```
  {
     minPenjualan=5000
     for(segment in listSeg)
     {
       if(listSeg[segment] < minPenjualan)
       {
         minPenjualan = listSeg[segment]
         segmentMinimal = segment
       }
     }
      printf ("\nTipe segmen customer yang penjualannya paling sedikit adalah %s dengan %.1f transaksi\n", segment, minPenjualan);
  }
  ```
     Jika jumlah transaksi dari suatu segment lebih kecil dibandingkan transaksi yang disimpan (`minPenjualan`) maka jumlah transaksi (`listSeg[segment]`) dan index (`segment`) akan disimpan dalam variabel `segment` dan `minPenjualan`. Kemudian, hasilnya akan di cetak sesuai format.<br>
     
- **Penjelasan dan Penyelesaian Soal 2d**<br>
 Pada soal 2d hampir sama dengan 2c tetapi terdapat beberapa perbedaan yang mencolok yaitu dimana pada soal 2d diminta untuk menampilkan wilayah bagian yang memiliki total keuntungan (profit) yang paling sedikit. Sama seperti dengan di 2c hal yang paling utama adalah menghitung profit di masing-masing region. 
  ```
     {
       if(NR!=1)
        {
          listGabungan[$13]+=$21
        }
 
     }
  ```
   Terdapat sebuah array `listGabungan` dengan index = kolom `region` yang berada di kolom 13 (`$13`). Akumulasi keuntungan masing-masing region dihitung dengan menggunakan `listGabungan[$13]+=$21` yang dimana `$21` merupakan sebuah kolom yang merujuk `Profit`.
   
  ```
      {
         profitMinimun=5000
         for(region in listGabungan)
         {
          if(listGabungan[region] < profitMinimum)
              {
                 listGabungan[region] = profitMinimum
                 regionMinimum = region
               }
          }
          printf ("\nWilayah bagian (region) yang memiliki total keuntungan (profit) yang paling    sedikit adalah  %s dengan total %.1f\n", region, profitMinimum);
       }
   ```
   Potongan program ini dijalankan guna untuk menge-*check* dan mencari jumlah profit atau keuntungan di masing-masing wilayah(region). Jika total keuntungan dari suatu region lebih kecil dibandingkan nilai yang disimpan maka akan tercetak sebuah index bernama `region` dan sebuah total keuntungan yang paling kecil bernama `profitMinimum`.
 
- **Penjelasan dan Penyelesaian Soal 2e**<br>
   Pada soal 2e meminta kita untuk membuat script hasil dari soal 2a, 2b, 2c, dan 2d yang disimpan ke `hasil.txt`. Dapat dilihat seperti dibawah ini: <br>

   ![ssshift1](https://github.com/rayhandaffa/soal-shift-sisop-modul-1-D06-2021/blob/main/ss%20shift1/hasil%2Ctxt.jpg)<br>
   
     Di akhir setiap program pada nomer 2a, 2b, 2c, maupun 2d terdapat sebuah syntax `Laporan-TokoShisop.tsv >> hasil.txt` output semua soal 2 akan ditampilkan pada file `hasil.txt` dengan melakukan redirection untuk mengirim oitput ke file `hasil.txt`. 
## Penjelasan dan Penyelesaian Soal 3
- **Penjelasan dan Penyelesaian Soal 3a**<br>
  Pada program ini, pertama-tama, dibuat dua variabel yang menyatakan jumlah download maksimum dan nomor gambar. Berikutnya dilakukan iterasi selama belum mencapai banyak download maksimum dan selama gambar kurang dari 23.
  ```
  for((i=1;i<=count && image<=23;i=i+1))
  do
  ```
  Untuk mendownload file gambar pada link tersebut, digunakan command `wget`, kemudian log hasil gambar tadi diatur sedemikian agar disimpan dalam file Foto.log, serta beri nama file gambar tersebut dengan newKitten.
  ```
  wget "https://loremflickr.com/320/240/kitten" -a Foto.log -O newKitten
  ```
  Sejak iterasi kedua, file gambar yang di-download dibandingkan dengan file gambar pertama menggunakan perintah `cmp`. Perintah ini memungkinkan untuk membandingkan dua file dari jenis apa pun dan menulis hasilnya ke output standar.
  ```
  reduplicate=`cmp $prevKitten newKitten -b`
  ```
  Jika setelah dicek ternyata ada duplikasi, maka file gambar newKitten yang sudah di-download akan dihapus menggunakan perintah rm. Namun jika tidak, maka file newKitten akan diganti namanya dan disimpan di folder.
  ```
  if [ $duplicate -eq 1 ]
  then
      rm newKitten
  else
      mv newKitten `printf "Koleksi_%02d" "$image"`
      image=$((image+1))
  fi
  ```
  Program ini dijalankan berulang kali hingga total 23 gambar telah diperoleh dan ketika jumlah download maksimum telah tercapai.
 
- **Penjelasan dan Penyelesaian Soal 3b**<br>

- **Penjelasan dan Penyelesaian Soal 3c**<br>

- **Penjelasan dan Penyelesaian Soal 3d**<br>
