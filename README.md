# 🏫 Mini Project (Sistem Pendaftaran Lomba Sekolah)

### Anggota Kelompok:
- [Mochamad Naufal Hanif](www.linkedin.com/in/mochamad-naufal-hanif-652ab23a5)
- [Keiyla Adya Azzani](www.linkedin.com/in/keiyla-adya-azzani-a75ab53a5)
- [Rinzani Fauziah](www.linkedin.com/in/rinzani-fauziah-9919383a5)

*Kelas: XI RPL 1*

---

## Deskripsi Proyek

Proyek ini merupakan mini project basis data **Sistem Pendaftaran Lomba Sekolah** yang dibuat menggunakan **MariaDB**. Sistem ini bertujuan untuk mengelola data peserta, data lomba, serta data pendaftaran peserta ke lomba secara terstruktur. Dengan sistem ini, proses pendaftaran lomba dapat dicatat dengan rapi dan mudah ditampilkan kembali menggunakan query database.

Database ini mengimplementasikan konsep **DDL (Data Definition Language)** untuk pembuatan dan perubahan struktur tabel, **DML (Data Manipulation Language)** untuk pengelolaan data, serta penggunaan **JOIN, VIEW, dan fungsi agregat** untuk menampilkan dan mengolah data pendaftaran lomba.

---

## 🗄️ Pembuatan Database

```sql
create database pendaftaran_lomba;
use pendaftaran_lomba;
```

Database `pendaftaran_lomba` dibuat sebagai tempat penyimpanan seluruh data yang berkaitan dengan pendaftaran lomba.

---

## 📑 Pembuatan Tabel (DDL)

### 1️⃣ Tabel Peserta

```sql
create table peserta(
    id_peserta varchar(10) primary key,
    nama_peserta varchar(50),
    kelas varchar(15)
);
```
```sql
describe peserta;
```
**Hasil:**
| Field | Type | Null | Key | Default | Extra |
| ------------ | ----------- | ---- | --- | ------- | ----- |
| id_peserta | varchar(10) | NO | PRI | NULL | |
| nama_peserta | varchar(50) | YES | | NULL | |
| kelas | varchar(15) | YES | | NULL | |

Tabel `peserta` digunakan untuk menyimpan data peserta lomba.  
`id_peserta` berfungsi sebagai **primary key**.

---

### 2️⃣ Tabel Lomba

```sql
create table lomba(
    id_lomba varchar(10) primary key,
    nama_lomba varchar(50),
    kategori varchar(50)
);
```
```sql
describe lomba;
```
**Hasil:**
| Field | Type | Null | Key | Default | Extra |
| ---------- | ----------- | ---- | --- | ------- | ----- |
| id_lomba | varchar(10) | NO | PRI | NULL | |
| nama_lomba | varchar(50) | YES | | NULL | |
| kategori | varchar(20) | YES | | NULL | |

Tabel `lomba` digunakan untuk menyimpan data lomba beserta kategorinya (Akademik dan Non-Akademik).

---

### 3️⃣ Tabel Pendaftaran

```sql
create table pendaftaran(
    id_pendaftaran varchar(10) primary key,
    id_peserta varchar(10),
    id_lomba varchar(10),
    tgl_daftar date,
    foreign key (id_peserta) references peserta(id_peserta),
    foreign key (id_lomba) references lomba(id_lomba)
);
```
```sql
describe pendaftaran;
```
**Hasil:**
| Field | Type | Null | Key | Default | Extra |
| -------------- | ----------- | ---- | --- | ------- | ----- |
| id_pendaftaran | varchar(10) | NO | PRI | NULL | |
| id_peserta | varchar(10) | YES | MUL | NULL | |
| id_lomba | varchar(10) | YES | MUL | NULL | |
| tgl_daftar | date | YES | | NULL | |

Tabel `pendaftaran` digunakan untuk mencatat peserta yang mendaftar ke lomba tertentu.  
Dan relasi antar tabel dibuat menggunakan **foreign key**.

---

## ✍️ Pengisian Data (DML – INSERT)

### 🔹Data Peserta

```sql
insert into peserta values
('PS001', 'Naufal', 'XI RPL 1'),
('PS002', 'Keiyla', 'XI DPIB 1'),
('PS003', 'Rinzani', 'XI TOI 1'),
('PS004', 'Hanif', 'XI DKV 3'),
('PS005', 'Fauziah', 'XI TOI 1');
```
**Hasil:**
| id_peserta | nama_peserta | kelas |
| ---------- | ------------ | --------- |
| PS001 | Naufal | XI RPL 1 |
| PS002 | Keiyla | XI DPIB 1 |
| PS003 | Rinzani | XI TOI 1 |
| PS004 | Hanif | XI DKV 1 |
| PS005 | Fauziah | XI TOI 1 |

