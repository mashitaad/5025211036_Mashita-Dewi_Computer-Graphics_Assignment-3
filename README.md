# Assignment 3
Tugas 3 Grafika Komputer A

## Soal 1
> Telah diberikan file RGB Triangle in WEBGL.html lalu ubahlah RGB Triangle tersebut menjadi RGB Square!

### Solusi Soal 1

```ruby
function draw() { 

    gl.clearColor(0,0,0,1);  // specify the color to be used for clearing
    gl.clear(gl.COLOR_BUFFER_BIT);  // clear the canvas (to black)

    /* Set up values for the "coords" attribute */

    let  coords = new Float32Array( [ -0.5,-0.5, 0.5,0.5, -0.5,0.5 ] );
   
    gl.bindBuffer(gl.ARRAY_BUFFER, bufferCoords);
    gl.bufferData(gl.ARRAY_BUFFER, coords, gl.STREAM_DRAW);
    gl.vertexAttribPointer(attributeCoords, 2, gl.FLOAT, false, 0, 0);
    gl.enableVertexAttribArray(attributeCoords); 
   
    /* Set up values for the "color" attribute */
   
    let  color = new Float32Array( [ 0,1,0, 1,0,0, 0,0,1 ] );

    gl.bindBuffer(gl.ARRAY_BUFFER, bufferColor);
    gl.bufferData(gl.ARRAY_BUFFER, color, gl.STREAM_DRAW);
    gl.vertexAttribPointer(attributeColor, 3, gl.FLOAT, false, 0, 0);
    gl.enableVertexAttribArray(attributeColor); 
    
    /* Draw the triangle. */
   
    gl.drawArrays(gl.TRIANGLES, 0, 3);

    let coords_2 = new Float32Array([-0.5,-0.5, 0.5,0.5, 0.5,-0.5]);

    gl.bindBuffer(gl.ARRAY_BUFFER, bufferCoords);
    gl.bufferData(gl.ARRAY_BUFFER, coords_2, gl.STREAM_DRAW);

    let color_2 = new Float32Array([0,1,0, 1,0,0, 1,1,1]);

    gl.bindBuffer(gl.ARRAY_BUFFER, bufferColor);
    gl.bufferData(gl.ARRAY_BUFFER, color_2, gl.STREAM_DRAW);

    /* Draw the second triangle. */
    gl.drawArrays(gl.TRIANGLES, 0, 3);
}
```
1. Inisialisasi dan Pengaturan Awal
```ruby
gl.clearColor(0, 0, 0, 1);
gl.clear(gl.COLOR_BUFFER_BIT);
```
Mengatur warna latar belakang canvas menjadi hitam.

2. Menyiapkan Data Koordinat
```ruby
gl.bindBuffer(gl.ARRAY_BUFFER, bufferCoords);
gl.bufferData(gl.ARRAY_BUFFER, coords, gl.STREAM_DRAW);	
```
Membuat array Float32 yang berisi koordinat vertex untuk segitiga.

3. Mengirim Data Koordinat ke GPU
```ruby
gl.bindBuffer(gl.ARRAY_BUFFER, bufferCoords);
gl.bufferData(gl.ARRAY_BUFFER, coords, gl.STREAM_DRAW);
```
Mengikat dan mengirim data koordinat ke buffer di GPU.

4. Menyiapkan Data Warna
```ruby
let color = new Float32Array([0, 1, 0, 1, 0, 0, 0, 0, 1]);
```
Membuat array Float32 yang berisi data warna untuk setiap vertex.

5. Mengirim Data Warna ke GPU.
```ruby
gl.bindBuffer(gl.ARRAY_BUFFER, bufferColor);
gl.bufferData(gl.ARRAY_BUFFER, color, gl.STREAM_DRAW);
```
Mengikat dan mengirim data koordinat ke buffer di GPU.

6. Menggambar Segitiga Pertama
```ruby
gl.drawArrays(gl.TRIANGLES, 0, 3);
```
Menggambar segitiga pertama menggunakan data koordinat dan warna yang telah 	disiapkan.

7. Menyiapkan Data Koordinat dan Warna untuk Segitiga Kedua
```ruby	
let coords_2 = new Float32Array([-0.5, -0.5, 0.5, 0.5, 0.5, -0.5]);
let color_2 = new Float32Array([0, 1, 0, 1, 0, 0, 1, 1, 1]);
```
Membuat array baru untuk koordinat dan warna segitiga kedua
	
