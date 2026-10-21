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

## kangkyu Zipformer2 Korean — 0.14.0

Original kangkyu/icefall-asr-ko-streaming-zipformer-174m checkpoint, Apache-2.0; no automotive fine-tuning.
https://huggingface.co/kangkyu/icefall-asr-ko-streaming-zipformer-174m
Independent FP32 export and strict FP16 QNN HTP compilation; chunk16, 2460-token Korean syllable vocabulary,
116 encoder cache inputs and batched beam8 decoder/joiner. Public development controls and realtime parity
validated on Honor FCP-AN10 / SM8650 only. This does not establish held-out broadcasting/automotive accuracy.
Only the SM8650 pack is currently published; all seven other HTP targets remain unavailable for this family.
The older zipformer_ko / KsponSpeech family is retired from the 0.14.0 app selector. Earlier immutable packs
are retained for reproducibility; model choice does not silently fall back to them or to CPU inference.
Catalog revision 13 adds one pack and preserves all 34 prior package descriptors and binary digests.

## Zipformer Korean — 0.15.0

The display name is now Zipformer Korean. Its source remains kangkyu's original Zipformer2
checkpoint; model ID `zipformer2_ko` and the validated SM8650 binary pack remain unchanged.

| Chipset | Download and execution | Hardware evidence |
| --- | --- | --- |
| SM8650 | FP16 HTP V75 encoder + beam8 heads | Honor public fixtures, live parity, offline regression |
| SM8450 | Independently compiled FP16 HTP V69 context pack + existing exact runtime | Host compiled; device validation pending |
| SM8550 | Independently compiled FP16 HTP V73 context pack + existing exact runtime | Host compiled; device validation pending |
| SA8155 | Experimental W8A8 arm64 QNN model libraries + DSP V66 runtime; graph finalized on target | No SA8155 board/BSP validation |

SA8155 is not an HTP context. Original FP32 graphs, public recurrent-state calibration,
DSP-specific exact mask lowering and SDK 2.40 quantization produced the model libraries.
They use the pinned Maven 2.51.0 DSP runtime candidate; BSP/unsigned-PD compatibility,
DSP operator type/shape acceptance, recognition accuracy and latency require the actual board.
The app marks this package Experimental DSP, verifies backendId=5 and performs strict DSP
graph composition/finalization. Failure is reported; CPU inference is never substituted.
Original runtime licenses, model provenance and code licenses accompany the packs.
No automotive fine-tuning is claimed. Prior 35 package descriptors and binary digests are preserved.
