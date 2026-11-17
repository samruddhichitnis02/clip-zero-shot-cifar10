# Homework 11 — CLIP on CIFAR-10

**Model:** OpenAI CLIP ViT-B/32 (`open_clip`, `ViT-B-32-quickgelu`, `pretrained='openai'`) · **Data:** CIFAR-10 test split · **GPU:** RTX 3060 Laptop

| File | What it is |
|---|---|
| `HW11_CLIP_CIFAR10.ipynb` | Executed notebook (code + outputs + findings) |
| `HW11_CLIP_CIFAR10.html` | Same notebook as a standalone web page |
| `results/` | CSV/TXT/JSON metrics (`summary.json` has the headline numbers) |
| `results/figures/` | All plots (PNG) |
| `logs/clip_run.log` | Timestamped run log (all metrics) |
| `logs/nbconvert_execution.log` | Notebook execution log |
| `data/cifar10_test.parquet` | CIFAR-10 test split (HF mirror `uoft-cs/cifar10`) |

## Part 1 — Caption "a photo of a dog" vs 1,000 images (100 per class)
- Mean cosine similarity: **dog 0.261** vs 0.216 for the other classes. Order: dog > cat > deer > frog > bird > horse > airplane > automobile > ship > truck.
- 19 of the top-20 images are dogs. Retrieval P@10 / P@50 / P@100 = 0.90 / 0.88 / 0.78.
- With one caption per class, the matching caption has the highest mean similarity for **10/10** classes.

## Part 2 — Zero-shot classification (10,000 test images)
| | Single template | 18-prompt ensemble |
|---|---|---|
| Overall top-1 | 88.30 % | **89.83 %** |

Per-class accuracy (ensemble): horse 97.5, ship 95.4, automobile 94.3, truck 93.8, airplane 91.5, bird 89.1, dog 87.4, cat 85.3, deer 82.4, frog 81.6.
Top confusions: deer→horse (121), cat→dog (80), dog→cat (63), frog→cat (62).

## Reproduce
```
pip install -r requirements.txt
jupyter nbconvert --to notebook --execute --inplace HW11_CLIP_CIFAR10.ipynb
```
