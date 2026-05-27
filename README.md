# 📦 Data Versioning Using DVC

A hands-on project demonstrating **Data Version Control (DVC)** for tracking and managing dataset changes alongside Git. This project showcases how to version large data files, reproduce data pipelines, and switch between different dataset snapshots — all without bloating your Git repository.

---

## 🎯 Objective

In machine learning projects, data changes as frequently as code. Traditional Git is not designed for large binary/data files. **DVC** bridges this gap by:

- Tracking data files with lightweight `.dvc` metafiles in Git
- Storing actual data in a configurable remote storage (local, S3, GCS, Azure, etc.)
- Enabling seamless checkout of data at any Git commit — just like code

This project demonstrates the full DVC workflow using an **E-Commerce Customer dataset**.

---

## 🏗️ Project Structure

```
Data-Versioning-Using-DVC/
│
├── .dvc/                    # DVC configuration directory
│   ├── .gitignore
│   └── config               # Remote storage configuration
│
├── .dvcignore               # Patterns for DVC to ignore
│
├── data/
│   ├── .gitignore           # Ensures raw data isn't tracked by Git
│   ├── customer.csv         # Versioned dataset (tracked by DVC)
│   └── customer.csv.dvc     # DVC metafile (tracked by Git)
│
├── src/
│   └── data-ingestion.py    # Data ingestion & preprocessing script
│
└── README.md
```

---

## 📊 Dataset

The project uses the [E-Commerce Customers](https://github.com/araj2/customer-database) dataset, which contains customer session and membership data including:

| Feature | Description |
|---------|-------------|
| `Email` | Customer email address |
| `Address` | Customer mailing address |
| `Avatar` | Avatar color preference |
| `Avg. Session Length` | Average in-store session duration |
| `Time on App` | Time spent on mobile app (minutes) |
| `Time on Website` | Time spent on website (minutes) |
| `Length of Membership` | Membership duration (years) |
| `Yearly Amount Spent` | Total annual spending ($) |

---

## ⚙️ Data Pipeline

The `src/data-ingestion.py` script performs the following steps:

1. **Fetches** the raw dataset from a public GitHub URL
2. **Selects** numerical features (columns 3 onwards)
3. **Filters** customers with `Length of Membership > 3` years
4. **Exports** the processed data to `data/customer.csv`

---

## 🚀 Getting Started

### Prerequisites

- Python 3.8+
- Git
- DVC (`pip install dvc`)

### Installation

```bash
# Clone the repository
git clone https://github.com/Aman-Husain-123/Data-Versioning-Using-DVC.git
cd Data-Versioning-Using-DVC

# Install dependencies
pip install pandas numpy dvc
```

### Run the Data Ingestion Pipeline

```bash
python src/data-ingestion.py
```

### Configure DVC Remote Storage

```bash
# Initialize DVC (already done in this repo)
dvc init

# Add a remote storage location
dvc remote add -d myremote /path/to/your/storage

# Push data to remote
dvc push
```

---

## 🔄 DVC Workflow — Version Your Data

### Track a Data File

```bash
# Add data file to DVC tracking
dvc add data/customer.csv

# Stage the DVC metafile and .gitignore changes
git add data/customer.csv.dvc data/.gitignore

# Commit
git commit -m "Track customer dataset with DVC"
```

### Switch Between Data Versions

This is the core power of DVC — **time-travel through your data**:

```bash
# View commit history
git log --oneline

# Checkout a previous code + data snapshot
git checkout <commit-hash>
dvc checkout

# The data/customer.csv now matches that exact point in time!
```

### Push & Pull Data from Remote

```bash
# Push versioned data to remote storage
dvc push

# Pull data on a different machine
dvc pull
```

---

## 📝 Experiment Log

| Commit | Description | Data Snapshot |
|--------|-------------|---------------|
| `916624e` | Initial commit | Repository setup |
| `a2f573b` | Folder is been added | Project structure created |
| `9b0b7e0` | Commit with DVC config files | DVC initialized & configured |
| `8644ba7` | Add first experiment | First dataset version tracked |
| `268758f` | Add second experiment | Updated dataset version |

---

## 🛠️ Tech Stack

| Tool | Purpose |
|------|---------|
| **Git** | Source code version control |
| **DVC** | Data version control & pipeline management |
| **Python** | Data ingestion & preprocessing |
| **Pandas** | Data manipulation & analysis |
| **NumPy** | Numerical computing |

---

## 📚 Key Concepts Demonstrated

- **`.dvc` files** — Lightweight metafiles that store MD5 hashes pointing to actual data in remote storage
- **`dvc checkout`** — Syncs the data files in your workspace to match the current Git commit
- **`dvc push / pull`** — Transfers data between local cache and remote storage
- **`dvc remote`** — Configurable storage backends (local filesystem, AWS S3, Google Cloud, Azure, SSH, etc.)
- **Data & Code in sync** — Every Git commit has a corresponding data snapshot via DVC

---

## 🤝 Contributing

1. Fork the repository
2. Create your feature branch (`git checkout -b feature/new-experiment`)
3. Commit your changes (`git commit -m 'Add new data experiment'`)
4. Push to the branch (`git push origin feature/new-experiment`)
5. Open a Pull Request

---

## 📄 License

This project is open source and available for learning and educational purposes.

---

## 👤 Author

**Aman Husain**
- GitHub: [@Aman-Husain-123](https://github.com/Aman-Husain-123)

---

> 💡 **Tip:** Use `git log --oneline` followed by `git checkout <hash>` + `dvc checkout` to explore how the dataset evolved across experiments!