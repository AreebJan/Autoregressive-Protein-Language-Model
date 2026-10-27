# Autoregressive Protein Language Model

Deep Learning Project — DTU, 02456 (2026)

## 1. Project Overview

This project investigates the generation of protein sequences using **autoregressive deep learning models**.

The objective is to train neural networks that learn the probability distribution of protein sequences and subsequently guide sequence generation towards specific protein families.

The project consists of three phases:

### Phase 1 — Autoregressive Models
- Implement a Multi-Layer Perceptron (MLP) that predicts the next amino acid based on the previous three amino acids.
- Implement an RNN (e.g., GRU or LSTM) or a causal Transformer.
- Train and evaluate the models.
- Generate new protein sequences.
- Evaluate generated sequences using ESMFold.

### Phase 2 — Classifier Guidance
- Train a classifier to predict protein family membership from complete and partial sequences.
- Combine the classifier with the autoregressive model.
- Investigate how guidance strength affects generated sequences.

### Phase 3 — Classifier-Free Guidance
- Train a conditional autoregressive model using label dropout.
- Implement classifier-free guidance.
- Compare guided and unguided generation.
- Evaluate protein family membership and structural plausibility.

The dataset will contain sequences from three protein families:

- Acylphosphatase (AcyP)
- Histidine-containing phosphocarrier protein (HPr)
- HU DNA-binding proteins (HU)

---

## 2. Project Structure

```text
Autoregressive-Protein-Language-Model/
│
├── README.md
├── requirements.txt
├── .gitignore
│
├── data/
│   ├── raw/                  # Original datasets
│   └── processed/            # Preprocessed datasets
│
├── notebooks/
│   └── exploration.ipynb     # Exploratory analysis
│
├── src/
│   ├── __init__.py
│   ├── data.py                # Data loading and tokenization
│   ├── train.py               # Model training
│   ├── generate.py            # Protein sequence generation
│   ├── evaluate.py            # Model evaluation
│   │
│   ├── models/
│   │   ├── __init__.py
│   │   ├── mlp.py             # MLP model
│   │   ├── rnn.py             # RNN / GRU / LSTM
│   │   └── transformer.py     # Transformer model
│   │
│   └── guidance/
│       ├── __init__.py
│       ├── classifier.py
│       └── classifier_free.py
│
├── tests/
│   └── test_data.py
│
├── outputs/
│   ├── checkpoints/          # Saved model weights
│   └── figures/              # Plots and visualizations
│
└── report/                    # Project report
```

---

## 3. Getting Started

### Step 1 — Install Git and Python

Make sure Git and Python are installed.

Check using:

```bash
git --version
python3 --version
```

If Git is missing on Ubuntu:

```bash
sudo apt update
sudo apt install git
```

We recommend using Python 3.11 or newer, subject to compatibility with the project's dependencies.

### Step 2 — Clone the Repository

Open a terminal and navigate to the directory where you want to store the project.

Clone the repository using SSH:

```bash
git clone git@github.com:AreebJan/Autoregressive-Protein-Language-Model.git
```

Alternatively, use HTTPS:

```bash
git clone https://github.com/AreebJan/Autoregressive-Protein-Language-Model.git
```

Navigate into the project:

```bash
cd Autoregressive-Protein-Language-Model
```

Open the project in VS Code:

```bash
code .
```

**Note:** SSH requires a configured GitHub SSH key. HTTPS may require GitHub authentication when pushing changes.

---

## 4. Python Environment

Each group member should create their own virtual Python environment.

This ensures that dependencies are installed locally without affecting other Python projects.

### Step 1 — Create the Environment

From the project directory:

```bash
python3 -m venv .venv
```

### Step 2 — Activate the Environment

On Ubuntu/Linux/WSL:

```bash
source .venv/bin/activate
```

On Windows PowerShell:

```powershell
.venv\Scripts\Activate.ps1
```

The terminal should now display:

```text
(.venv) user@computer:~/project$
```

### Step 3 — Install Dependencies

```bash
python -m pip install --upgrade pip
python -m pip install -r requirements.txt
```

**Important:** The current requirements were generated in an Ubuntu environment with CUDA-enabled PyTorch. Members using Windows, macOS, or different GPU configurations may need to install a compatible PyTorch build separately.

### Step 4 — Configure VS Code

1. Open VS Code.
2. Press `Ctrl + Shift + P`.
3. Search for `Python: Select Interpreter`.
4. Select `.venv/bin/python` (Linux/WSL) or `.venv\Scripts\python.exe` (Windows).

### Step 5 — Verify PyTorch

Run:

```bash
python -c "import torch; print(torch.__version__)"
```

To check GPU availability:

```bash
python -c "import torch; print(torch.cuda.is_available())"
```

Output:

- `True`: PyTorch can access a CUDA-compatible GPU.
- `False`: CUDA is unavailable in the current environment. CPU training may still work.

A GPU is recommended but not required for initial development.

---

## 5. Git — Basic Workflow

Git tracks changes to files, while GitHub allows us to share those changes with the group.

### Important Concepts

| Term | Meaning |
|---|---|
| Repository | The project and its version history |
| Clone | Download a local copy of the repository |
| Pull | Download and integrate changes from GitHub |
| Add | Select changes for the next commit |
| Commit | Save a snapshot of your changes locally |
| Push | Upload your commits to GitHub |
| Branch | An independent line of development |
| Merge | Combine changes from different branches |
| Pull Request | Request that changes be reviewed and merged |

