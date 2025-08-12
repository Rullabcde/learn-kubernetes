## Pengertian Kubernetes

[Kubernetes](https://kubernetes.io/) adalah platform open-source yang dirancang untuk mengotomatiskan proses pengelolaan, penskalaan, dan penerapan aplikasi container. Kubernetes menyediakan kerangka kerja untuk menjalankan aplikasi containerized di lingkungan yang terdistribusi, membantu memastikan ketersediaan tinggi, skalabilitas, dan efisiensi sumber daya.

## Arsitektur Cluster Kubernetes

<img src="https://kubernetes.io/images/docs/kubernetes-cluster-architecture.svg" alt="architecture kubernetes" width="400">
Cluster Kubernetes terdiri dari beberapa komponen utama yang bekerja bersama untuk mengelola aplikasi yang berjalan di dalamnya. Berikut adalah komponen-komponen utama dari arsitektur Kubernetes:

### 1. _Node_

- _Master Node_: Mengontrol dan mengelola seluruh cluster. Master node terdiri dari beberapa komponen seperti API Server, Scheduler, Controller Manager, dan etcd.

  - _API Server_: Komponen utama yang berinteraksi dengan komponen lain dalam Kubernetes. Semua perintah ke cluster Kubernetes dikirim ke API Server.
  - _Scheduler_: Bertanggung jawab untuk menugaskan Pod ke Node berdasarkan sumber daya yang tersedia dan kebutuhan aplikasi.
  - _Controller Manager_: Mengelola kontroler yang menangani berbagai tugas seperti replikasi Pod, pengaturan endpoint, dan lainnya.
  - _etcd_: Penyimpanan key-value yang menyimpan semua data konfigurasi cluster.

- _Worker Node_: Menjalankan aplikasi dalam bentuk Pod dan dikendalikan oleh Master Node. Worker Node terdiri dari beberapa komponen:
  - _Kubelet_: Agen yang berjalan di setiap Node dan memastikan container dijalankan sebagaimana mestinya.
  - _Kube-proxy_: Mengelola jaringan dalam cluster, memastikan komunikasi antar Pod dan layanan berjalan lancar.
  - _Container Runtime_: Perangkat lunak yang menjalankan container, misalnya Docker atau containerd.

### 2. _Pod_

- Unit terkecil dalam Kubernetes yang berisi satu atau lebih container. Setiap Pod memiliki IP unik dan berbagi penyimpanan serta jaringan. Pod adalah cara Kubernetes mengelola aplikasi containerized.

### 3. _Service_

- Abstraksi untuk mendefinisikan kumpulan Pod dan menyediakan cara yang stabil untuk mengaksesnya. Service memungkinkan Anda mengakses aplikasi di dalam Pod tanpa perlu tahu IP Pod secara langsung.

### 4. _Namespace_

- Mekanisme untuk mengisolasi dan mempartisi sumber daya dalam cluster. Namespace memungkinkan pengguna untuk mengelola beberapa lingkungan seperti dev, staging, dan production dalam satu cluster.

### 5. _Deployment_

- Abstraksi yang mendefinisikan bagaimana aplikasi di-deploy dan di-manage di dalam cluster. Deployment mengelola proses scaling dan rolling update Pod secara otomatis.

### 6. _ConfigMap dan Secret_

- _ConfigMap_: Menyimpan data konfigurasi dalam bentuk key-value yang bisa digunakan oleh Pod.
- _Secret_: Menyimpan data sensitif seperti password dan token yang juga dalam bentuk key-value, tetapi lebih aman dari ConfigMap.