---

### 🔹Data Lomba

```sql
insert into lomba values
('LB001', 'Cerdas Cermat', 'Akademik'),
('LB002', 'Olimpiade Matematika', 'Akademik'),
('LB003', 'Olimpiade Bulu Tangkis', 'Non-Akademik'),
('LB004', 'Karya Tulis Ilmiah', 'Akademik'),
('LB005', 'Olimpiade Bola Voli', 'Non-Akademik');
```
**Hasil:**
| id_lomba | nama_lomba | kategori |
| -------- | ------------------ | ------------ |
| LB001 | Cerdas Cermat | Akademik |
| LB002 | Olimpiade Fisika | Akademik |
| LB003 | Karya Tulis Ilmiah | Akademik |
| LB004 | Bola Voli | Non-Akademik |
| LB005 | Bulu Tangkis | Non-Akademik |

---
### 🔹Data Pendaftaran

```sql
insert into pendaftaran values
('DF001', 'PS001', 'LB001', '2026-02-01'),
('DF002', 'PS002', 'LB001', '2026-02-01'),
('DF003', 'PS003', 'LB003', '2026-02-02'),
('DF004', 'PS004', 'LB004', '2026-02-02'),
('DF005', 'PS005', 'LB005', '2026-02-03'),
('DF006', 'PS001', 'LB004', '2026-02-03'),
('DF007', 'PS002', 'LB003', '2026-02-04'),
('DF008', 'PS003', 'LB001', '2026-02-04'),
('DF009', 'PS004', 'LB005', '2026-02-05'),
('DF010', 'PS005', 'LB003', '2026-02-05');
```
**Hasil:**
| id_pendaftaran | id_peserta | id_lomba | tanggal_daftar |
| -------------- | ---------- | -------- | -------------- |
| DF001 | PS001 | LB001 | 2026-02-01 |
| DF002 | PS002 | LB001 | 2026-02-01 |
| DF003 | PS003 | LB004 | 2026-02-02 |
| DF004 | PS004 | LB003 | 2026-02-02 |
| DF005 | PS005 | LB005 | 2026-02-03 |
| DF006 | PS001 | LB003 | 2026-02-03 |
| DF007 | PS002 | LB004 | 2026-02-04 |
| DF008 | PS003 | LB001 | 2026-02-04 |
| DF009 | PS004 | LB005 | 2026-02-05 |
| DF010 | PS005 | LB004 | 2026-02-05 |

----

## ✏️ Manipulasi Data (DML - UPDATE | DELETE)

### 🔹UPDATE

```sql
update peserta
set kelas = 'XI DKV 1'
where id_peserta = 'PS004';
```
```sql
select * from peserta;
```
**Hasil:**
| id_peserta | nama_peserta | kelas     |
|------------|--------------|-----------|
| PS001      | Naufal       | XI RPL 1  |
| PS002      | Keiyla       | XI DPIB 1 |
| PS003      | Rinzani      | XI TOI 1  |
| PS004      | Hanif        | XI DKV 1  |
| PS005      | Fauziah      | XI TOI 1  |

Digunakan untuk memperbarui data kelas peserta.

---

### 🔹DELETE

```sql
delete from pendaftaran
where id_pendaftaran = 'DF010';
```
```sql
select * from pendaftaran;
```
**Hasil:**
| id_pendaftaran | id_peserta | id_lomba | tanggal_daftar |
|----------------|------------|----------|----------------|
| DF001          | PS001      | LB001    | 2026-02-01     |
| DF002          | PS002      | LB001    | 2026-02-01     |
| DF003          | PS003      | LB003    | 2026-02-02     |
| DF004          | PS004      | LB004    | 2026-02-02     |
| DF005          | PS005      | LB005    | 2026-02-03     |
| DF006          | PS001      | LB004    | 2026-02-03     |
| DF007          | PS002      | LB003    | 2026-02-04     |
| DF008          | PS003      | LB001    | 2026-02-04     |
| DF009          | PS004      | LB005    | 2026-02-05     |

Digunakan untuk menghapus satu data pendaftaran tertentu.

---

## 🔧 Perubahan Struktur Tabel (DDL – ALTER)

```sql
alter table pendaftaran
change tgl_daftar tanggal_daftar date;
```
```sql
describe pendaftaran;
```

**Hasil:**
| Field          | Type        | Null | Key | Default | Extra |
|----------------|-------------|------|-----|---------|-------|
| id_pendaftaran | varchar(10) | NO   | PRI | NULL    |       |
| id_peserta     | varchar(10) | YES  | MUL | NULL    |       |
| id_lomba       | varchar(10) | YES  | MUL | NULL    |       |
| tanggal_daftar | date        | YES  |     | NULL    |       |
Perintah ini digunakan untuk mengganti nama kolom agar lebih jelas.

