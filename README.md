# Mask6D — Mini Reproduction (Student Edition)

This repo gives you **end-to-end code** to satisfy a Stage‑3 deep dive: 
- **Self‑supervised pretraining** via masked point‑cloud reconstruction
- **Fine‑tuning** a pose head for 6D pose (translation + rotation)
- **Evaluation** with ADD‑S and simple plots
- **Synthetic dataset fallback** so you can run even without LINEMOD/YCB

> ⚠️ Educational, lightweight approximation of the Mask6D idea. Not the authors' official code.

## Quick Start

```bash
# 1) Install
pip install -r requirements.txt

# 2) (Optional) Prepare real data (LINEMOD/YCB) paths in config.json
# Otherwise we auto-create a small synthetic dataset (cubes, cylinders).

# 3) Pretrain (masked reconstruction)
python -m mask6d.train_pretrain --epochs 15 --mask_ratio 0.8 --out runs/pretrain

# 4) Fine-tune pose head (uses synthetic pose labels)
python -m mask6d.train_finetune --epochs 10 --pretrained runs/pretrain/encoder.pt --out runs/finetune

# 5) Plot & metrics
python -m mask6d.visualize --runs runs

# ADD‑S evaluation (on synthetic validation set automatically happens in fine-tune)
```

## Files

- `mask6d/models.py` — Encoder (PointNet‑lite), Decoder (MLP), PoseHead
- `mask6d/data.py` — Synthetic dataset + stubs for real datasets
- `mask6d/mask_utils.py` — Masking utilities
- `mask6d/metrics.py` — Chamfer distance, ADD/ADD‑S, quaternion helpers
- `mask6d/train_pretrain.py` — Pretraining loop
- `mask6d/train_finetune.py` — Fine‑tuning loop
- `mask6d/visualize.py` — Simple matplotlib plots (loss & AUC curves)
- `config.json` — Put dataset paths here if using real data

## Extra Files
- `presentation.txt (presentation.md)` — stage 3 presentation
- `Mask6D_Report.pdf` — A simple report

## License
For educational use.
