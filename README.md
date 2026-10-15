# NanoMaxS QNN downloads

These are target-specific inference packs, not new training or automotive fine-tuning.
Model names in the demo are display names; original provenance is retained in each asset-manifest.json.

- NanoMaxS: Qualcomm AI Hub Whisper-Small v0.64.0, derived from OpenAI Whisper (MIT); Qualcomm model card: Apache-2.0. https://huggingface.co/qualcomm/Whisper-Small
- Zipformer English/Chinese: Qualcomm AI Hub v0.64.0; SM8850 uses the original pfluo/k2fsa-zipformer-chinese-english-mixed checkpoint, recompiled for its exact HTP. https://huggingface.co/qualcomm/Zipformer and https://huggingface.co/pfluo/k2fsa-zipformer-chinese-english-mixed
- Zipformer Korean: independent KsponSpeech checkpoint, Apache-2.0 model card. https://huggingface.co/johnBamma/icefall-asr-ksponspeech-pruned-transducer-stateless7-streaming-2024-06-12
- NanoMax3: NVIDIA Nemotron 3.5 ASR streaming 0.6B, exported by sherpa-onnx. https://huggingface.co/nvidia/nemotron-3.5-asr-streaming-0.6b and https://github.com/k2-fsa/sherpa-onnx/releases/tag/asr-models-qnn-binary-3
- QNN Runtime: Qualcomm QAIRT 2.51.0; the original LICENSE.pdf and NOTICE.txt are included in each runtime pack. Upstream model and runtime terms continue to apply.

SM8650/SM8850 model contexts have prior device evidence. Other published packs have target/hash preparation checks only; hardware validation is pending. Nine of the 24 model/SoC combinations are still missing. No CPU inference fallback is provided.

GitHub release assets contain binaries; the private Android source repository contains source, manifests and preparation tools only. Downloaded pack SHA256 values and per-file hashes are covered by an Ed25519-signed catalog. The Android APK pins the public verification key. Audio is not uploaded.
