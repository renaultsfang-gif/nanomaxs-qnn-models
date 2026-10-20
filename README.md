# NanoMaxS QNN downloads

These are target-specific inference packs, not new training or automotive fine-tuning.
Model names in the demo are display names; original provenance is retained in each asset-manifest.json.

- NanoMaxS: Qualcomm AI Hub Whisper-Small v0.64.0, derived from OpenAI Whisper (MIT); Qualcomm model card: Apache-2.0. https://huggingface.co/qualcomm/Whisper-Small
- Zipformer English/Chinese: Qualcomm AI Hub v0.64.0; SM8850 uses the original pfluo/k2fsa-zipformer-chinese-english-mixed checkpoint, recompiled for its exact HTP. https://huggingface.co/qualcomm/Zipformer and https://huggingface.co/pfluo/k2fsa-zipformer-chinese-english-mixed
- Zipformer Korean: independent KsponSpeech checkpoint, Apache-2.0 model card. https://huggingface.co/johnBamma/icefall-asr-ksponspeech-pruned-transducer-stateless7-streaming-2024-06-12
- NanoMax3: NVIDIA Nemotron 3.5 ASR streaming 0.6B, exported by sherpa-onnx. https://huggingface.co/nvidia/nemotron-3.5-asr-streaming-0.6b and https://github.com/k2-fsa/sherpa-onnx/releases/tag/asr-models-qnn-binary-3
- SenseVoiceSmall: Alibaba Tongyi Speech Team, QwenAudio/SenseVoice; upstream k2-fsa/sherpa-onnx 2024-07-17 INT8 QNN conversion, 10 second graph. Five languages (Mandarin, Cantonese, English, Japanese, Korean), ITN enabled. Rolling-window incremental display, not native stateful streaming. Model weights use the FunASR Model Open Source License Agreement v1.1; code licenses MIT and Apache-2.0 are included separately. https://github.com/QwenAudio/SenseVoice
- QNN Runtime: Qualcomm QAIRT 2.51.0; the original LICENSE.pdf and NOTICE.txt are included in each runtime pack. Upstream model and runtime terms continue to apply.

Catalog revision 12 adds SM8450 (SOC 36 / HTP V69) and SM8550 (SOC 43 / HTP V73): exact-target runtime, Zipformer Chinese/English, Zipformer Korean and NanoMax2/SenseVoiceSmall. SM8450 Chinese/English uses official AI Hub v0.64.0 contexts. SM8550 Chinese/English and both Korean packs are independently host-compiled from their original checkpoints with QNN EP 2.7.0 / QAIRT 2.51.0. SenseVoice uses upstream exact-SoC INT8 contexts. SM8450 and SM8550 hardware validation is pending; host compilation and hashes do not establish accuracy or latency. All 26 previous binary assets are unchanged. The catalog now contains 34 packs (8 runtimes and 26 models), with 14 of 40 model/SoC combinations unavailable. Whisper Small and NanoMax3 have no published packs for the two added targets. SM8650/SM8850 have prior device evidence. SA8155 remains an unpublished experimental DSP candidate. No CPU inference fallback is provided. Android 13+, arm64-v8a required.

GitHub release assets contain binaries; the private Android source repository contains source, manifests and preparation tools only. Downloaded pack SHA256 values and per-file hashes are covered by an Ed25519-signed catalog. The Android APK pins the public verification key. Audio is not uploaded.
