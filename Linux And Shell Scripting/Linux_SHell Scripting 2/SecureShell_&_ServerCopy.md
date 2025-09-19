
# SSH and SCP Learning Notes

## 🔑 SSH (Secure Shell)
- **Definition:**  
  SSH is a secure protocol used to connect to remote servers or machines over a network.  
- **How it works:**  
  - Uses **asymmetric cryptography** (public/private key pairs) or passwords.  
  - All communication is **encrypted**.  
- **Purpose:**  
  - Secure remote login into another machine.  
  - Run commands on a remote server.  
  - Forward/tunnel network traffic securely.  

### Example Command:
```bash
ssh user@server_ip
````

---

## 📂 SCP (Secure Copy Protocol)

* **Definition:**
  SCP is used to **securely copy files** between client and server.
* **How it works:**

  * Uses SSH under the hood for authentication & encryption.
  * Works for both **uploading (push)** and **downloading (pull)** files.

### Example Commands:

* **Push file to server:**

```bash
scp -i client-key-file.pem file_name.txt server_name:folder_location_on_server/where_to_put_file
```

* **Pull file from server:**

```bash
scp -i client-key-file.pem server_name:folder_location_of_server/file.txt client_folder_location/where_to_put_file
```

---

## ⚡ Quick Difference

* **SSH** → Login to a remote machine securely.
* **SCP** → Copy files between client & server securely.

```
