## 0. Prasyarat

Pastikan Command Prompt dibuka dari path instalasi Kafka.

---

## 1. Generate Cluster ID

Digunakan untuk mengidentifikasi cluster Kafka secara unik (KRaft).

```bash
bin\windows\kafka-storage.bat random-uuid
```

Output:

```text
[ cluster-id ]
```

---

## 2. Format Storage (Inisialisasi Metadata)

Menginisialisasi storage metadata Kafka dengan cluster ID tertentu.

```bash
bin\windows\kafka-storage.bat format ^
  --cluster-id [ cluster-id ] ^
  --config config\kraft\server.properties
```

---

## 3. Menjalankan Kafka Broker

```bash
bin\windows\kafka-server-start.bat config\kraft\server.properties
```

Broker akan berjalan di:

```text
localhost:9092
```

---

## 4. Membuat Topic

```bash
bin\windows\kafka-topics.bat ^
  --bootstrap-server localhost:9092 ^
  --create ^
  --topic [ nama-topic ]
```

**Catatan penting**:

* Data di Kafka bersifat **append-only**
* Message selalu ditambahkan ke **akhir log**
* Tidak bisa insert ke tengah atau depan

---

## 5. Melihat Daftar Topic

```bash
bin\windows\kafka-topics.bat ^
  --bootstrap-server localhost:9092 ^
  --list
```

Output:

```text
[ nama-topic-1 ]
[ nama-topic-2 ]
```

---

## 6. Mengirim Message (Producer)

```bash
bin\windows\kafka-console-producer.bat ^
  --bootstrap-server localhost:9092 ^
  --topic [ nama-topic ]
```

Input manual:

```text
[ isi-pesan ]
[ isi-pesan ]
[ isi-pesan ]
```

---

## 7. Membaca Message (Consumer)

```bash
bin\windows\kafka-console-consumer.bat ^
  --bootstrap-server localhost:9092 ^
  --topic [ nama-topic ] ^
  --from-beginning
```

Output:

```text
[ isi-pesan ]
[ isi-pesan ]
[ isi-pesan ]
```

---

## 8. Consumer Group

Consumer group digunakan untuk:

* Load balancing antar consumer
* Manajemen offset

```bash
bin\windows\kafka-console-consumer.bat ^
  --bootstrap-server localhost:9092 ^
  --topic [ nama-topic ] ^
  --group [ nama-consumer-group ] ^
  --from-beginning
```

---

## 9. Melihat Informasi Offset Consumer Group

```bash
bin\windows\kafka-consumer-groups.bat ^
  --bootstrap-server localhost:9092 ^
  --all-groups ^
  --all-topics ^
  --describe
```

Informasi yang ditampilkan:

* Current offset
* Log end offset
* Lag per consumer group
