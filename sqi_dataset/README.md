# Wearable ECG quality: 10-second windows

| File | Purpose | Windows |
|---|---|---|
| `set_A.npz` | design your rule | 993 |
| `set_B.npz` | test it on different subjects | 724 |

Each file contains:

| Key | Content |
|---|---|
| `ecg` | windows × 2500 matrix: ECG in mV at 250 Hz (one row = one window) |
| `acc` | windows × 250 matrix: acceleration magnitude in g at 25 Hz, same windows |
| `label` | quality class of each window: 1, 2 or 3 |
| `fs_ecg`, `fs_acc` | sampling frequencies (Hz) |

Quality classes:

1. Clean signal: P, QRS and T clearly visible.
2. Increased noise: beats can be detected reliably (clear QRS), but morphology cannot be measured.
3. Unusable signal: QRS not recognisable.

```python
import numpy as np
d = np.load("set_A.npz")
ecg, acc, label = d["ecg"], d["acc"], d["label"]
fs_ecg, fs_acc = int(d["fs_ecg"]), int(d["fs_acc"])
```

**Source.** Windows extracted and resampled from: Nemcova A, Smisek R, Opravilová K, Vitek M, Smital L,
Maršánová L. *Brno University of Technology ECG Quality Database (BUT QDB)* (version 1.0.0). PhysioNet, 2020.
https://doi.org/10.13026/kah4-0w24. License: CC BY 4.0.
Goldberger A, et al. PhysioBank, PhysioToolkit, and PhysioNet. *Circulation* 101(23):e215–e220, 2000.