8. Mengirim Data Koordinat dan Warna Segitiga Kedua ke GPU
```ruby	
gl.bindBuffer(gl.ARRAY_BUFFER, bufferCoords);
gl.bufferData(gl.ARRAY_BUFFER, coords_2, gl.STREAM_DRAW);

gl.bindBuffer(gl.ARRAY_BUFFER, bufferColor);
gl.bufferData(gl.ARRAY_BUFFER, color_2, gl.STREAM_DRAW);
```	
Mengikat dan mengirim data koordinat dan warna segitiga kedua ke buffer di GPU.
	
9. Menggambar Segitiga Kedua
```ruby	
gl.drawArrays(gl.TRIANGLES, 0, 3);	
```
Menggambar segitiga kedua menggunakan data koordinat dan warna yang telah disiapkan.

<img width="424" alt="Persegi" src="https://github.com/mashitaad/5025211036_Mashita-Dewi_Computer-Graphics_Assignment-3/assets/87978863/0ee0af0e-119e-46c8-ae02-bbc21d8a741a">

## Soal 2
> Diberikan file contoh1.html yang merupakan gambar kubus yang dibuat dengan WebGL dan glMatrix, coba ubahlah kubus 2D tersebut menjadi 3D!.

### Solusi Soal 2

```ruby
function draw() { 
    gl.clearColor(0,0,0,1);
    gl.clear(gl.COLOR_BUFFER_BIT | gl.DEPTH_BUFFER_BIT);
    
    /* Draw the six faces of a cube, with different colors. */
    
    drawPrimitive(gl.TRIANGLE_FAN, [0.133, 0.611, 0.565, 1], [-0.5, -0.4, -0.5, -0.5, 0.4, -0.5, 0.3, 0.4, -0.5, 0.3, -0.4, -0.5]);  
    drawPrimitive(gl.TRIANGLE_FAN, [0.913, 0.721, 0.141, 1], [-0.3, -0.2, 0.5, 0.5, -0.2, 0.5, 0.5, 0.6, 0.5, -0.3, 0.6, 0.5]); 
    drawPrimitive(gl.TRIANGLE_FAN, [0.917, 0.722, 0.133, 1], [-0.3, 0.6, -0.5, -0.5, 0.4, 0.5, 0.3, 0.4, 0.5, 0.5, 0.6, -0.5]);
    drawPrimitive(gl.TRIANGLE_FAN, [0.596, 0.498, 0.133, 1], [-0.3, -0.2, -0.5, 0.5, -0.2, -0.5, 0.3, -0.4, 0.5, -0.5, -0.4, 0.5]);  
    drawPrimitive(gl.TRIANGLE_FAN, [0.929, 0.576, 0.133, 1], [0.5, -0.2, -0.5, 0.5, 0.6, -0.5, 0.3, 0.4, 0.5, 0.3, -0.4, 0.5]);
    drawPrimitive(gl.TRIANGLE_FAN, [0.596, 0.498, 0.596, 1], [-0.3, -0.2, -0.5, -0.5, -0.4, 0.5, -0.5, 0.4, 0.5, -0.3, 0.6, -0.5]);  
}
```
1. Inisialisasi dan Pengaturan Awal
```ruby	
gl.clearColor(0,0,0,1);
gl.clear(gl.COLOR_BUFFER_BIT | gl.DEPTH_BUFFER_BIT);
```
Mengatur warna latar belakang canvas dan membersihkan buffer warna dan buffer 	kedalaman.

