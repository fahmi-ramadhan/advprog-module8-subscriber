## Advanced Programming Module 8 - Subscriber

### Reflection

> 7a. what is amqp?

AMQP adalah singkatan dari "Advanced Message Queuing Protocol", sebuah protokol untuk mengirimkan dan menerima pesan antara aplikasi dan layanan, misalnya di sini antara _subscriber_ dengan _publisher_.

> 7b. what it means? `guest:guest@localhost:5672`, what is the first guest, what is the second guest, and what is `localhost:5672` for?

`guest:guest@localhost:5672` adalah bagian dari URL koneksi yang digunakan untuk terhubung ke server RabbitMQ (_message broker_ berbasis AMQP yang populer).

- `guest` pertama adalah nama pengguna untuk otentikasi.
- `guest` kedua adalah kata sandi untuk otentikasi.
- `localhost:5672` adalah alamat host dan nomor port tempat RabbitMQ berjalan. `localhost` berarti di mesin yang sama dengan klien, dan `5672` adalah port default untuk protokol AMQP.

### Simulation Slow Subscriber

![Simulation Slow Subscriber](https://i.imgur.com/MimMdbW.png)

Perhatikan bahwa terdapat 15 pesan pada _queue_, ini terjadi karena terdapat _buffer_ 1 detik untuk menunggu setiap proses pengiriman pesan dan saya mengeksekusi `cargo run` pada _publisher_ sebanyak 4 kali secara cepat.

### Running At Least Three Subscribers

![Console](https://i.imgur.com/Qurnus3.png)
![RabbitMQ](https://i.imgur.com/5DW7srG.png)

Dengan menjalankan 3 _subscriber_ yang terhubung ke _queue_ yang sama, dapat dilihat bahwa pemrosesan _event_ terbagi di antara _subscriber_-_subscriber_ tersebut. Pada kasus ini, saya mengeksekusi `cargo run` pada _publisher_ sebanyak 4 kali dan terlihat bahwa _queued message_ pada grafik menurun menjadi 7,5. Hal ini diperoleh melalui pemrosesan _event_ secara simultan oleh beberapa _subscriber_.

Melalui refleksi ini, dapat dipertimbangkan juga untuk melakukan peningkatan pada kode _publisher_ dan _subscriber_. Sebagai contoh, _publisher_ dapat dioptimalkan dengan implementasi pengiriman asinkronus untuk menghindari menunggu setiap pesan terkirim, serta menggunakan _batch processing_ untuk mengirim beberapa pesan sekaligus yang dapat mengurangi beban jaringan. Selain itu, pada _subscriber_, _parallel processing_ untuk setiap _subscriber_ juga dapat diterapkan dengan memanfaatkan fitur konkurensi Rust seperti _threads_ atau _async-await_. Hal ini akan membantu meningkatkan kinerja dan efisiensi sistem yang berbasis _event_-_driven_.
