# MedASR GitHub assets

This folder contains a compact set of MedASR model assets for local experimentation and inference. It is intended to be used together as a self-contained speech recognition package with a TFLite model, preprocessing configuration, tokenizer files, and a sample audio clip.

## What is included

- medasr_10sec_window.tflite: the exported MedASR TFLite model for a 10-second inference window
- preprocessor_config.json: feature extractor settings for audio preprocessing
- processor_config.json: processor configuration used by the MedASR pipeline
- tokenizer.json and tokenizer_config.json: tokenizer assets for decoding model outputs
- mel_filters.bin: mel filterbank data used during feature extraction
- test_audio.wav: a small sample audio file for quick testing

## Intended use

These files are meant for:

- running local inference with a TFLite/LiteRT-compatible runtime
- testing audio preprocessing and tokenizer behavior
- integrating the model into a mobile or embedded speech pipeline

## Requirements

A typical setup includes:

- Python 3.10+
- TensorFlow Lite / LiteRT runtime
- optional: transformers, librosa, or soundfile for preprocessing and audio loading

## Quick start

1. Keep all files in this folder together so the model and config assets remain aligned.
2. Load the TFLite model using your preferred runtime.
3. Load the preprocessing configuration and tokenizer files from the same directory.
4. Feed a 16 kHz mono audio waveform through the preprocessing pipeline and run inference.

Example concept:

```python
import tensorflow as tf

interpreter = tf.lite.Interpreter(model_path="medasr_10sec_window.tflite")
interpreter.allocate_tensors()

print(interpreter.get_input_details())
print(interpreter.get_output_details())
```

## Notes

- The model assets are designed to work as part of the same MedASR pipeline; changing file locations may break loading expectations.
- For best results, use audio sampled at 16 kHz and matching the preprocessing settings in the JSON config files.
- This folder is useful for prototyping and local testing rather than as a full end-to-end deployment package.
