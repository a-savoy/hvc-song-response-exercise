# Female zebra finch HVC — single-neuron song-response exercise

A small, self-contained Python data-analysis exercise. Starting from real recordings, reproduce the
target figure: how one neuron responds when a female zebra finch hears an unfamiliar male's song.

## Design
One neuron in the HVC (a song-related brain area) of a female zebra finch, responding to an
unfamiliar male's song. Each trial plays the same 3 s song twice (a "tandem pair": song, gap, song).

## Setup — Google Colab

You'll do all of this in a Colab notebook. There is nothing to install on your own computer.

1. Sign in to your Google account (use your UMich account).
2. Go to [colab.research.google.com](https://colab.research.google.com).
3. Click New notebook.
4. In the empty cell, type: 'print("hello")'
5. Press Shift + Return (or Shift + Enter).
6. 'hello' should appear below the cell.

Then open your preferred AI/LLM interface in another browser tab or window — or use Colab's built-in
AI assistant. See [Using an AI assistant](#using-an-ai-assistant) below.

### Get the data into your notebook

In a new cell, run:

    !git clone https://github.com/a-savoy/hvc-song-response-exercise.git
    %cd hvc-song-response-exercise

That copies this repository into your Colab session and moves you into it, so the paths
'data/unfamiliar_spikes.csv' and 'data/unfamiliar_song.wav' will work.

Colab already has 'numpy', 'pandas', 'matplotlib', and 'scipy' — no 'pip install' needed.

> Your Colab session is temporary. If it disconnects, or you come back the next day, re-run
> those two lines before you continue. Anything you want to keep, save to your Drive or download.

## Your task

Write Python that reads the two files in 'data/' and reproduces 'target_figure.png' — four stacked panels:

1. **Spectrogram** of the two song presentations
2. **Oscillogram** — the song waveform, colored by the neuron's firing rate
3. **PSTH** — firing rate in 100 ms bins
4. **Raster** — one row per trial (20 trials)

The x-axis is a 15 s display: '3 s pre + 3 s song A + 3 s gap + 3 s song B + 3 s post'.

### Steps
- **1.** Read the CSV into per-trial spike-time arrays (group by 'trial').
- **2.** Bin all spikes into 100 ms bins, divide by (bin width × n_trials) → firing rate (PSTH).
- **3.** Read the WAV; draw the spectrogram and firing-rate-colored waveform (song at 3–6 s and 9–12 s).
- **4.** Draw the PSTH bars and the raster; save.

Build it up one panel at a time. Get the raster drawing before you worry about the spectrogram — it's
the simplest panel and it tells you immediately whether you read the data correctly.

## Using an AI assistant

You may use any LLM you like (ChatGPT, Claude, Gemini, …), or the AI assistant built into Colab.
Things that tend to work well:

- **Describe the data before asking for code.** For example: "I have a CSV with columns 'trial' and
  'spike_time_s', one row per spike, 20 trials, spike times from 0 to 15 seconds."
- **Paste error messages in full.** The traceback is the single most useful thing you can hand it.
- **Ask it to explain what it wrote,** line by line, until you could reproduce the code yourself.
- **Work one panel at a time** instead of asking for the whole figure in one shot.

The point is to end up understanding the figure, not just to produce it. An LLM will happily write
code that runs and plots the wrong thing, so check every panel against 'target_figure.png' yourself
rather than trusting that it worked.

## Checking your work

Compare what you make against 'target_figure.png', one panel at a time:

- Do the two song windows sit at 3–6 s and 9–12 s?
- Does the raster have 20 rows, one per trial?
- Does the PSTH peak where the raster looks densest?
- Is the whole x-axis 0 to 15 s?

'reference_solution.ipynb' in this repository is a complete worked solution, broken into
explained steps. Do not open it first. Start with the data, the target figure, your own blank
notebook, and your LLM — then open the solution to see how I built the figure, once you have
made a real attempt yourself.

## The data ('data/')

| File | Format | What it is |
|---|---|---|
| 'unfamiliar_spikes.csv' | CSV: 'trial, spike_time_s' | one row per spike; 'spike_time_s' is already on the 0–15 s display axis. Every trial 0–19 appears; a trial with no spikes carries a single 'NaN' row so the trial count is preserved |
| 'unfamiliar_song.wav' | 44.1 kHz WAV | the unfamiliar song (played twice per trial; laid into both song windows) |

One fixed detail: the firing-rate color scale is pinned ('FR_MIN_GLOBAL=0.0', 'FR_MAX_GLOBAL=59.5') so
this panel's colors match the original multi-song figure exactly; set both to 'None' to auto-scale.

## Running locally instead

If you would rather work on your own machine than in Colab, clone the repository, then run these
from inside the repository folder:

    python3 -m venv .venv
    source .venv/bin/activate
    pip install -r requirements.txt notebook
    jupyter notebook

The first two lines create and switch into a virtual environment. They matter: on macOS and most
Linux systems the interpreter is 'python3' rather than 'python', and there is no bare 'pip' command
at all until an environment is activated. On Windows, activate with '.venv\Scripts\activate'
instead of the 'source' line.

## License

Licensed under **CC BY 4.0** — free to use and adapt with attribution. See ['LICENSE'](LICENSE).
Suggested credit: *Savoy, A. (2026). Female zebra finch HVC single-neuron song-response
teaching example. CC BY 4.0.*
