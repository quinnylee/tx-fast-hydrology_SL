# tx-fast-hydrology

Routing and data assimilation code for the TxDOT FAST project, including the
`BmiKF` model interface. Requires Python 3.11 or newer.

## Installation

Install directly from the hydrology repository's `EKF_Troute` branch without
manually cloning the repository:

```sh
python -m pip install "tx-fast-hydrology @ git+https://github.com/slama0077/tx-fast-hydrology_SL.git@EKF_Troute"
```

Git must be installed for this command. The package configuration is at the
hydrology repository root. For a reproducible installation, replace
`@EKF_Troute` with `@<tag-or-commit>`.

This installs the package normally, without editable mode, and installs the
core dependencies: NumPy, pandas, SciPy, and Numba.

## Usage

```python
from tx_fast_hydrology.bmi_KF import BmiKF

model = BmiKF()
model.initialize("KF.yaml")
model.update()
discharge = model.get_value_ptr("discharge")
model.finalize()
```

Provide your own configuration and input data. Relative paths in the
configuration retain their existing behavior: they are resolved against the
working directory. The `Interface` class already handles this by initializing
KF from the configuration file's directory.

The package installation does not install t-route or the optional dependencies
used by the download utilities, web application, and HDF-backed smoother.
Those features require their corresponding dependencies separately.