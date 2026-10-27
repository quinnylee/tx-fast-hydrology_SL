# tx-fast-hydrology

Routing and data assimilation code for the TxDOT FAST project, including the
`BmiKF` model interface. Requires Python 3.11 or newer.

## Installation

Install directly from GitHub without manually cloning the repository:

```sh
python -m pip install "tx-fast-hydrology @ git+https://github.com/slama0077/Python_Interface.git#subdirectory=KF"
```

Git must be installed for this command. For a reproducible installation, put
`@<tag-or-commit>` after `.git` and before `#subdirectory=KF`.

To test local packaging changes, run this from the `Python_Interface` directory:

```sh
python -m pip install ./KF
```

Both commands install the package normally, without editable mode, and install
the core dependencies: NumPy, pandas, SciPy, and Numba.

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

## Notebook check

Open `interface.ipynb` from the repository root with the existing t-route
environment selected. Its first code cell installs `./KF` into the notebook's
Python environment. The next cell imports `BmiKF` and checks that it comes from
the installed distribution. Restart the kernel before running the notebook if
KF was previously imported from the source directory.
