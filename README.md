# 🚀 CareerHub - Modern Recruitment & Job Board Platform

<p align="center">
  <img src="https://img.shields.io/badge/WordPress-7.1.3-21759B?style=for-the-badge&logo=wordpress&logoColor=white" alt="WordPress" />
  <img src="https://img.shields.io/badge/Docker-Desktop-2496ED?style=for-the-badge&logo=docker&logoColor=white" alt="Docker Desktop" />
  <img src="https://img.shields.io/badge/MariaDB-10.11-003545?style=for-the-badge&logo=mariadb&logoColor=white" alt="MariaDB" />
  <img src="https://img.shields.io/badge/PHP-8.3-777BB4?style=for-the-badge&logo=php&logoColor=white" alt="PHP" />
  <img src="https://img.shields.io/badge/Elementor-Builder-92003B?style=for-the-badge&logo=elementor&logoColor=white" alt="Elementor" />
</p>

> **CMS Capstone Project**  
> An enterprise-grade, fully responsive online job recruitment and employment portal built on top of **WordPress** and containerized using **Docker Desktop & Docker Compose** (WordPress App, MariaDB, and phpMyAdmin).

---

## 📸 Preview

<p align="center">
  <img src="docs/screenshots/careerhub-homepage.png" alt="CareerHub Homepage Preview" width="100%" style="border-radius: 8px; box-shadow: 0 4px 20px rgba(0,0,0,0.15);" />
</p>

---

## ✨ Key Features

### 🎯 1. For Job Seekers
- **Smart Job Search & Filtering:** Multi-criteria real-time filtering directly on the Hero banner (by keywords, position, skillsets, and geographical location).
- **Featured Top Jobs:** Curated listings highlighting top career opportunities with key metadata (company logo, role, contract type, location, and brief summary).
- **In-Depth Job Details:** Clean layout detailing responsibilities, qualifications, benefits, and application deadlines.
- **Online Job Application:** Seamless CV submission and application forms routed directly to hiring teams.
- **Career Guide & Blog:** Informative articles covering AI-era hiring trends, interview strategies, CV optimization, and workplace communication skills.
- **Newsletter Subscription:** Automated email alerts for new job openings.

### 🏢 2. For Employers
- **Job Submission Portal (`Submit Job`):** Intuitive multi-step form for publishing new job vacancies with customizable requirements.
- **Employer Dashboard:** Centralized panel to manage active postings, review applicants, and update hiring statuses.
- **Company Profiles:** Dedicated brand landing pages showcasing mission, office culture, and open positions.

### ⚙️ 3. Architecture & Tech Highlights
- **Containerized Environment:** Fully reproducible local development powered by Docker Compose.
- **High-Performance Database:** MariaDB 10.11 with persistent volume storage and phpMyAdmin interface.
- **Visual Page Building:** Integrated with **Elementor**, allowing flexible drag-and-drop landing page design and custom CSS styling.
- **Accessibility (a11y):** Integrated with One Click Accessibility tools ensuring WCAG-compliant readability and navigation.
- **SMTP & Communications:** Integrated with WP Mail SMTP and Contact Form 7 for reliable transactional email delivery.

---

## 📂 Project Structure

```text
JobScout/
├── .env                  # Environment configuration (ports, database credentials)
├── .env.example          # Sample environment variables template
├── docker-compose.yml    # Multi-container orchestration (WordPress, MariaDB, phpMyAdmin)
├── database.sql          # Pre-configured, production-ready SQL database dump
├── docs/                 # Documentation and high-resolution screenshots
│   └── screenshots/
│       └── careerhub-homepage.png
├── docker/
│   └── uploads.ini       # Optimized PHP runtime settings (64MB upload, 256MB memory)
└── wordpress/            # WordPress core & source code (mounted directly into container)
    └── wp-content/
        ├── plugins/      # WP Job Manager, Elementor, Newsletter, SMTP, a11y...
        └── themes/       # Custom JobScout theme
```

---

## 🛠️ Quick Start & Installation

### Prerequisites
- Install and launch **[Docker Desktop](https://www.docker.com/products/docker-desktop/)** (Supports Windows WSL2, macOS, and Linux).
- Git installed on your local machine.

---

### Step 1: Map Local Domain (Recommended)
To support WordPress permalinks and internal routing seamlessly, map the project domain to your local loopback address:

- **Windows:** Open `C:\Windows\System32\drivers\etc\hosts` with Administrator privileges.
- **macOS / Linux:** Run `sudo nano /etc/hosts` in your terminal.

Add the following line to the file and save:
```text
127.0.0.1 wordpress.local
```

---

### Step 2: Configure Environment Variables
Copy `.env.example` to create your local `.env` file:

```bash
# Windows PowerShell
Copy-Item .env.example .env

# macOS / Linux
cp .env.example .env
```
*(Default settings configure `WP_PORT=80`, `PMA_PORT=8081`, and pre-configured MariaDB credentials).*

---

### Step 3: Spin Up Containers
Launch the Docker stack in detached mode:

```bash
docker compose up -d
```
> The startup sequence will build the internal bridge network and launch `wordpress_db`, `wordpress_app`, and `wordpress_pma`.

---

### Step 4: Import Sample Database
Once the database container reports **healthy**, import the pre-configured dataset:

```bash
# Windows PowerShell / CMD:
cmd /c "docker exec -i wordpress_db mariadb -u wp_user -pwp_user_password cms-cuoiky < database.sql"

# macOS / Linux:
docker exec -i wordpress_db mariadb -u wp_user -pwp_user_password cms-cuoiky < database.sql
```

---

## 🌐 Access Endpoints

| Service | URL | Notes |
| :--- | :--- | :--- |
| **CareerHub Web Portal** | [http://wordpress.local](http://wordpress.local) | Primary public website |
| **WordPress Admin Panel** | [http://wordpress.local/wp-admin](http://wordpress.local/wp-admin) | Administrative management portal |
| **phpMyAdmin** | [http://localhost:8081](http://localhost:8081) | Web-based database management |

---

## 🔑 Default Credentials

### 1. WordPress Admin Dashboard
- **Login URL:** `http://wordpress.local/wp-login.php`
- **Username:** `root`
- **Password:** `admin123`

### 2. Demo User Accounts (Role Testing)
| Role | Username | Password | Permissions |
| :--- | :--- | :--- | :--- |
| **Employer** | `employer_demo` | `demo123` | Post jobs, manage listings, view applicants |
| **Job Seeker** | `jobseeker_demo` | `demo123` | Search listings, save jobs, submit applications |

### 3. phpMyAdmin Database Access
- **Host / Server:** `db`
- **Root Account:** `root` / `root_secret_password`
- **Application User:** `wp_user` / `wp_user_password`
- **Database Name:** `cms-cuoiky`

---

## 💻 Common Management Commands

```bash
# Check container status
docker compose ps

# View live WordPress application logs
docker compose logs -f wordpress

# Gracefully stop all services
docker compose down

# Restart the entire stack
docker compose restart

# Export latest database changes to database.sql
cmd /c "docker exec wordpress_db mariadb-dump -u wp_user -pwp_user_password cms-cuoiky > database.sql"

# Wipe database volume completely to reset from scratch
docker compose down -v
```

---

## 📄 License
This project is developed for educational purposes as part of the Content Management System (CMS) capstone curriculum.