---

## 🔗 Implementasi JOIN

### 🔹INNER JOIN

```sql
select peserta.nama_peserta, lomba.nama_lomba
from pendaftaran
inner join peserta on pendaftaran.id_peserta = peserta.id_peserta
inner join lomba on pendaftaran.id_lomba = lomba.id_lomba;
```
**Hasil:**
| nama_peserta | nama_lomba             |
|--------------|------------------------|
| Naufal       | Cerdas Cermat          |
| Keiyla       | Cerdas Cermat          |
| Rinzani      | Olimpiade Bulu Tangkis |
| Hanif        | Karya Tulis Ilmiah     |
| Fauziah      | Olimpiade Bola Voli    |
| Naufal       | Karya Tulis Ilmiah     |
| Keiyla       | Olimpiade Bulu Tangkis |
| Rinzani      | Cerdas Cermat          |
| Hanif        | Olimpiade Bola Voli    |

Digunakan untuk menampilkan peserta yang **sudah mendaftar lomba**.

---

### 🔹LEFT JOIN

```sql
select lomba.nama_lomba, peserta.nama_peserta
from lomba
left join pendaftaran on lomba.id_lomba = pendaftaran.id_lomba
left join peserta on pendaftaran.id_peserta = peserta.id_peserta;
```
**Hasil:**
| nama_lomba             | nama_peserta |
|------------------------|--------------|
| Cerdas Cermat          | Naufal       |
| Cerdas Cermat          | Keiyla       |
| Cerdas Cermat          | Rinzani      |
| Olimpiade Matematika   | NULL         |
| Olimpiade Bulu Tangkis | Rinzani      |
| Olimpiade Bulu Tangkis | Keiyla       |
| Karya Tulis Ilmiah     | Hanif        |
| Karya Tulis Ilmiah     | Naufal       |
| Olimpiade Bola Voli    | Fauziah      |
| Olimpiade Bola Voli    | Hanif        |

Digunakan untuk menampilkan **seluruh lomba**, termasuk lomba yang belum memiliki peserta.

---

## 👁️ VIEW
_VIEW digunakan untuk menyimpan hasil JOIN agar query lebih sederhana._

```sql
create view view_pendaftaran as
select peserta.nama_peserta,
       lomba.nama_lomba,
       lomba.kategori,
       pendaftaran.tanggal_daftar
from pendaftaran
join peserta on pendaftaran.id_peserta = peserta.id_peserta
join lomba on pendaftaran.id_lomba = lomba.id_lomba;
```
**Hasil:**
| Field          | Type        | Null | Key | Default | Extra |
|----------------|-------------|------|-----|---------|-------|
| nama_peserta   | varchar(50) | YES  |     | NULL    |       |
| nama_lomba     | varchar(50) | YES  |     | NULL    |       |
| kategori       | varchar(50) | YES  |     | NULL    |       |
| tanggal_daftar | date        | YES  |     | NULL    |       |

---

```sql
select * from view_pendaftaran;
```
**Hasil:**
| Field          | Type        | Null | Key | Default | Extra |
|----------------|-------------|------|-----|---------|-------|
| nama_peserta   | varchar(50) | YES  |     | NULL    |       |
| nama_lomba     | varchar(50) | YES  |     | NULL    |       |
| kategori       | varchar(50) | YES  |     | NULL    |       |
| tanggal_daftar | date        | YES  |     | NULL    |       |

---

## 📊 Fungsi Agregat

### 🔹COUNT

```sql
select count(*) as jumlah_pendaftaran from pendaftaran;
```
**Hasil:**
| jumlah_pendaftaran  |
|-------------------- | 
|         9           |
| |
---

### 🔹MIN 

```sql
select min(tanggal_daftar) as pendaftaran_pertama from pendaftaran;
```
**Hasil:**
| pendaftaran_pertama |
|---------------------|
| 2026-02-01          |
||

---

### 🔹MAX

```sql
select max(tanggal_daftar) as pendaftaran_terakhir from pendaftaran;
```
**Hasil:**
| pendaftaran_pertama |
|---------------------|
| 2026-02-05          |
||

---

## ✅ Kesimpulan

Mini project ini telah menerapkan konsep **DDL, DML, JOIN, VIEW, dan fungsi agregat** secara lengkap. Database pendaftaran lomba dapat digunakan untuk mengelola data peserta, lomba, dan pendaftaran dengan baik serta memenuhi kriteria tugas basis data.

---
