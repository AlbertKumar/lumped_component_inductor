# spice_my_inductor
Takes an s-parameter (Touchstone s2p) file and creates a lumped component Spice (.sp) model.

1. Download the files:
  - inductor.py
  - skrf_extensions.py
  - aux.py

2. Make sure you have the following installed.
  - numpy
  - scikit-rf
  - lmfit
  - matplotlib
  
Example script.
```
from inductor import *

# Load in the s2p data.
inductor = Inductor(data="sample.s2p")

# Print the modeled parameters.
print(inductor.model_parameters)

# Write out the data in spice format.
inductor.write_spice(filename='./my_inductor.cir')

# Show the model vs data.
inductor.show_plot()
```

Plots:

![smi_inductor_fit_series](https://user-images.githubusercontent.com/56657608/204691855-6f247cbb-3774-48ff-9796-2887db88a785.png)


Generated spice file.
```
.subckt smi_inductor PLUS MINUS
Ls0 PLUS N001 5.014841488858481e-9
Rs0 N001 MINUS 6.969829290617154
Ls1 N001 N002 2.9056030702109865e-9
Rs1 N002 MINUS 17.339014722636662
Cox1L PLUS N003L 159.999999839297e-15
Rsi1L N003L 0 1999.9999987641813
Csi1L N003L 0 49.9999986071684e-15
Cox1R MINUS N003R 159.999999839297e-15
Rsi1R N003R 0 1999.9999987641813
Csi1R N003R 0 49.9999986071684e-15
Csub N003L N003R 25.303154359963667e-15
Rsub N003L N003R 3952.076319416227
Cp PLUS MINUS 37.63844211044595
.ends
```

References:
H. -H. Chen, H. -W. Zhang, S. -J. Chung, J. -T. Kuo and T. -C. Wu, "Accurate Systematic Model-Parameter Extraction for On-Chip Spiral Inductors," in IEEE Transactions on Electron Devices, vol. 55, no. 11, pp. 3267-3273, Nov. 2008, doi: 10.1109/TED.2008.2005131.
