# 📦 Biossmann Odoo 18.0

This repository contains custom modules and configuration for the **Biossmann Odoo 18.0** instance.  
It includes production modules, utility scripts, and documentation to help developers set up their environment quickly.

---

## 🚀 Setup Instructions

### 1. Clone the Repository
```bash
git clone <repo-url>
cd biossmann-odoo
```

### 2. Install Dependencies
Make sure you have the following installed:

- **Python 3.10+**
- **PostgreSQL**
- **Odoo 18.0**
- Required Python packages (install via `requirements.txt` if provided).

---

## 🔗 Create Symlink for `PuntoVentaFolioTracker`

In order for Odoo to recognize the `PuntoVentaFolioTracker` module, we link it into the `addons` directory using a **symbolic link**.  
This avoids **code duplication** and keeps **development/production** in sync.

### 🖥 On Windows (Run as Administrator in Command Prompt)
```powershell
mklink /D "C:\biossmann-odoo\odoo-18.0\biossmann_addons" "C:\biossmann-odoo\production\PuntoVentaFolioTracker"
```

### 💻 On Linux / macOS
```bash
ln -s /home/<user>/biossmann-odoo/production/PuntoVentaFolioTracker /home/<user>/biossmann-odoo/odoo-18.0/biossmann_addons
```

### 🔹 Explanation
- **First path** → The destination (`odoo-18.0/biossmann_addons`), where Odoo expects custom modules.  
- **Second path** → The source (`production/PuntoVentaFolioTracker`), which contains the actual code.  
- `/D` (Windows only) → Specifies that the link is for a directory.  
- `ln -s` (Linux/macOS) → Creates a symbolic link.  

### ⚠️ Notes
1. Ensure the folder `odoo-18.0/biossmann_addons` does **not already exist** as a normal directory (delete or rename it if needed).  
2. On **Windows**, run the command as **Administrator**.  
3. On **Linux/macOS**, ensure you have correct permissions.  

### ✅ Result
After running the command, Odoo will load the `PuntoVentaFolioTracker` module as if it were inside the standard `addons` folder.

---

## 🛠 Development Guidelines

- Follow **branch naming conventions**:  
  - `feature/<name>` for new features.  
  - `bugfix/<name>` for fixes.  
  - `hotfix/<name>` for urgent patches.  

- Keep commits **atomic and descriptive**. Example:  
```bash
git commit -m "feature: add folio tracker validation on POS orders"
```

- Use **pull requests** for merging into `main` or `production`.

---

## 📂 Repository Structure

> Reflects the current root layout of the repository.

```text
biossmann-odoo/
├── backup/        # Database dumps, backups, and archives
├── docker/        # Dockerfiles, docker-compose, and environment configs
├── odoo-18.0/     # Odoo installation folder (core + addons path)
├── production/    # Production-ready code and custom modules
├── .gitignore     # Git ignore rules
└── README.md      # Project documentation (this file)
```

> Note: `odoo-18.0/biossmann_addons` is expected to be a **symlink you create locally** (not tracked by git).

---

## 🐳 Running with Docker

If you prefer using Docker for development or deployment, use the provided configuration.

### 1. Build the Docker image
```bash
docker build -t biossmann-odoo docker/
```

### 2. Run Odoo container
```bash
docker run -d   --name biossmann-odoo   -p 8069:8069   -v $(pwd)/odoo-18.0:/mnt/odoo   -v $(pwd)/production:/mnt/production   biossmann-odoo
```

### 3. Run with docker-compose (recommended)
If a `docker-compose.yml` exists inside the `docker/` folder:
```bash
cd docker
docker-compose up -d
```

This will start Odoo and any related services (like PostgreSQL) as defined.

---

## 📜 License
This project is licensed under the **MIT License** unless otherwise stated in individual module directories.