2. Menggambar Enam Wajah Kubus dengan Warna Berbeda
```ruby
drawPrimitive(gl.TRIANGLE_FAN, [0.133, 0.611, 0.565, 1], [-0.5, -0.4, -0.5, -0.5, 0.4, -0.5, 0.3, 0.4, -0.5, 0.3, -0.4, -0.5]);  
drawPrimitive(gl.TRIANGLE_FAN, [0.913, 0.721, 0.141, 1], [-0.3, -0.2, 0.5, 0.5, -0.2, 0.5, 0.5, 0.6, 0.5, -0.3, 0.6, 0.5]); 
drawPrimitive(gl.TRIANGLE_FAN, [0.917, 0.722, 0.133, 1], [-0.3, 0.6, -0.5, -0.5, 0.4, 0.5, 0.3, 0.4, 0.5, 0.5, 0.6, -0.5]);  
drawPrimitive(gl.TRIANGLE_FAN, [0.596, 0.498, 0.133, 1], [-0.3, -0.2, -0.5, 0.5, -0.2, -0.5, 0.3, -0.4, 0.5, -0.5, -0.4, 0.5]);  
drawPrimitive(gl.TRIANGLE_FAN, [0.929, 0.576, 0.133, 1], [0.5, -0.2, -0.5, 0.5, 0.6, -0.5, 0.3, 0.4, 0.5, 0.3, -0.4, 0.5]);  
drawPrimitive(gl.TRIANGLE_FAN, [0.596, 0.498, 0.596, 1], [-0.3, -0.2, -0.5, -0.5, -0.4, 0.5, -0.5, 0.4, 0.5, -0.3, 0.6, -0.5]);  
```
- Setiap baris memanggil fungsi drawPrimitive untuk menggambar satu wajah kubus.
- Argumen pertama (gl.TRIANGLE_FAN) adalah mode penggambaran yang digunakan.
- Argumen kedua adalah array RGBA yang menentukan warna wajah kubus.
- Argumen ketiga adalah array koordinat vertex untuk membentuk wajah kubus tersebut.	
- Warna yang digunakan diubah dari nilai heksadesimal ke nilai 	desimal antara 0 dan 1 agar sesuai dengan format yang diterima oleh WebGL.

<img width="424" alt="Kubus" src="https://github.com/mashitaad/5025211036_Mashita-Dewi_Computer-Graphics_Assignment-3/assets/87978863/abf05aa3-10a4-4a7c-8610-f4816cac595b">

### Memperlihatkan Segala Sisi Kubus
1. Sisi Depan
```ruby
function draw() { 
    gl.clearColor(0,0,0,1);
    gl.clear(gl.COLOR_BUFFER_BIT | gl.DEPTH_BUFFER_BIT);
    
    /* Draw the six faces of a cube, with different colors. */
    
    drawPrimitive(gl.TRIANGLE_FAN, [0.133, 0.611, 0.565, 1], [-0.5, -0.4, -0.5, -0.5, 0.4, -0.5, 0.3, 0.4, -0.5, 0.3, -0.4, -0.5]);  
    // drawPrimitive(gl.TRIANGLE_FAN, [0.913, 0.721, 0.141, 1], [-0.3, -0.2, 0.5, 0.5, -0.2, 0.5, 0.5, 0.6, 0.5, -0.3, 0.6, 0.5]); 
    // drawPrimitive(gl.TRIANGLE_FAN, [0.917, 0.722, 0.133, 1], [-0.3, 0.6, -0.5, -0.5, 0.4, 0.5, 0.3, 0.4, 0.5, 0.5, 0.6, -0.5]);
    // drawPrimitive(gl.TRIANGLE_FAN, [0.596, 0.498, 0.133, 1], [-0.3, -0.2, -0.5, 0.5, -0.2, -0.5, 0.3, -0.4, 0.5, -0.5, -0.4, 0.5]);  
    // drawPrimitive(gl.TRIANGLE_FAN, [0.929, 0.576, 0.133, 1], [0.5, -0.2, -0.5, 0.5, 0.6, -0.5, 0.3, 0.4, 0.5, 0.3, -0.4, 0.5]);
    // drawPrimitive(gl.TRIANGLE_FAN, [0.596, 0.498, 0.596, 1], [-0.3, -0.2, -0.5, -0.5, -0.4, 0.5, -0.5, 0.4, 0.5, -0.3, 0.6, -0.5]);  

}
```
Saat ini, hanya sisi depan yang diaktifkan untuk digambar `drawPrimitive(gl.TRIANGLE_FAN, [0.133, 0.611, 0.565, 1], [-0.5, -0.4, -0.5, -0.5, 0.4, -0.5, 0.3, 0.4, -0.5, 0.3, -0.4, -0.5]);`. Anda dapat mengaktifkan sisi lainnya (menghilangkan komentar pada panggilan drawPrimitive yang lain) untuk menggambar keseluruhan kubus dengan warna-warna yang berbeda pada setiap sisinya.

<img width="432" alt="Kubus Sisi Depan" src="https://github.com/mashitaad/5025211036_Mashita-Dewi_Computer-Graphics_Assignment-3/assets/87978863/360affee-8cf3-4e82-9aa0-f0a93c80ae94">

