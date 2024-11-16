# LOGIN DENGAN PERSISTENCE 🔑
## Langkah-langkah membuat halaman login dengan persistence 👤
### 1. 🗂️ Membuat tabel baru untuk menyimpan data akun 

### 2. 📝 Isi tabel dengan beberapa username akun beserta passwordnya

### 3. 🚪 Beralih ke Netbeans, buat persistence unit baru, dengan cara klik kanan package > New > Entity classes from database

### 4. 🕹️ Pilih database connection, kemudian pilih tabel yang dibutuhkan, klik add agar tabel yang dipilih pindah ke kotak selected tables, kemudian klik next hingga finish

### 5.	🗂️ Maka, secara otomatis akan terdapat package baru yaitu META-INF dan class baru yaitu Dataakun.java

### 6.	🖼️ Selanjutnya, buat frame baru untuk tampilan menu Login, yaitu dengan cara klik kanan package > New > JFrame form

### 7.	🔑 Source code untuk button LOGIN

    private void btnLoginActionPerformed(java.awt.event.ActionEvent evt) {                                         
        String username = txtUser.getText();
        String password = new String(pw.getPassword());

        EntityManagerFactory manfact = Persistence.createEntityManagerFactory("PersistancePU");
        EntityManager man = manfact.createEntityManager();

        try {
            man.getTransaction().begin();

            Query query = man.createQuery("SELECT l FROM Dataakun l WHERE l.username = :username");
            query.setParameter("username", username);

            if (!query.getResultList().isEmpty()) {
                Dataakun user = (Dataakun) query.getSingleResult();

                if (password.equals(user.getPassword())) {
                    JOptionPane.showMessageDialog(this, "Login berhasil. Selamat Datang!");

                    new MataKuliah().setVisible(true);
                    this.dispose();

                    txtUser.setText("");
                    pw.setText("");
                } else {
                    JOptionPane.showMessageDialog(this, "Password salah, Silakan coba lagi!");
                    pw.setText("");
                }
            } else {
                JOptionPane.showMessageDialog(this, "Username tidak ditemukan. Periksa kembali.");
                txtUser.setText("");
                pw.setText("");
            }

            man.getTransaction().commit();
        } catch (Exception e) {
            e.printStackTrace();
        } finally {
            man.close();
            manfact.close();
        }
    } 
    
### 8.	👤 Selanjutnya, buat frame baru untuk membuat akun apabila pengguna belum memiliki akun

### 9.	🔓 Source code untuk button CREATE, ketika pesan “Register Anda berhasil” muncul, maka program akan langsung mengembalikan pengguna ke halaman login
     private void btnCreateActionPerformed(java.awt.event.ActionEvent evt) {                                          

        String username = txtUser.getText();
        String password = txtPW.getText();

        EntityManagerFactory manfact = Persistence.createEntityManagerFactory("PersistancePU");
        EntityManager man = manfact.createEntityManager();
        man.getTransaction().begin();

        Dataakun lg = new Dataakun();
        lg.setUsername(username);
        lg.setPassword(password);

        man.persist(lg);
        man.getTransaction().commit();

        man.close();
        manfact.close();

        JOptionPane.showMessageDialog(this, "Register Anda berhasil");

        new LoginPage().setVisible(true);
        this.dispose();
    }        

# IMPLEMENTASI 🔥
## Masukkan username dan password



## Apabila username dan password yang diinputkan sesuai, maka akan muncul pesan seperti gambar berikut, dan akan langsung masuk ke halaman Matakuliah



## Mencoba membuat akun baru dengan klik Register, maka akan langsung masuk ke halaman NEW ACCOUNT berikut, kemudian isi username dan password baru, kemudian klik CREATE



## Maka, akan keluar pesan berhasil seperti berikut, dan ketika di klik ok, akan langsung beralih ke halaman login



## Mencoba login dengan akun yang telah deregister tadi



## Dan, login pun berhasil, ini berarti username dan password yang baru didaftarkan tadi telah berhasil disimpan


