# Membuat Filter Instagram dengan Meta Spark

Kita akan membuat filter dimana kita nanti bisa memilih pilihan (makanan yang kita suka) kiri dan kanan dengan cara menyandarkan kepala kita ke kiri dan ke kanan.  
[Video Result](https://www.loom.com/share/8634791ed93e434cbbff5b1c7e8f09f9)
[Link Project](https://drive.google.com/file/d/1XFmWwOBThlkdSfwZVGtmpfTuP40npZ_c/view?usp=sharing)

## Berikut step by step pembuatannya

---

1. Download dan jalankan Meta Spark Studio.  
[Download](https://spark.meta.com/download/)

2. Create New kemudian Blank Project.
![](create-new.png)

3. Tampil IDE Meta Spark.
![](meta-spark.png)

4. Simpan dulu project kita.
![](save-project.png)

5. Siapkan asset gambarnya untuk permainan kita. Disini saya siapkan 3 gambar untuk pilihan kiri, dan 3 gambar untuk pilihan kanan.

|kiri1.png|kiri2.png|kiri3.png|kanan1.png|kanan2.png|kanan3.png|
|---|---|---|---|---|---|
|![](kiri1.png)|![](kiri2.png)|![](kiri3.png)|![](kanan1.png)|![](kanan2.png)|![](kanan3.png)|

6. Buat `animation sequence` untuk pilihan kiri dan juga kanan.
![](animation-seq.png)
Kemudian masukkan namanya `Kiri`.
![](kiri.png)
Di window property dari `Kiri`, kita pilih `Texture -- Choose File`, kemudian pilih ketiga png kiri kita dari 1-3.
![](animation-choose.png)
Kemudian nanti akan tercipta Texture `kiri[1-3]`
![](animation-kiri.png)
Ulangi prosesnya untuk `animation sequence` yang `Kanan`, sampai jadi kurang lebih seperti di bawah.
![](animation-kanan.png)

7. Buat `material` untuk pilihan kiri dan juga kanan.
![](material-buat.png)
Beri nama `Kiri`.
![](material-kiri.png)
Di property material kiri, kita set `Shader Type` jadi `Flat` dan pilih `Texture` nya ke animation sequence Kiri.
![](material-shader.png)
Lakukan hal yang sama untuk material `Kanan`, sampai kurang lebih jadi seperti di bawah.
![](material-kanan.png)

8. Buat `Null Object` sebagai penampung di Scene, dengan cara `Add Object`.
![](null-object.png)
Buat dua buah `Plane` object.
![](add-plane.png)
![](dua-plane.png)
Rename kedua plane.
![](rename-plane.png)  
Rename nullObject0 jadi Kartu.
![](rename-null.png)
Dan pindahkan plane Kiri dan Kanan ke dalam Kartu.
![](kartu-kiri.png)
Nanti di simulasi akan muncul planenya (dalam kotak bersemut).
![](plane-semut.png)  
Kemudian kita perlu atur posisi dari plane Kiri dan Kanan agar tidak menumpuk di tengah.
Untuk plane `Kiri` kita beri `-0,06` dan `0,1` di 2 axis pertama `Position`.
![](kiri-position.png)
Untuk plane `Kanan` kita beri `0,06` dan `0,1` di 2 axis pertama `Position`.
![](kanan-position.png)
Maka simulasi akan seperti ini.  
![](simulasi-plane.png)  
Tinggal kita kasih materialnya kepada plane Kiri dan juga Kanan.
![](plane-kiri-mat.png)
![](plane-kanan-mat.png)
Nanti di simulasi, animasinya tidak akan berhenti (loop), mengulang seluruh aset gambar kita.  
![](simulasi-plane-ok.png)  
Agar berhenti, kita pilih kedua `animation sequence` kita, kemudian di property `Current Frame`, kita klik, nanti kedua current frame Kiri dan Kanan akan masuk ke `Patch Editor`.
![](animation-stop.png)

9. Berikutnya kita siapkan `Face Tracker`, add new object face tracker di Scene.
![](add-facetracker.png)
Nanti akan tercipta faceTracker0.
![](facetracker-tercipta.png)
Kemudian drag faceTracker0 ke `Patch Editor`, nanti akan tercipta kurang lebih seperti di bawah.
![](face-patcheditor.png)
Kemudian kita perlu add patch untuk handle event `face lean`, yaitu `Head Rotation`.
![](head-rotation.png)
Maka akan tercipta patch head rotation.
![](head-rotation-tercipta.png)
Disini kita perlu sambungkan kiri head rotation kepada face tracker.
![](face-ke-head.png)
Kemudian kita misalnya ingin memberikan efek zoom kepada pilihan kiri pada saat kita nyender ke kiri, begitupun dengan kasus kanan. 

Berikut untuk yang kiri, dimana kita perlu nambah patch `If Then Else`, mengganti menjadi `vector 3` dan beri `1,2` di setiap axis thennya dan `1` di setiap axis elsenya.

Kemudian di Scene pilih plane Kiri, di property `Scale` nya perlu kita klik juga agar muncul di `Plane Editor`.

Kemudian perlu kita sambungkan dari `Left Lean State` nya face, kepada If nya kita, yang kemudian If nya ke scale property Kiri.
![](lean-kiri.png)

Lakukan hal yang sama dengan `Right Lean State` nya face.
![](lean-kanan.png)

Nanti di simulasi akan terlihat, pas nyender, dia akan membesar kotaknya.
![](plane-membesar.png)  

10. Berikutnya kita perlu handle untuk pertanyaan berikutnya, dimana apabila kita sudah memilih baik kiri ataupun kanan, kita mesti pindah ke soal berikutnya.

Kita perlu buat `OR` dan `Counter` di Plane Editor.

Kita sambungkan input OR dari Left dan Right Lean nya face, dan output OR kepada `Increase` counter.
![](face-or.png)

Karena kita hanya ada 3 set soal, maka `Maximum Count` counter mesti kita stel jadi 3, kemudian kita perlu ambil property `Current Frame` dari animation (yang tadi sempat kita klik biar berhenti loop animasinya), dan sambungkan 
![](face-max.png)

Selesai! Kita bisa lihat hasilnya di video di bawah yaa.
https://www.loom.com/share/8634791ed93e434cbbff5b1c7e8f09f9

Maka sekarang, setelah kita nyender, pertanyaan akan berubah. Untuk tutorial kali ini, belum ada end-game yang akan terjadi, dia akan terus-terusan berputar di ketiga pertanyaan yang kita punya. 

Semoga bermanfaat. Sampai ketemu di tutorial berikutnya.