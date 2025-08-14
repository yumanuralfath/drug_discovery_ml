# 🧪 Drug Discovery ML

Pipeline machine learning sederhana untuk *drug discovery* berbasis data dari [ChEMBL](https://www.ebi.ac.uk/chembl/).  
Project ini menggunakan **Poetry** untuk manajemen dependensi dan mendukung eksperimen interaktif melalui **Jupyter Notebook**.

---

## 📂 Struktur Project

```
drug-discovery-ml/
├── drug_discovery_ml/          # Package utama
├── notebooks/                  # Notebook Jupyter
│   └── 01-fetch-data.ipynb
├── pyproject.toml             # Konfigurasi Poetry & dependensi
├── poetry.lock                # Versi pasti dari dependensi
└── README.md
```

---

## 🛠 Persyaratan

- Python **3.13** (direkomendasikan via pyenv atau conda)
- [Poetry](https://python-poetry.org/) (≥ 2.0.0)
- **Opsional:** [Conda](https://docs.conda.io/en/latest/) untuk instalasi RDKit

---

## 🚀 Instalasi

### 1. Clone repository

```bash
git clone https://github.com/username/drug-discovery-ml.git
cd drug-discovery-ml
```

### 2. Install dependensi utama

```bash
poetry install
```

Jika ingin menginstall Jupyter dan library ML:

```bash
poetry add notebook ipykernel pandas numpy scikit-learn matplotlib tqdm chembl-webresource-client
```

### 🧬 (Opsional) Instal RDKit

Untuk parsing SMILES dan membuat fingerprint molekul, install RDKit via conda:

```bash
conda create -n chem python=3.13
conda activate chem
conda install -c conda-forge rdkit
```

> **Catatan:** RDKit via pip tidak direkomendasikan karena masalah kompatibilitas.

---

## 📓 Menjalankan Jupyter Notebook

### 1. Tambahkan kernel Jupyter untuk environment Poetry

```bash
poetry run python -m ipykernel install --user --name=drug-discovery-ml --display-name "Python (drug-discovery-ml)"
```

### 2. Jalankan Jupyter

```bash
poetry run jupyter notebook
```

Atau:

```bash
poetry run jupyter lab
```

### 3. Pilih kernel

Di Jupyter UI:
**Kernel** → **Change Kernel** → **Python (drug-discovery-ml)**

---

## 📑 Notebook yang tersedia

- **01-fetch-data.ipynb** – Mengambil data bioactivity dari ChEMBL dan menampilkan visualisasi awal.
- **(Opsional) 02-train-model.ipynb** – Melatih model ML sederhana (Random Forest) untuk memprediksi aktivitas molekul.

---

## 🔍 Contoh penggunaan di notebook

```python
from chembl_webresource_client.new_client import new_client
import pandas as pd

target = "CHEMBL203"  # EGFR example
activity = new_client.activity
res = activity.filter(target_chembl_id=target).only(
    ["molecule_chembl_id", "canonical_smiles", "standard_value"]
)[:50]

df = pd.DataFrame(res)
df.head()
```