2. Sisi Belakang
```ruby
function draw() { 
    gl.clearColor(0,0,0,1);
    gl.clear(gl.COLOR_BUFFER_BIT | gl.DEPTH_BUFFER_BIT);
    
    /* Draw the six faces of a cube, with different colors. */
    
    // drawPrimitive(gl.TRIANGLE_FAN, [0.133, 0.611, 0.565, 1], [-0.5, -0.4, -0.5, -0.5, 0.4, -0.5, 0.3, 0.4, -0.5, 0.3, -0.4, -0.5]);  
	drawPrimitive(gl.TRIANGLE_FAN, [0.913, 0.721, 0.141, 1], [-0.3, -0.2, 0.5, 0.5, -0.2, 0.5, 0.5, 0.6, 0.5, -0.3, 0.6, 0.5]); 
    // drawPrimitive(gl.TRIANGLE_FAN, [0.917, 0.722, 0.133, 1], [-0.3, 0.6, -0.5, -0.5, 0.4, 0.5, 0.3, 0.4, 0.5, 0.5, 0.6, -0.5]);
    // drawPrimitive(gl.TRIANGLE_FAN, [0.596, 0.498, 0.133, 1], [-0.3, -0.2, -0.5, 0.5, -0.2, -0.5, 0.3, -0.4, 0.5, -0.5, -0.4, 0.5]);  
    // drawPrimitive(gl.TRIANGLE_FAN, [0.929, 0.576, 0.133, 1], [0.5, -0.2, -0.5, 0.5, 0.6, -0.5, 0.3, 0.4, 0.5, 0.3, -0.4, 0.5]);
    // drawPrimitive(gl.TRIANGLE_FAN, [0.596, 0.498, 0.596, 1], [-0.3, -0.2, -0.5, -0.5, -0.4, 0.5, -0.5, 0.4, 0.5, -0.3, 0.6, -0.5]);  

}
```
Saat ini, hanya sisi belakang yang diaktifkan untuk digambar `drawPrimitive(gl.TRIANGLE_FAN, [0.913, 0.721, 0.141, 1], [-0.3, -0.2, 0.5, 0.5, -0.2, 0.5, 0.5, 0.6, 0.5, -0.3, 0.6, 0.5]);`. Anda dapat mengaktifkan sisi lainnya (menghilangkan komentar pada panggilan drawPrimitive yang lain) untuk menggambar keseluruhan kubus dengan warna-warna yang berbeda pada setiap sisinya.

<img width="430" alt="Kubus Sisi Belakang" src="https://github.com/mashitaad/5025211036_Mashita-Dewi_Computer-Graphics_Assignment-3/assets/87978863/c10ccebd-8a21-43d6-8eca-0c3c79279bfd">

3. Sisi Atas
```ruby
function draw() { 
    gl.clearColor(0,0,0,1);
    gl.clear(gl.COLOR_BUFFER_BIT | gl.DEPTH_BUFFER_BIT);
    
    /* Draw the six faces of a cube, with different colors. */
    
    // drawPrimitive(gl.TRIANGLE_FAN, [0.133, 0.611, 0.565, 1], [-0.5, -0.4, -0.5, -0.5, 0.4, -0.5, 0.3, 0.4, -0.5, 0.3, -0.4, -0.5]);  
    // drawPrimitive(gl.TRIANGLE_FAN, [0.913, 0.721, 0.141, 1], [-0.3, -0.2, 0.5, 0.5, -0.2, 0.5, 0.5, 0.6, 0.5, -0.3, 0.6, 0.5]); 
	drawPrimitive(gl.TRIANGLE_FAN, [0.917, 0.722, 0.133, 1], [-0.3, 0.6, -0.5, -0.5, 0.4, 0.5, 0.3, 0.4, 0.5, 0.5, 0.6, -0.5]);
    // drawPrimitive(gl.TRIANGLE_FAN, [0.596, 0.498, 0.133, 1], [-0.3, -0.2, -0.5, 0.5, -0.2, -0.5, 0.3, -0.4, 0.5, -0.5, -0.4, 0.5]);  
    // drawPrimitive(gl.TRIANGLE_FAN, [0.929, 0.576, 0.133, 1], [0.5, -0.2, -0.5, 0.5, 0.6, -0.5, 0.3, 0.4, 0.5, 0.3, -0.4, 0.5]);
    // drawPrimitive(gl.TRIANGLE_FAN, [0.596, 0.498, 0.596, 1], [-0.3, -0.2, -0.5, -0.5, -0.4, 0.5, -0.5, 0.4, 0.5, -0.3, 0.6, -0.5]);  

}
```
Saat ini, hanya sisi atas yang diaktifkan untuk digambar `drawPrimitive(gl.TRIANGLE_FAN, [0.917, 0.722, 0.133, 1], [-0.3, 0.6, -0.5, -0.5, 0.4, 0.5, 0.3, 0.4, 0.5, 0.5, 0.6, -0.5]);`. Anda dapat mengaktifkan sisi lainnya (menghilangkan komentar pada panggilan drawPrimitive yang lain) untuk menggambar keseluruhan kubus dengan warna-warna yang berbeda pada setiap sisinya.

