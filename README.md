This project sets up a reverse proxy architecture using **Docker**, **Traefik**, **Nginx**, and **Terraform**, where the services are hosted on **domain names** instead of IP addresses or port numbers. Everything is automated with Terraform, and the setup is entirely local (no cloud dependency).

> ✅ In previous projects, we exposed apps using public IP and ports (e.g., `http://<public-ip>:8080`).  
> 🆕 In this project, we access services using custom domain names like:
>
> - **http://traefik.localdns.xyz**
> - **http://www.45ddvx39.localdns.xyz**

No IPs. No ports. Just neat domain-based access — just like real-world production.

---

## 🛠️ Tech Used

- **Terraform** – for infrastructure as code (IaC)
- **Docker** – to run containers
- **Traefik** – for routing traffic via domain names
- **Nginx** – as a sample web server
- **/etc/hosts** – for local domain resolution

---

## 🌐 Domain Note

We used domains like:

- `traefik.localdns.xyz`
- `www.45ddvx39.localdns.xyz`

These aren't public domains. They're **mapped in your `/etc/hosts`** file to your local machine so that the browser treats them like real URLs. You don't need to access via port or public IP.

---

## 📁 Folder Structure

```
.
├── configs/
│   ├── app.conf                # Nginx site config
│   ├── nginx.conf              # Main Nginx config
│   └── traefik_dynamic.toml    # Traefik route config
├── html/
│   └── index.html              # Web content for Nginx
├── main.tf                     # Terraform: defines Docker containers
├── providers.tf                # Terraform: Docker provider
├── variables.tf                # Terraform: input variables
├── outputs.tf                  # Terraform: outputs after apply
```

---

## ⚙️ How to Use

### 1. Clone the Repo

```bash
git clone https://github.com/yourusername/your-repo.git
cd your-repo
```

### 2. Set Up `/etc/hosts`

Edit your system's `/etc/hosts` file and add:

```
127.0.0.1 traefik.localdns.xyz
127.0.0.1 www.45ddvx39.localdns.xyz
```

> This maps the domain names to your local machine.

### 3. Initialize Terraform

```bash
terraform init
```

### 4. Apply the Terraform Plan

```bash
terraform apply
```

Type `yes` when asked.

---

## ✅ What Happens

- Docker provider is initialized via Terraform.
- Traefik container is launched as reverse proxy on port 80.
- Nginx container is launched serving HTML content.
- Both containers are networked together.
- Routing rules in `traefik_dynamic.toml` send traffic to the right container based on domain name.

---

## 🔍 Access the Sites

Once applied and running, open these in your browser:

- **http://traefik.localdns.xyz** → Traefik dashboard (these website as given by the owner of this repo so i used by as it goes)
- **http://www.45ddvx39.localdns.xyz** → Nginx-served webpage

---

## 🧼 To Clean Up

```bash
terraform destroy
```

Type `yes` to confirm. This will remove the containers and network.

---

## 📦 Why This Project Matters

This project is designed to reflect how **real production systems** route traffic using domains, not ports. It also shows how to:

- Automate container deployment with Terraform

- Avoid using ports/IPs for access
- Keep configs modular and readable
- Practice domain-based service discovery in a local setup

