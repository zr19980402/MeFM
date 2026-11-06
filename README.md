# Mechanically Consistent Foundation Model for General Loading Conditions

This repository contains the research code and retained experiment outputs for
the paper **Mechanically consistent foundation model for general loading
conditions**. It is a collection of case-specific research implementations.


## Repository Layout

| Path | Contents |
| --- | --- |
| `220_MeFM_footing` | Section 2.2 |
| `231_MeFM_plate` | Section 2.3.1 |
| `232_MeFM_beam` | Section 2.3.2 |
| `233_MeFM_gripper` | Section 2.3.3 |
| `240_MeFM_label` | Section 2.4 |
| `250_MeFM_paradigm` | Section 2.5 |
| `260_MeFM_LoRA` | Section 2.6 |
| `270_MeFM_comparison` | Section 2.7 |

Each experiment directory contains its own package, configuration, data, and outputs.

## System Requirements

- Operating system: Ubuntu 22.04
- Python: 3.12
- PyTorch: 2.8.0
- CUDA toolkit: 12.8
- GPU: NVIDIA A800 80 GB (NVLink), one GPU
- CPU: 18-core Intel Xeon Platinum 8374C

## Installation

```powershell
python -m pip install --upgrade pip
python -m pip install -r requirements.txt
```

## Training and Evaluation Commands


- Train from Scratch： Start training without resuming from a previous checkpoint:

```powershell
python train.py --resume=
```

- Resume Training： Resume training from an existing checkpoint:

```powershell
python train.py --resume <path>/lbfgs_latest.pth
```

- Evaluate a Trained Model： Evaluate the model under all available scenarios:

```powershell
python evaluate_model.py \
    --checkpoint <path>/lbfgs_best.pth \
    --scenario all
```

- Additional parameter：

To force the regeneration of reference solutions during evaluation: --force-reference
To save logs, checkpoints, and other generated files to a custom directory: --output-dir

## Notes

- Each experiment expects the mesh format, boundary-node conventions, loading-case structure, and FEM reference format specified in its own configuration files. Generate the required mesh by running:

  ```bash
  python Quadmesh.py
  ```

- In `260_MeFM_LoRA`, the original model is frozen during fine-tuning, and the generated results are saved in an `output_lora_*` directory. All other experiments save their results in an `output_*` directory.