<img width="437" alt="Kubus Sisi Atas" src="https://github.com/mashitaad/5025211036_Mashita-Dewi_Computer-Graphics_Assignment-3/assets/87978863/edef307c-c7ac-487d-8c19-4f43bf0de594">

4. Sisi Bawah
```ruby
function draw() { 
    gl.clearColor(0,0,0,1);
    gl.clear(gl.COLOR_BUFFER_BIT | gl.DEPTH_BUFFER_BIT);
    
    /* Draw the six faces of a cube, with different colors. */
    
    // drawPrimitive(gl.TRIANGLE_FAN, [0.133, 0.611, 0.565, 1], [-0.5, -0.4, -0.5, -0.5, 0.4, -0.5, 0.3, 0.4, -0.5, 0.3, -0.4, -0.5]);  
    // drawPrimitive(gl.TRIANGLE_FAN, [0.913, 0.721, 0.141, 1], [-0.3, -0.2, 0.5, 0.5, -0.2, 0.5, 0.5, 0.6, 0.5, -0.3, 0.6, 0.5]); 
    // drawPrimitive(gl.TRIANGLE_FAN, [0.917, 0.722, 0.133, 1], [-0.3, 0.6, -0.5, -0.5, 0.4, 0.5, 0.3, 0.4, 0.5, 0.5, 0.6, -0.5]);
    	drawPrimitive(gl.TRIANGLE_FAN, [0.596, 0.498, 0.133, 1], [-0.3, -0.2, -0.5, 0.5, -0.2, -0.5, 0.3, -0.4, 0.5, -0.5, -0.4, 0.5]);  
    // drawPrimitive(gl.TRIANGLE_FAN, [0.929, 0.576, 0.133, 1], [0.5, -0.2, -0.5, 0.5, 0.6, -0.5, 0.3, 0.4, 0.5, 0.3, -0.4, 0.5]);
    // drawPrimitive(gl.TRIANGLE_FAN, [0.596, 0.498, 0.596, 1], [-0.3, -0.2, -0.5, -0.5, -0.4, 0.5, -0.5, 0.4, 0.5, -0.3, 0.6, -0.5]);  

}
```
Saat ini, hanya sisi bawah yang diaktifkan untuk digambar `drawPrimitive(gl.TRIANGLE_FAN, [0.596, 0.498, 0.133, 1], [-0.3, -0.2, -0.5, 0.5, -0.2, -0.5, 0.3, -0.4, 0.5, -0.5, -0.4, 0.5]);`. Anda dapat mengaktifkan sisi lainnya (menghilangkan komentar pada panggilan drawPrimitive yang lain) untuk menggambar keseluruhan kubus dengan warna-warna yang berbeda pada setiap sisinya.

<img width="439" alt="Kubus Sisi Bawah" src="https://github.com/mashitaad/5025211036_Mashita-Dewi_Computer-Graphics_Assignment-3/assets/87978863/6673c836-db6f-4a72-a832-bbd5b0681594">

