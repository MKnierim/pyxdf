# PyXDF - Chunk Dejitter Extension
This fork of the [pyxdf repository](https://github.com/xdf-modules/pyxdf/blob/main/pyxdf) provides a function to dejitter signal timestamps when samples are received as chunks without temporal information for samples within those chunks (e.g., when OpenBCI Cyton data is streamed via LSL using the [OpenBCI_LSL](https://github.com/openbci-archive/OpenBCI_LSL/) python repository).

## Usage
1. Load the xdf streams with the pyxdf.load_xdf() and set dejitter_timestamps=False.
2. Extract the stream of interest and pass it to chunk_jitter_removal().

## Example
``` python
# Load xdf file
data, header = pyxdf.load_xdf('recording.xdf', dejitter_timestamps=False)

# Select stream of interest
stream = data[0] 

# Set parameters for chunk extrapolation
fs = 250 # Set sampling frequency
chunk_size = 120 # Set expected size of chunks

# Correct time stamps
stream, n_short_chunks = chunk_jitter_removal(stream, fs, chunk_size)
```
