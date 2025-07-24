medical-sr-project/
│
├── README.md
├── requirements.txt
├── .gitignore
│
├── notebooks/                      # For Jupyter notebooks
│   ├── 1_generate_synthetic.ipynb     # For data generation
│   ├── 2_pretrain_sr_model.ipynb      # Pretraining on synthetic data
│   ├── 3_finetune_asl_c13.ipynb       # Domain-specific fine-tuning
│   └── 4_evaluation_visualization.ipynb
│
├── src/              
             # Python scripts (for modularity)
│   ├── models/
│   │   ├── real_esrgan_model.py       # Wrapper for ESRGAN
│   │   ├── swinir_model.py            # Transformer-based model
│   │   └── loss_functions.py          # ASL/C13-specific loss functions
│   ├── data/
│   │   ├── dataset_loader.py          # Data loading logic
│   │   └── augmentations.py           # Data augmentation utils
│   └── train_utils/
│       ├── trainer.py                # Training loop logic
│       └── scheduler.py             # Learning rate + freezing scheduler
│
├── data/                         # Not pushed to GitHub (add to .gitignore)
│   ├── raw/
│   ├── synthetic/
│   └── processed/
│
├── checkpoints/                 # Model weights (also .gitignore)
│   ├── pretrained_esrgan.pth
│   └── fine_tuned_asl.pth
│
└── scripts/                     # CLI scripts for running training/eval
    ├── train_sr.py
    ├── finetune_asl.py
    └── eval_model.py


| Model Type                        | Name                     | Main Job                                          | Use In Training or Testing?   | Role                     |
| --------------------------------- | ------------------------ | ------------------------------------------------- | ----------------------------- | ------------------------ |
| 1. Super-Resolution CNN + GAN     | Real-ESRGAN              | Turn low-res images into sharp high-res           | ✅ Used in training & testing  | SR model                 |
| 2. Transformer-based SR           | SwinIR / HAT             | Do the same, but with better global understanding | ✅ Used in training & testing  | SR model                 |
| 3. GANs (optional for data synth) | Any GAN (e.g., StyleGAN) | Create **fake medical images** for training       | ✅ Only used in training phase | Synthetic data generator |

