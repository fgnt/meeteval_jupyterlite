# MeetEval demo running in JupyterLite

This repository contains the code for the visualization demo of [MeetEval](github.com/fgnt/meeteval).

## Building

To build the demo, you first have to install Pyodide and build the `meeteval` package as a WebAssembly module [as described here](https://pyodide.org/en/stable/development/building-and-testing-packages.html).

```bash
# Install Pyodide
pip install pyodide-build

# Install and setup emscripten
git clone https://github.com/emscripten-core/emsdk.git
cd emsdk
PYODIDE_EMSCRIPTEN_VERSION=$(pyodide config get emscripten_version)
./emsdk install ${PYODIDE_EMSCRIPTEN_VERSION}
./emsdk activate ${PYODIDE_EMSCRIPTEN_VERSION}
source emsdk_env.sh
cd ..

# Clone and build meeteval
git clone https://github.com/fgnt/meeteval
cd meeteval
pyodide build
cd ..

# Copy the built package to the demo folder
cp meeteval/dist/meeteval.* pypi

# Build the demo
jupyter lite build --output-dir dist
```