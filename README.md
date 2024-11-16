# Tugas Pemrograman Berbasi Obyek Pertemuan 13
## Membuat Form Login Dengan Persistance
### 1. Membuat table baru pada database, beri nama PwLogin. Ini nantinya akan digunakan untuk menyimpan data login.
![image](https://github.com/user-attachments/assets/394332d2-5432-4a91-879d-2bb07f9f988c)

### 2.	Kemudian membuat file persistence untuk menghubungkan entitas class yang ada pada table dalam database dengan file yang akan digunakan nantinya. Klik kanan pada package > New > Entity Classes from Databases…
![image](https://github.com/user-attachments/assets/3800335c-e14a-492d-96a8-16007837c2cd)
![image](https://github.com/user-attachments/assets/d3f00cab-a063-472b-99f2-5665eb4c2518)
Pilih database yang akan digunakan, dan pilih table yang akan dikoneksikan dengan program anda, kemudian klik Add >
![image](https://github.com/user-attachments/assets/8d4b4d3e-d851-4090-bb27-21e4d3f95f24)
Next terus sampai Finish.

### 3.	Kemudian buat file JFrame Form untuk membuat tampilan login dan beri nama formLogin, design seperti berikut, dan masukkan code berikut :
![image](https://github.com/user-attachments/assets/1900ee1a-0d2f-458e-8e07-2fdaf8cb2ef3)
Aktifkan text create new account? Lalu Double klik pada button LOGIN kemudian masukkan source code berikut, 
<pre>
  private void btnLoginActionPerformed(java.awt.event.ActionEvent evt) {                                         
        // TODO add your handling code here:
        if (txtUsername.getText().equals("") | txtPassword.getText().equals("")) {
            JOptionPane.showMessageDialog(null, "Isi Terlebih Dahulu");
        } else {
            EntityManagerFactory emf = Persistence.createEntityManagerFactory("LatihanSemester3PU");
            EntityManager em = emf.createEntityManager();

            em.getTransaction().begin();

            String user = txtUsername.getText();
            String pw = txtPassword.getText();
            Pwlogin y = em.find(Pwlogin.class, user);

            if (y == null) {
                JOptionPane.showMessageDialog(null, "Username tidak ditemukan");
                bersih();
            } else if (y.getPassword().equals(pw)) {
                JOptionPane.showMessageDialog(null, "SELAMAT DATANG!");
                entitasMatakuliah p = new entitasMatakuliah();
                p.setVisible(true);
                this.dispose();
            } else {
                JOptionPane.showMessageDialog(null, "Username atau Password yang Anda Masukkan Salah!");
            }
            em.getTransaction().commit();
            em.close();
            emf.close();
        }
    }  
</pre>
setelah itu masukkan code pada text create untuk membuat fungsi akun baru,
<pre>
  private void createnewMouseClicked(java.awt.event.MouseEvent evt) {                                       
        // TODO add your handling code here:
        create y = new create();
        y.setVisible(true);
        this.dispose();
    }   
</pre>
### 4.	Selanjutnya buat JFrame Form untuk tampilan create new account, dan masukkan source code berikut,
![image](https://github.com/user-attachments/assets/a5ee1d6e-3851-4025-87a5-7fb286b81b25)
<pre>
  if (txtUsername.getText().equals("") || txtPassword.getText().equals("")) {
            JOptionPane.showMessageDialog(null, "Isi semua data terlebih dahulu!");
        } else {
            String user, pw;
            user = txtUsername.getText();
            pw = txtPassword.getText();

            EntityManagerFactory emf = Persistence.createEntityManagerFactory("LatihanSemester3PU");
            EntityManager em = emf.createEntityManager();
            em.getTransaction().begin();

            Pwlogin y = em.find(Pwlogin.class, user);
            if (y != null) {
                JOptionPane.showMessageDialog(null, "Username sudah ada, coba gunakan username lain");
                bersih();
            } else {
                Pwlogin x = new Pwlogin();
                x.setUsername(user);
                x.setPassword(pw);
                em.persist(x);

                em.getTransaction().commit();
                JOptionPane.showMessageDialog(null, "Sukses dibuat");

                bersih();
                formLogin z = new formLogin();
                z.setVisible(true);
                this.dispose();
            }
            em.close();
            emf.close();
        }
</pre>
### 5.	Coba jalankan program anda pada file formLogin
![image](https://github.com/user-attachments/assets/83f6455b-f25d-418d-b8af-df0c11acc1bf)
Jika sebelumnya anda belum memiliki username dan password, akan muncul notif jika username dan password yang anda masukkan salah, klik pada create new account untuk mendafkarkan username dan password anda.

### 6.	Buat username dan password baru anda, berikut adalah tampilan Ketika anda klik create new account, kemudian simpan. 
![image](https://github.com/user-attachments/assets/a099cb32-1bc2-4b30-a7d1-758a697173cd)
Anda akan otomatis diarahkan pada halaman login setelah berhasil membuat username dan password baru.

![image](https://github.com/user-attachments/assets/7c402495-e621-4a61-85de-928626161273)
Jika berhasil akan muncul notif popup jika berhasil menyimpan.

![image](https://github.com/user-attachments/assets/fb82d62e-3865-48d5-995a-dee3f8d9de9b)
Anda akan diarahkan Kembali pada halaman login, dan masukkan ulang username dan password yang sudah anda buat sebelumnya kemudian klik LOGIN.

![image](https://github.com/user-attachments/assets/145a7f4a-a24c-4b7e-84a6-4244b4e2a7a1)
Jika sukses akan ada notif selamat dating dan diarahkan pada halaman entitas matakuliah.

![image](https://github.com/user-attachments/assets/7d080b48-203e-4521-b82d-75083fb473ef)

## Terima Kasih Sekian Penjelasan Untuk Materi Form Login dengan Persistance.


