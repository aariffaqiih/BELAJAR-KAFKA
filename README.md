## 1. Generate Cluster ID

```bash
bin\windows\kafka-storage.bat random-uuid
```

---

## 2. Format Storage (Inisialisasi Metadata)

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

---

## 4. Membuat Topic

```bash
bin\windows\kafka-topics.bat ^
  --bootstrap-server localhost:9092 ^
  --create ^
  --topic [ nama-topic ]
```

---

## 5. Melihat Daftar Topic

```bash
bin\windows\kafka-topics.bat ^
  --bootstrap-server localhost:9092 ^
  --list
```

---

## 6. Mengirim Message (Producer)

```bash
bin\windows\kafka-console-producer.bat ^
  --bootstrap-server localhost:9092 ^
  --topic [ nama-topic ]
```

---

## 7. Mengirim Message dengan Key (Routing ke Partition)

```bash
bin\windows\kafka-console-producer.bat ^
  --bootstrap-server localhost:9092 ^
  --topic [ nama-topic ] ^
  --property "parse.key=true" ^
  --property "key.separator=:"
```

Format input:

```text
[key]:[value]
```

Kafka menentukan partition dengan rumus:

```text
hash(key) % jumlah-partition
```

---

## 8. Membaca Message (Consumer)

```bash
bin\windows\kafka-console-consumer.bat ^
  --bootstrap-server localhost:9092 ^
  --topic [ nama-topic ] ^
  --from-beginning
```

---

## 9. Consumer Group

```bash
bin\windows\kafka-console-consumer.bat ^
  --bootstrap-server localhost:9092 ^
  --topic [ nama-topic ] ^
  --group [ nama-consumer-group ] ^
  --from-beginning
```

---

## 10. Melihat Informasi Offset Consumer Group

```bash
bin\windows\kafka-consumer-groups.bat ^
  --bootstrap-server localhost:9092 ^
  --all-groups ^
  --all-topics ^
  --describe
```

---

## 11. Melihat Detail Topic (Partition & Replication)

```bash
bin\windows\kafka-topics.bat ^
  --bootstrap-server localhost:9092 ^
  --describe ^
  --topic [ nama-topic ]
```

---

## 12. Membaca Message Beserta Key dan Partition

```bash
bin\windows\kafka-console-consumer.bat ^
  --bootstrap-server localhost:9092 ^
  --topic [ nama-topic ] ^
  --group [ nama-consumer-group ] ^
  --from-beginning ^
  --property print.key=true ^
  --property print.partition=true
```

---

## 13. Offset dan Lag per Partition

```bash
bin\windows\kafka-consumer-groups.bat ^
  --bootstrap-server localhost:9092 ^
  --all-groups ^
  --all-topics ^
  --describe
```
