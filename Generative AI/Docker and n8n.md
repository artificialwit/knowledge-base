# 🚀 n8n Docker Command Cheat Sheet

Manage your **n8n** instance easily with these Docker commands.

---

## 🔍 Check Docker Containers

| Description                  | Command                     |
|------------------------------|------------------------------|
| Show running containers      | `sudo docker ps`            |
| Show all containers (stopped too) | `sudo docker ps -a`    |

---

## ▶️ Start / Stop / Restart n8n

| Description            | Command                    |
|------------------------|----------------------------|
| Start n8n              | `sudo docker start n8n`    |
| Stop n8n               | `sudo docker stop n8n`     |
| Restart n8n            | `sudo docker restart n8n`  |

---

## 📦 Manage Containers

| Description            | Command                    |
|------------------------|----------------------------|
| Remove n8n container   | `sudo docker rm n8n`       |
| View n8n logs          | `sudo docker logs n8n`     |

---

## 🚨 Run n8n Manually

If you need to manually run n8n:

```bash
sudo docker run -d \
  --name n8n \
  -p 5678:5678 \
  -v ~/.n8n:/home/node/.n8n \
  -e GENERIC_TIMEZONE="Asia/Kolkata" \
  --restart unless-stopped \
  n8nio/n8n
