# DVC Dataset Versioning Workflow

## 1. DVC Remote

This practical uses a local DVC remote for storing dataset objects.

Remote name:

myremote

Remote location:

~/dvc-remote-storage

---

## 2. Dataset Versioning Workflow

The workflow used in this practical is:

dvc add → git add → git commit → dvc push

### Step 1: Track the dataset with DVC

```bash
python -m dvc add data/raw/iris_v1.csv