## Dockerizing Flask With Compose and Machine

Featuring:

- Docker v18.09.2
- Docker Compose v1.23.2
- Docker Machine v0.16.1

## Dependency yang diinstall (windows machine):

Link https://docs.docker.com/docker-for-windows/install/

1. Docker
2. Virtualbox
3. wsl_update_x64

## Docker Commands

1. Run - menjalankan container
   ex: docker run nginx

2. ps - daftar container yang ada
   ex: docker ps - melihat daftar container aktif
   docker ps -a - melihat daftar container aktif dan tidak aktif

3. Stop - memberhentikan container
   ex: docker stop nama_container

4. Rm - Remove a container
   ex: docker rm nama_container

5. images - daftar images di machine docker
   ex: docker images

6. rmi - menghapus images yang ada di machine docker
   ex: docker rmi nginx

7. pull - download image baru
   ex: docker pull nginx

## Docker Run

1. Run: Menjalankan images
   ex: docker run redis (latest version), docker run redis: 4.0. (versi 4.0)

2. run -i & run -it : Menerima input command

3. PORT mapping: Agar client dapat melakukan akses ke host, assign port
   ex: docker run -p 80:5000 application_name

   Akses aplikasi terdapat 2 cara

   1. Akses melalui ip docker ex: 172.17.0.2 (hanya assesible dari dalam docker host (internal ip))
   2. Menggunakan ip docker host 192.168.1.5, lalu alokasikan ke port yang kosong.

4. Volume mapping: Melakukan alokasi db diluar container, agar saat db di dalam container dihapus, akan terbuat backup di luar docker
   ex: docker run -v /nama_direktori/datadir:/var/lib/mysql mysql

5. Inspect Container: Menyajikan data JSON dari container yang dipilih
   ex: docker inspect nama_container

6. Container logs: Menyajikan data logs dari container
   ex: docker logs nama_container

## Environment Variables

1. .ENV dialokasikan untuk mengubah variabel saat sudah masuk container
   ex: docker run -e NAMA_DB=acikiwir nama_aplikasi

2. Inspect Environment Variables = digunakan untuk melihat variable env
   ex: docker inspect nama_aplikasi

## Images

1. Membuat images dari web app yang dibangun
   1. Buat Dockerfile, berisi perintah berkaitan dengan instalasi dependencies yang digunakan dan running aplikasi
   2. docker build Dockerfile -t directory/nama_aplikasi
   3. docker push directory/nama_aplikasi

## Networking

1. Bridge: IP default yang ada pada docker host, setiap container memiliki ip default nya masing-masing (172.17.0.x)

2. Host : Digunakan agar memungkinkan mengakses container dari luar docker host. 1 port hanya dapat dialokasikan untuk 1 container

3. User defined network: digunakan agar mampu membuat custom bridge
   ex: docker network create \ --driver bridge \ --subnet 182.18.0.0/016 custom-isolated-network

4. Inspect Network: melihat deskripsi network dari container berkaitan (IPAddress, MACAddress)
   ex: docker inspect nama_container

5. EMBEDDED DNS: Dapat digunakan untuk mengkases container lain dari suatu container
   ex: container web membutuhkan koneksi ke container db. Dapat diembed cukup dengan nama saja

## Compose
