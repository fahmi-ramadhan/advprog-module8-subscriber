## Advanced Programming Module 8 - Subscriber

### Reflection

> 7a. what is amqp?

AMQP adalah singkatan dari "Advanced Message Queuing Protocol", sebuah protokol untuk mengirimkan dan menerima pesan antara aplikasi dan layanan, misalnya di sini antara _subscriber_ dengan _publisher_.

> 7b. what it means? `guest:guest@localhost:5672`, what is the first guest, what is the second guest, and what is `localhost:5672` for?

`guest:guest@localhost:5672` adalah bagian dari URL koneksi yang digunakan untuk terhubung ke server RabbitMQ (_message broker_ berbasis AMQP yang populer).

- `guest` pertama adalah nama pengguna untuk otentikasi.
- `guest` kedua adalah kata sandi untuk otentikasi.
- `localhost:5672` adalah alamat host dan nomor port tempat RabbitMQ berjalan. `localhost` berarti di mesin yang sama dengan klien, dan `5672` adalah port default untuk protokol AMQP.
