# Female zebra finch HVC single-neuron song-response exercise

A small, self-contained Python data-analysis exercise. Starting from real recordings, reproduce the
target figure, which shows spiking from one neuron in female zebra finch HVC (a song-related brain area), 
in response to an unfamiliar male's song. Each trial plays the same 3 s song twice (a "tandem pair": song, gap, song).

## Setup Google Colab

You'll do all of this in a Colab notebook. There is nothing to install on your own computer.

1. Sign in to your Google account (use your UMich account).
2. Go to [colab.research.google.com](https://colab.research.google.com).
3. Click New notebook.
4. In the empty cell, type: 'print("hello")'
5. Press Shift + Return (or Shift + Enter).
6. 'hello' should appear below the cell.

Then open your preferred AI/LLM interface in another browser tab or window, or use Colab's built-in
AI assistant. See [Using an AI assistant](#using-an-ai-assistant) below.

### Get the data into your notebook

In a new cell, run:

    !git clone https://github.com/a-savoy/hvc-song-response-exercise.git
    %cd hvc-song-response-exercise

That copies this repository into your Colab session and moves you into it, so the paths
'data/unfamiliar_spikes.csv' and 'data/unfamiliar_song.wav' will work.

Colab already has 'numpy', 'pandas', 'matplotlib', and 'scipy', so no 'pip install' needed.

> Your Colab session is temporary. If it disconnects, or you come back the next day, re-run
> those two lines before you continue. Anything you want to keep, save to your Drive or download.

## Your task

Write Python that reads the two files in 'data/' and reproduces 'target_figure.png' — four stacked panels:

- **Spectrogram** showing the two song presentations
- **Oscillogram** showing the song waveform, colored by the neuron's firing rate
- **PSTH** with firing rate in 100 ms bins
- **Raster** with one row per trial (20 trials)

The x-axis is a 15 s display: '3 s pre + 3 s song A + 3 s gap + 3 s song B + 3 s post'.

### Steps
1. Read the CSV into per-trial spike-time arrays (group by 'trial').
2. Bin all spikes into 100 ms bins, divide by (bin width × n_trials) → firing rate (PSTH).
3. Read the WAV; draw the spectrogram and firing-rate-colored waveform (song at 3–6 s and 9–12 s).
4. Draw the PSTH bars and the raster; save.

## Checking your work

'reference_solution.ipynb' in this repository is a complete worked solution, broken into
explained steps. Do not open it first. Start with the data, the target figure, your own blank
notebook, and your LLM, then open the solution to see how I built the figure, once you have
made a real attempt yourself.

## The data ('data/')

| File | Format | What it is |
|---|---|---|
| 'unfamiliar_spikes.csv' | CSV: 'trial, spike_time_s' | one row per spike; 'spike_time_s' is already on the 0–15 s display axis. Every trial 0–19 appears; a trial with no spikes carries a single 'NaN' row so the trial count is preserved |
| 'unfamiliar_song.wav' | 44.1 kHz WAV | the unfamiliar song (played twice per trial; laid into both song windows) |

## Running locally instead

If you would rather work on your own machine than in Colab, clone the repository, then run these
from inside the repository folder:

    python3 -m venv .venv
    source .venv/bin/activate
    pip install -r requirements.txt notebook
    jupyter notebook

The first two lines create and switch into a virtual environment. On macOS and most
Linux systems, the interpreter is 'python3' rather than 'python', and there is no 'pip' command
at all until an environment is activated. On Windows, activate with '.venv\Scripts\activate'
instead of the 'source' line.

## License

Licensed under **CC BY 4.0**. Free to use and adapt with attribution. See ['LICENSE'](LICENSE).
Suggested credit: *Savoy, A. (2026). Female zebra finch HVC single-neuron song-response
teaching example. CC BY 4.0.*
