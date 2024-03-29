# text2room_DE

Installing Pytorch 
Windows
pip3 install torch torchvision torchaudio --index-url https://download.pytorch.org/whl/cu121

Linux
pip3 install torch torchvision torchaudio

Installing Pytorch3D
Link should be "https://dl.fbaipublicfiles.com/pytorch3d/packaging/wheels/py310_cu121_pyt210/download.html"
This is using pytorch 210 and Cuda 121

import os
import sys
import torch
need_pytorch3d=False
try:
    import pytorch3d
except ModuleNotFoundError:
    need_pytorch3d=True
if need_pytorch3d:
    if torch.__version__.startswith("2.1.") and sys.platform.startswith("linux"):
        f"We try to install PyTorch3D via a released wheel."
        pyt_version_str=torch.__version__.split("+")[0].replace(".", "")
        version_str="".join([
            f"py3{sys.version_info.minor}_cu",
            torch.version.cuda.replace(".",""),
            f"_pyt{pyt_version_str}"
        ])
        print(f' https://dl.fbaipublicfiles.com/pytorch3d/packaging/wheels/{version_str}/download.html')
        !pip install fvcore iopath
        !pip install --no-index --no-cache-dir pytorch3d -f https://dl.fbaipublicfiles.com/pytorch3d/packaging/wheels/{version_str}/download.html
    else:
        # We try to install PyTorch3D from source.
        !pip install 'git+https://github.com/facebookresearch/pytorch3d.git@stable'