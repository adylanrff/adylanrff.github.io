---
title:  "Developer Note: SLAP That Function!"
description: Jangan lupa pakai prinsip ini kalau ingin berkolaborasi dengan mudah! 
tags: [30daysofwriting]
---

Sebenarnya apa sih yang membuat seorang developer itu dibilang jago? 

Bisa bikin REST API sambil merem? Bisa buat model regresi linier tanpa library? Bisa pakai tools termutakhir yang orang-orang nggak pernah denger? Sebenarnya bisa apa aja ya, tergantung intepretasi kita masing-masing. Kalau menurut gue, developer yang jago itu adalah orang yang bisa nulis kode dengan *simple stupid*.

Lah kok malah dengan nulis dengan *bego*? 

Maksudnya *simple stupid* di sini adalah dia bisa nulis kode yang kalau orang sedang baca kode yang dia tulis orang tersebut bisa langsung bilang "*ooh*". Mungkin malah orang akan bertanya-tanya "*ah katanya jago kok gini doang ngodingnya?*" Padahal justru itu yang dicari: **code clarity and simplicity**. Hal ini akan mempercepat *development* sebuah *project* dan tentu saja produktivitas tim akan meningkat dengan mudahnya kode untuk dibaca dan dimengerti oleh anggota tim. 

Salah satu hal yang mau gue highlight saat kita menulis kode adalah prinsip **SLAP: Single Level of Abstraction Principle**. Menurut gue ini penting banget buat kita semua untuk tahu.

## Apa itu SLAP?

Intinya SLAP itu adalah membuat sebuah fungsi agar cuma punya satu level abstraksi saja. Agar lebih gampang dimengerti langsung aja kita pakai kode. Ini contoh yang gue buat, kalau misalnya ada salah di *syntax* atau apapun tolong kasih tahu gue segera ya!

## Contoh Penerapan SLAP

Coba perhatikan contoh kode untuk memastikan bahwa email, address, username, dan password sebuah registrasi valid di bawah ini

```
def verify_registration(email, address, username, password):
  // Validasi email
  res = db_conn.query("SELECT * from users WHERE email = $1", email)
  is_email_valid_ = len(res) == 0

  // Validasi username
  res = db_conn.query("SELECT * from users WHERE username = $1", username)
  is_username_valid = len(res) == 0

  // Validasi address
  is_address_valid = len(address)>0

  // Validasi password
  is_password_valid = re.match(r'[A-Za-z0-9@#$%^&+=]{8,}', password)

  return is_email_valid_ and is_username_valid and is_address_valid and is_password_valid
```

Kalau menurut *SLAP*, kode di atas melanggar prinsip abstraksi tunggal. Kalau diperhatikan, kode di atas mencampur adukkan interaksi ke database dan verifikasi-verifikasi lainnya. Kalau begitu, abstraksinya sudah nggak tunggal lagi. Ada abstraksi di level *database*, ada abstraksi di level *app*. 

Proses yang gua suka tapi selalu paling memusingkan adalah *refactoring*, tapi ayo kita coba sama-sama *refactor* kode di atas sehingga mematuhi *SLAP*.

```
def verify_registration(email, address, username, password):
  is_email_valid = verify_email(email) 
  is_username_valid = verify_username(username) 
  is_address_valid = verify_address(address) 
  is_password_valid = verify_password(password)
  
  return is_email_valid_ and is_username_valid and is_address_valid and is_password_valid

def verify_email(email):
  res = db_conn.query("SELECT * from users WHERE email = $1", email)
  return len(res) == 0
  
def verify_username(username):
  res = db_conn.query("SELECT * from users WHERE username = $1", username)
  return len(res) == 0

def verify_address(address):
  return len(address)>0

def verify_password(password):
  return re.match(r'[A-Za-z0-9@#$%^&+=]{8,}', password)
```

Dengan dipisahnya masing-masing validasi sehingga punya fungsinya masing-masing, abstraksi untuk setiap fungsi pada kode di atas sudah pasti menjadi *single abstraction*. Pada fungsi `verify_registration`, hanya ada pemanggilan fungsi-fungsi verifikasi untuk masing-masing komponen yang harus divalidasi. Dengan begini, *SLAP* sudah terpenuhi. 

This should be a quote for us, programmers, to live by:

> “Any fool can write code that a computer can understand. Good programmers write code that humans can understand.” – Martin Fowler

Sampai jumpa besok!