5. Sisi Kanan
```ruby
function draw() { 
    gl.clearColor(0,0,0,1);
    gl.clear(gl.COLOR_BUFFER_BIT | gl.DEPTH_BUFFER_BIT);
    
    /* Draw the six faces of a cube, with different colors. */
    
    // drawPrimitive(gl.TRIANGLE_FAN, [0.133, 0.611, 0.565, 1], [-0.5, -0.4, -0.5, -0.5, 0.4, -0.5, 0.3, 0.4, -0.5, 0.3, -0.4, -0.5]);  
    // drawPrimitive(gl.TRIANGLE_FAN, [0.913, 0.721, 0.141, 1], [-0.3, -0.2, 0.5, 0.5, -0.2, 0.5, 0.5, 0.6, 0.5, -0.3, 0.6, 0.5]); 
    // drawPrimitive(gl.TRIANGLE_FAN, [0.917, 0.722, 0.133, 1], [-0.3, 0.6, -0.5, -0.5, 0.4, 0.5, 0.3, 0.4, 0.5, 0.5, 0.6, -0.5]);
    // drawPrimitive(gl.TRIANGLE_FAN, [0.596, 0.498, 0.133, 1], [-0.3, -0.2, -0.5, 0.5, -0.2, -0.5, 0.3, -0.4, 0.5, -0.5, -0.4, 0.5]);  
    	drawPrimitive(gl.TRIANGLE_FAN, [0.929, 0.576, 0.133, 1], [0.5, -0.2, -0.5, 0.5, 0.6, -0.5, 0.3, 0.4, 0.5, 0.3, -0.4, 0.5]);
    // drawPrimitive(gl.TRIANGLE_FAN, [0.596, 0.498, 0.596, 1], [-0.3, -0.2, -0.5, -0.5, -0.4, 0.5, -0.5, 0.4, 0.5, -0.3, 0.6, -0.5]);  

}
```
Saat ini, hanya sisi kanan yang diaktifkan untuk digambar `drawPrimitive(gl.TRIANGLE_FAN, [0.929, 0.576, 0.133, 1], [0.5, -0.2, -0.5, 0.5, 0.6, -0.5, 0.3, 0.4, 0.5, 0.3, -0.4, 0.5]);`. Anda dapat mengaktifkan sisi lainnya (menghilangkan komentar pada panggilan drawPrimitive yang lain) untuk menggambar keseluruhan kubus dengan warna-warna yang berbeda pada setiap sisinya.

<img width="431" alt="Kubus Sisi Kanan" src="https://github.com/mashitaad/5025211036_Mashita-Dewi_Computer-Graphics_Assignment-3/assets/87978863/5eab2448-816a-4131-b518-896314fd8e93">

6. Sisi Kiri
```ruby
function draw() { 
    gl.clearColor(0,0,0,1);
    gl.clear(gl.COLOR_BUFFER_BIT | gl.DEPTH_BUFFER_BIT);
    
    /* Draw the six faces of a cube, with different colors. */
    
    // drawPrimitive(gl.TRIANGLE_FAN, [0.133, 0.611, 0.565, 1], [-0.5, -0.4, -0.5, -0.5, 0.4, -0.5, 0.3, 0.4, -0.5, 0.3, -0.4, -0.5]);  
    // drawPrimitive(gl.TRIANGLE_FAN, [0.913, 0.721, 0.141, 1], [-0.3, -0.2, 0.5, 0.5, -0.2, 0.5, 0.5, 0.6, 0.5, -0.3, 0.6, 0.5]); 
    // drawPrimitive(gl.TRIANGLE_FAN, [0.917, 0.722, 0.133, 1], [-0.3, 0.6, -0.5, -0.5, 0.4, 0.5, 0.3, 0.4, 0.5, 0.5, 0.6, -0.5]);
    // drawPrimitive(gl.TRIANGLE_FAN, [0.596, 0.498, 0.133, 1], [-0.3, -0.2, -0.5, 0.5, -0.2, -0.5, 0.3, -0.4, 0.5, -0.5, -0.4, 0.5]);  
    // drawPrimitive(gl.TRIANGLE_FAN, [0.929, 0.576, 0.133, 1], [0.5, -0.2, -0.5, 0.5, 0.6, -0.5, 0.3, 0.4, 0.5, 0.3, -0.4, 0.5]);
    	drawPrimitive(gl.TRIANGLE_FAN, [0.596, 0.498, 0.596, 1], [-0.3, -0.2, -0.5, -0.5, -0.4, 0.5, -0.5, 0.4, 0.5, -0.3, 0.6, -0.5]);  

}
```
Saat ini, hanya sisi kiri yang diaktifkan untuk digambar `drawPrimitive(gl.TRIANGLE_FAN, [0.596, 0.498, 0.596, 1], [-0.3, -0.2, -0.5, -0.5, -0.4, 0.5, -0.5, 0.4, 0.5, -0.3, 0.6, -0.5]);`

<img width="441" alt="Kubus Sisi Kiri" src="https://github.com/mashitaad/5025211036_Mashita-Dewi_Computer-Graphics_Assignment-3/assets/87978863/d2abfc20-7166-47d9-91a9-1b587262f12b">
