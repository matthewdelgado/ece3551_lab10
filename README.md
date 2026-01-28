# Audio Player with ALSA

This repository contains C++ programs for playing and manipulating WAV audio files using the Advanced Linux Sound Architecture (ALSA) library.

## Project Overview

The project currently provides a basic WAV file player (`WavePlayer.cpp`). The presence of `EchoPlayer.cpp` and `ReversePlayer.cpp` suggests future enhancements to implement audio effects like echo and reverse playback.

## Files

- `WavePlayer.cpp`: A C++ program to play WAV audio files through ALSA.
- `EchoPlayer.cpp`: (Currently identical to `WavePlayer.cpp`) Intended for playing WAV files with an echo effect.
- `ReversePlayer.cpp`: (Currently empty) Intended for playing WAV files in reverse.
- `guitar.wav`: An example WAV audio file for testing.
- `README.md`: This file.

## Requirements

To compile and run these programs, you need:

- A C++ compiler (e.g., g++)
- ALSA development libraries (e.g., `libasound2-dev` on Debian/Ubuntu)

## How to Compile

You can compile the programs using g++:

```bash
g++ -o WavePlayer WavePlayer.cpp -lasound
g++ -o EchoPlayer EchoPlayer.cpp -lasound
g++ -o ReversePlayer ReversePlayer.cpp -lasound
```

## How to Run

### WavePlayer

To play a WAV file:

```bash
./WavePlayer <path_to_wav_file>
```

If no file is provided, it will prompt you to enter the filename.

Example:

```bash
./WavePlayer guitar.wav
```

### EchoPlayer (Future Implementation)

Once implemented, this would play a WAV file with an echo effect.

```bash
./EchoPlayer <path_to_wav_file>
```

### ReversePlayer (Future Implementation)

Once implemented, this would play a WAV file in reverse.

```bash
./ReversePlayer <path_to_wav_file>
```

## WAV Header Structure

The `WAV_HEADER` struct used in the C++ files defines the standard WAV file format:

```cpp
typedef struct WAV_HEADER
{
    /* RIFF Chunk Descriptor */
    uint8_t RIFF[4];    // RIFF Header Magic header
    uint32_t ChunkSize; // RIFF Chunk Size
    uint8_t WAVE[4];    // WAVE Header
    /* "fmt" sub-chunk */
    uint8_t fmt[4];         // FMT header
    uint32_t Subchunk1Size; // Size of the fmt chunk
    uint16_t AudioFormat;   // Audio format 1=PCM,6=mulaw,7=alaw,     257=IBM Mu-Law, 258=IBM A-Law, 259=ADPCM
    uint16_t NumOfChan;     // Number of channels 1=Mono 2=Sterio
    uint32_t SamplesPerSec; // Sampling Frequency in Hz
    uint32_t bytesPerSec;   // bytes per second
    uint16_t blockAlign;    // 2=16-bit mono, 4=16-bit stereo
    uint16_t bitsPerSample; // Number of bits per sample
    /* "data" sub-chunk */
    uint8_t Subchunk2ID[4]; // "data"  string
    uint32_t Subchunk2Size; // Sampled data length
} wav_hdr;
```