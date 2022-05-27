# Sistem-Operasi-Docker-2---Aliens
# Nama dan NIM
Nama  : Kevinsien Heldrayetno <br />
NIM   : 120140174
# Aliens
Program yang saya gunakan adalah program yang dibuat oleh [Anthony Oliver](https://github.com/xamox) yang berupa aplikasi permainan yang terinspirasi dari Alien Shooter. Permainan ini memiliki tujuan untuk memusnahkan alien dan bertahan hidup dari serangan alien dan mendapatkan skor yang tinggi. permainan ini berakhir ketika nyawa dari pemain habis
# Cara Menjalankan Kontainer
Hal ini dapat dimulai dengan mengclone repository lalu pindahkan ke dalam folder yang akan digunakan. Kita harus mengganti directory yang terdapat dalam file `Makefile`.
## Cara mengganti directory dalam Makefile
```
build-handson:
	docker build . -t handson

xhost:
	xhost +	

run-windows:
	docker run --privileged -it --rm --cap-add=SYS_PTRACE -u 1000:1000 -e DISPLAY=127.0.0.1:0.0 -v %userprofile%\[Directory Folder]:/home/docker handson

run-linux:	xhost
	docker run --privileged -it --rm \
	--cap-add=SYS_PTRACE \
	-u 1000:1000 \
	-v /tmp/.X11-unix:/tmp/.X11-unix \
	-e DISPLAY \
	-v /run/dbus:/run/dbus \
	-v /dev/shm:/dev/shm \
	--device /dev/snd \
	--device /dev/dri \
	-e PULSE_SERVER=unix:${XDG_RUNTIME_DIR}/pulse/native \
	-v ${XDG_RUNTIME_DIR}/pulse/native:${XDG_RUNTIME_DIR}/pulse/native \
	-v /run/user/1000/pulse:/run/user/1000/pulse \
	-v /var/run/dbus:/var/run/dbus \
	-v ~/[Directory Folder]/home/docker \
	handson

run-mac:	xhost
	docker run --privileged -it --rm -u 1000:1000 \
	--cap-add=SYS_PTRACE \
	-v /tmp/.X11-unix:/tmp/.X11-unix \
	-e DISPLAY=docker.for.mac.host.internal:0 \
	-v ~/.config/pulse:/run/user/1000/pulse \
	-v ~/[Directory Folder]/home/docker \
	handson
```
Kita dapat mengganti `[Directory Folder]` dengan directory folder yang dipakai

Selanjutnya buka terminal pada direktori folder tersebut lalu masukan perintah build seperti berikut:
```
make build-handson
```

Lalu kita dapat mengecek apakah terdpat repository `handson` setelah proses build selesai dengan menjalankan perintah images untuk melihat daftar images yang terdapat local storage. perintah dari langkah tersebut adalah sebagai berikut:
```
docker images
```

Ketika proses build telah selesai atau setelah mengecek images yang terdapat dalam local storage, jalankan perintah run sesuai sistem operasi yang digunakan sebagai berikut :
### Windows
```
make run-windows
```
### Linux
```
make run-linux
```
### Mac
```
make run-mac
```

Dan langkah terakhir yang digunakan untuk menjalankan pygame melalui kontainer yang telah dibuat adalah sebagai berikut:
```
python3 aliens.py
```

#Video Penjelasan
[![IMAGE ALT TEXT HERE](https://img.youtube.com/vi/iQpaFnFqYJw/0.jpg)]([https://www.youtube.com/watch?v=YOUTUBE_VIDEO_ID_HERE](https://www.youtube.com/watch?v=iQpaFnFqYJw))