### Before Starting Work

Always make sure you have the latest version:

```bash
git pull origin main
```

This downloads and integrates changes made by other group members.

### After Making Changes

Check which files have changed:

```bash
git status
```

Add your changes:

```bash
git add .
```

Commit your changes:

```bash
git commit -m "Describe what you changed"
```

Upload your changes:

```bash
git push origin main
```

### Example

Suppose you have implemented the amino acid tokenizer.

```bash
git pull origin main

# Make changes to src/data.py

git status
git add src/data.py
git commit -m "Implement amino acid tokenization"
git push origin main
```

Your changes are now available to the group.

### Important Rules When Collaborating

1. **Always pull before starting work.**
2. Communicate which files you are working on.
3. Avoid editing the same files simultaneously when working directly on `main`.
4. Write descriptive commit messages.
5. Never commit large datasets, virtual environments, or model checkpoints.
6. Never use `git push --force` on `main`.
7. If Git reports a merge conflict, resolve it before pushing. Ask another group member if you are unsure.

For larger features, using separate branches and Pull Requests is recommended.

---

## 6. Working with Branches (Optional)

Branches allow group members to work independently without modifying `main` directly.

Create a new branch:

```bash
git switch -c feature/mlp-model
```

Make your changes and commit:

```bash
git add .
git commit -m "Implement MLP model"
```

Push the branch:

```bash
git push -u origin feature/mlp-model
```

Then create a Pull Request on GitHub.

After the changes have been merged, return to `main`:

```bash
git switch main
git pull origin main
```

---

## 7. Working with Data

The project dataset will be placed in:

```text
data/raw/
```

Preprocessed datasets will be stored in:

```text
data/processed/
```

**Important:** Dataset files are excluded from Git by `.gitignore`.

This prevents large files from being uploaded unnecessarily.

Each group member must obtain the dataset separately.

Once the dataset is available, we will document its expected filenames and preprocessing steps here.

---

## 8. Model Development

The initial development workflow will be:

**Step 1 — Data Processing**

Implement amino acid tokenization, sequence encoding, and preparation of training examples.

**Step 2 — MLP**

Implement a neural network that predicts the next amino acid from the previous three amino acids.

**Step 3 — RNN or Transformer**

Implement a sequence model capable of learning dependencies across longer protein sequences.

**Step 4 — Training**

Implement training loops, loss calculations, validation, and model checkpointing.

**Step 5 — Generation**

Generate new protein sequences using trained autoregressive models.

**Step 6 — Guidance**

Implement classifier guidance and classifier-free guidance.

**Step 7 — Evaluation**

Evaluate generated sequences using family classification and protein structure prediction.

---

## 9. Running Tests

We use `pytest` for automated testing.

From the project directory:

```bash
python -m pytest
```

Tests will be added as the project develops.

---

## 10. Useful Git Commands

| Command | Description |
|---|---|
| `git status` | Show changed files |
| `git pull` | Get changes from GitHub |
| `git add .` | Stage all changes |
| `git add filename` | Stage a specific file |
| `git commit -m "message"` | Create a commit |
| `git push` | Upload commits |
| `git log --oneline -5` | Show the five latest commits |
| `git branch` | Show local branches |
| `git switch main` | Switch to main |
| `git diff` | Show unstaged changes |

---

## 11. Troubleshooting

### Git: Permission denied (publickey)

Your SSH key may not be configured with GitHub.

Use HTTPS instead or configure SSH authentication.

### Python: ModuleNotFoundError

Make sure your virtual environment is activated:

```bash
source .venv/bin/activate
```

Install the required packages:

```bash
python -m pip install -r requirements.txt
```

### CUDA is not available

Check GPU availability:

```bash
nvidia-smi
```

Then:

```bash
python -c "import torch; print(torch.cuda.is_available())"
```

CUDA requires a compatible NVIDIA GPU, driver, and PyTorch installation.

On WSL2, the NVIDIA driver should be installed on Windows.

### Git: Push rejected

Another group member may have pushed changes.

First try:

```bash
git pull origin main
```

Resolve any conflicts before pushing again:

```bash
git push origin main
```

Do not force-push to overwrite other members' work.

---

## 12. Project Status

- [x] Initialize GitHub repository
- [x] Create project directory structure
- [x] Set up initial Python environment and dependencies
- [ ] Obtain protein dataset
- [ ] Implement data preprocessing
- [ ] Implement MLP
- [ ] Implement RNN or Transformer
- [ ] Train and evaluate models
- [ ] Implement classifier guidance
- [ ] Implement classifier-free guidance
- [ ] Evaluate generated protein structures
- [ ] Complete project report

---

## 13. References

Project assignment: *Guidance of Autoregressive Protein Language Models*, DTU, 2026.

Relevant literature:

1. Bengio et al. (2003). *A Neural Probabilistic Language Model*.
2. Vaswani et al. (2017). *Attention Is All You Need*.
3. Ho & Salimans (2022). *Classifier-Free Diffusion Guidance*.
4. Lin et al. (2023). *Evolutionary-scale prediction of atomic-level protein structure with a language model*.