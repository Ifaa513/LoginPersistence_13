# LOGIN DENGAN PERSISTENCE 🔑
## Langkah-langkah membuat halaman login dengan persistence 👤
### 1. 🗂️ Membuat tabel baru untuk menyimpan data akun 

![LOG1](https://github.com/user-attachments/assets/e0daa999-df44-41bd-a8d0-dd5893f2d26d)

### 2. 📝 Isi tabel dengan beberapa username akun beserta passwordnya

![LOG2](https://github.com/user-attachments/assets/399b0770-c4e8-4f64-a0c2-77eabd316a73)

### 3. 🚪 Beralih ke Netbeans, buat persistence unit baru, dengan cara klik kanan package > New > Entity classes from database

![LOG3](https://github.com/user-attachments/assets/a4c0a267-6a60-4eb2-89e0-3f32ed21868c)

### 4. 🕹️ Pilih database connection, kemudian pilih tabel yang dibutuhkan, klik add agar tabel yang dipilih pindah ke kotak selected tables, kemudian klik next hingga finish

![LOG4](https://github.com/user-attachments/assets/4a141346-af3a-4a58-beb2-b75e83c0b435)

![LOG5](https://github.com/user-attachments/assets/1c491619-5f39-452c-892f-1f906d88a43a)

![LOG6](https://github.com/user-attachments/assets/52230702-d06e-4898-9d47-34e5d065efd6)

### 5.	🗂️ Maka, secara otomatis akan terdapat package baru yaitu META-INF dan class baru yaitu Dataakun.java

![LOG7](https://github.com/user-attachments/assets/44f6d5f8-ad42-463f-bf76-3d06546102b4)

### 6.	🖼️ Selanjutnya, buat frame baru untuk tampilan menu Login, yaitu dengan cara klik kanan package > New > JFrame form

![LOG9](https://github.com/user-attachments/assets/ccc0679f-56cc-40c5-b323-958238e309d2)

![image](https://github.com/user-attachments/assets/3e06117a-432d-4d49-b1d9-19081a314b76)

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

![image](https://github.com/user-attachments/assets/4a1fba31-0320-41db-b6a9-aac6da2818f6)

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

![image](https://github.com/user-attachments/assets/45d05a84-62c0-4a5b-88a6-815f9017ebd5)

## Apabila username dan password yang diinputkan sesuai, maka akan muncul pesan seperti gambar berikut, dan akan langsung masuk ke halaman Matakuliah

![image](https://github.com/user-attachments/assets/9616dbc8-cf12-4331-8acb-90845d92bed3)

![image](https://github.com/user-attachments/assets/97eca76b-b758-485e-a902-a284476fb008)

## Mencoba membuat akun baru dengan klik Register, maka akan langsung masuk ke halaman NEW ACCOUNT berikut, kemudian isi username dan password baru, kemudian klik CREATE

![image](https://github.com/user-attachments/assets/bcbe519a-bfaf-4000-83d2-738909b7749f)

## Maka, akan keluar pesan berhasil seperti berikut, dan ketika di klik ok, akan langsung beralih ke halaman login

![image](https://github.com/user-attachments/assets/58dcfd53-459b-46ca-9b1d-a7b1d28ccf95)

## Mencoba login dengan akun yang telah deregister tadi

![image](https://github.com/user-attachments/assets/3d507a04-2e87-4360-8c14-006f95c40231)

## Dan, login pun berhasil, ini berarti username dan password yang baru didaftarkan tadi telah berhasil disimpan

![image](https://github.com/user-attachments/assets/23b4ddf7-f739-4a95-a145-ccb94dd7daec)
