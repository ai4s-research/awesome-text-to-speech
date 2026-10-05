<div align="center">
  <img src="assets/banner.jpg" alt="Awesome Text-to-Speech" width="100%">
  <h1>🔊 Awesome Text-to-Speech (TTS)</h1>
  <p>A curated list of the best Text-to-Speech, speech synthesis, and voice-cloning research — models, papers, benchmarks, and toolkits, with a focus on 2025–2026.</p>
  <p>
    <a href="https://awesome.re"><img src="https://awesome.re/badge.svg" alt="Awesome"></a>
    <a href="LICENSE"><img src="https://img.shields.io/badge/License-MIT-yellow.svg" alt="License: MIT"></a>
    <a href="https://github.com/ai4s-research/awesome-text-to-speech/stargazers"><img src="https://img.shields.io/github/stars/ai4s-research/awesome-text-to-speech?style=social" alt="GitHub Stars"></a>
    <a href="https://github.com/ai4s-research/awesome-text-to-speech/network/members"><img src="https://img.shields.io/github/forks/ai4s-research/awesome-text-to-speech?style=social" alt="GitHub Forks"></a>
    <a href="https://github.com/ai4s-research/awesome-text-to-speech/commits/main"><img src="https://img.shields.io/github/last-commit/ai4s-research/awesome-text-to-speech" alt="Last Commit"></a>
  </p>
</div>

---

**Text-to-speech (TTS)** has shifted from pipeline acoustic models to codec language models, flow matching, and full-duplex speech LLMs. This list tracks the models, papers, codecs, benchmarks, and toolkits that matter — with a bias toward 2025–2026 work and open weights you can actually run.

> Found a great model or paper we missed? [Contributions welcome](CONTRIBUTING.md).

---

## 📚 Contents

- [Surveys & Overviews](#-surveys--overviews)
- [Zero-shot & Large-scale TTS Models](#-zero-shot--large-scale-tts-models)
- [Voice Cloning & Speaker Adaptation](#-voice-cloning--speaker-adaptation)
- [Expressive, Controllable & Emotional TTS](#-expressive-controllable--emotional-tts)
- [Streaming, Real-time & Efficient TTS](#-streaming-real-time--efficient-tts)
- [Multilingual & Low-resource TTS](#-multilingual--low-resource-tts)
- [Neural Audio Codecs](#-neural-audio-codecs)
- [Singing Voice Synthesis](#-singing-voice-synthesis)
- [Benchmarks & Datasets](#-benchmarks--datasets)
- [Open-source Toolkits & Implementations](#-open-source-toolkits--implementations)
- [Commercial & Closed Systems](#-commercial--closed-systems)
- [Related Awesome Lists](#-related-awesome-lists)

## 📖 Surveys & Overviews

- [A Survey on Neural Speech Synthesis](https://arxiv.org/abs/2106.15561) — The canonical Tan et al. reference that fixed the text-analysis → acoustic-model → vocoder framing; dated on the LLM era but still the standard background read (2021).
- [Towards Controllable Speech Synthesis in the Era of Large Language Models: A Systematic Survey](https://arxiv.org/abs/2412.06602) — First survey to treat controllability as the through-line, tracing the shift from hand-engineered control knobs to natural-language-prompt control (2024).
- [WavChat: A Survey of Spoken Dialogue Models](https://arxiv.org/abs/2411.13577) — 60-page deep dive cleanly separating cascaded vs. end-to-end voice-dialogue stacks; the most thorough conversational-speech reference (2024).
- [Recent Advances in Speech Language Models: A Survey](https://arxiv.org/abs/2410.03751) — ACL 2025 survey of end-to-end SpeechLMs that drop the text bottleneck and generate speech directly (2024).
- [On The Landscape of Spoken Language Models: A Comprehensive Survey](https://arxiv.org/abs/2504.08528) — Heavyweight unifying SLM survey (Watanabe, Livescu, Dupoux, Lee, Adi); the single best overview if you read only one (2025).
- [From Turn-Taking to Synchronous Dialogue: A Survey of Full-Duplex Spoken Language Models](https://arxiv.org/abs/2509.14515) — The first survey focused on full-duplex (overlap / barge-in) speech models; exactly the right scope for the post-Moshi wave (2025).
- [Recent Advances in Discrete Speech Tokens: A Review](https://arxiv.org/abs/2502.06490) — IEEE TPAMI-accepted review splitting acoustic vs. semantic tokens; the cleanest theory companion to the codec literature below (2025).
- [Discrete Audio Tokens: More Than a Survey!](https://arxiv.org/abs/2506.10274) — Massive multi-institution survey that also runs its own benchmark of tokenizers; the most current *empirical* tokenizer reference (2025).
- [Voice Cloning: Comprehensive Survey](https://arxiv.org/abs/2505.00579) — Spans speaker adaptation, few-/zero-shot and multilingual cloning plus misuse and detection; the closest thing to a dedicated zero-shot-TTS survey (2025).

## 🚀 Zero-shot & Large-scale TTS Models

### Foundational

- [VALL-E: Neural Codec Language Models are Zero-Shot Text to Speech Synthesizers](https://arxiv.org/abs/2301.02111) — Recast TTS as language modeling over EnCodec tokens with 3-second-prompt cloning; the origin point of the entire codec-LM TTS wave (2023).
- [VALL-E 2: Human Parity Zero-Shot Text to Speech Synthesizers](https://arxiv.org/abs/2406.05370) — First codec-LM TTS to claim human parity; its Repetition-Aware Sampling fixes VALL-E's infinite-loop failure mode (research-only) (2024).
- [NaturalSpeech 3: Zero-Shot Speech Synthesis with Factorized Codec and Diffusion Models](https://arxiv.org/abs/2403.03100) — Factorizes speech into content/prosody/timbre/acoustic subspaces (FACodec) so attributes become individually promptable instead of entangled (2024).
- [E2 TTS: Embarrassingly Easy Fully Non-Autoregressive Zero-Shot TTS](https://arxiv.org/abs/2406.18009) — Strips TTS down to flow-matching + vocoder with no duration model, aligner, or G2P, yet beats Voicebox/NaturalSpeech 3; the conceptual parent of F5-TTS (2024).
- [F5-TTS: A Fairytaler that Fakes Fluent and Faithful Speech with Flow Matching](https://arxiv.org/abs/2410.06885) — Made the E2 recipe actually trainable (ConvNeXt text refinement + inference-time Sway Sampling) and became the de-facto open-weights zero-shot cloner (2024).

### 2025-2026 flagship systems

- [CosyVoice 2: Scalable Streaming Speech Synthesis with Large Language Models](https://arxiv.org/abs/2412.10117) — Swaps VQ for finite scalar quantization (near-100% codebook use) and adds chunk-aware causal flow matching so one model does both streaming and non-streaming (2024).
- [CosyVoice 3: Towards In-the-wild Speech Generation via Scaling-up and Post-training](https://arxiv.org/abs/2505.17589) — Scales 0.5B→1.5B and 10k→1M hours, adds differentiable-reward RL post-training to harden zero-shot synthesis on messy real-world speech (2025).
- [Llasa: Scaling Train-Time and Inference-Time Compute for Llama-based Speech Synthesis](https://arxiv.org/abs/2502.04128) — Shows you can ditch the bespoke TTS stack for a single standard LLaMA + one VQ codec and ride LLM scaling laws, including verifier-guided inference search (2025).
- [MegaTTS 3: Sparse Alignment Enhanced Latent Diffusion Transformer for Zero-Shot Speech Synthesis](https://arxiv.org/abs/2502.18924) — ByteDance; a sparse-alignment scheme gives the DiT soft boundary hints instead of forced alignment, hitting strong quality in ~8 steps (2025).
- [MiniMax-Speech: Intrinsic Zero-Shot Text-to-Speech with a Learnable Speaker Encoder](https://arxiv.org/abs/2505.07916) — A learnable speaker encoder needing no reference transcript enables truly *intrinsic* zero-shot cloning across 32 languages; topped the public TTS Arena (2025).
- [Qwen3-TTS Technical Report](https://arxiv.org/abs/2601.15621) — Qwen team's flagship open large-scale system: 5M+ hours, dual-track LM and dual speech tokenizers for ~97 ms first-packet streaming plus 3 s cloning (2026).
- [OmniVoice: Towards Omnilingual Zero-Shot Text-to-Speech with Diffusion Language Models](https://arxiv.org/abs/2604.00688) — Pushes zero-shot TTS to genuinely "omnilingual" coverage on a diffusion-LM backbone, doing both cloning and reference-free voice design (2026).
- [Fish Audio S2 Technical Report](https://arxiv.org/abs/2603.08823) — The 2026 successor in the Fish-Speech / OpenAudio line; a current data point on where the open dual-AR TTS recipe has scaled to (2026).
- [Kokoro-82M](https://github.com/hexgrad/kokoro) — An 82M StyleTTS2-based model that rivals systems 10x its size, Apache-2.0; the reason "tiny local TTS" became a serious category (2025).
- [Higgs Audio v2](https://github.com/boson-ai/higgs-audio) — Boson AI foundation model doing multi-speaker dialogue, humming, and simultaneous speech+music zero-shot — unusually broad generation surface (2025).
- [VibeVoice](https://github.com/microsoft/VibeVoice) — Microsoft's open long-form TTS (up to ~90 min, 4 speakers) via next-token diffusion, MIT, ICLR 2026 Oral; the open frontier for long multi-speaker audio (2026).
- [Sesame CSM](https://github.com/SesameAILabs/csm) — The viral conversational speech model (Llama backbone over Mimi codes), Apache-2.0; the open reference for natural conversational TTS (2025).
- [Qwen3-Omni](https://github.com/QwenLM/Qwen3-Omni) — Leading open omni LLM with real-time speech output across many languages, Apache-2.0 (2025).
- [GLM-4-Voice](https://github.com/zai-org/GLM-4-Voice) — A 9B end-to-end open speech LLM (speech-in / speech-out), Apache-2.0 (2024).
- [Kimi-Audio](https://github.com/MoonshotAI/Kimi-Audio) — Open universal audio foundation model that understands, generates, and converses in one stack (2025).
- [MiMo-Audio](https://github.com/XiaomiMiMo/MiMo-Audio) — Xiaomi's 7B speech LM with few-shot speech generation and instruct-TTS (2025).
- [VoxCPM](https://huggingface.co/openbmb/VoxCPM1.5) — Tokenizer-free continuous TTS on MiniCPM-4, Apache-2.0; argues against discrete codecs for naturalness (2025).

## 🧬 Voice Cloning & Speaker Adaptation

- [VoiceCraft: Zero-Shot Speech Editing and Text-to-Speech in the Wild](https://arxiv.org/abs/2403.16973) — Causal-masking + delayed-stacking token rearrangement enables in-place *editing* of real recordings (insert/replace), not just synthesis (2024).
- [Seed-TTS: A Family of High-Quality Versatile Speech Generation Models](https://arxiv.org/abs/2406.02430) — ByteDance large AR TTS matching ground-truth human speech, with speech factorization via self-distillation and RL preference biasing (2024).
- [MaskGCT: Zero-Shot Text-to-Speech with Masked Generative Codec Transformer](https://arxiv.org/abs/2409.00750) — Brings the masked-generative (parallel mask-and-predict) paradigm to TTS with no text-speech alignment and no duration prediction (2024).
- [Autoregressive Speech Synthesis without Vector Quantization (MELLE)](https://arxiv.org/abs/2407.08551) — Drops VQ entirely to autoregress continuous mel frames via regression + spectrogram-flux loss, sidestepping codec-LM robustness flaws in one stage (2024).
- [Spark-TTS: An Efficient LLM-Based Text-to-Speech Model with Single-Stream Decoupled Speech Tokens](https://arxiv.org/abs/2503.01710) — Its BiCodec packs semantic + fixed-length speaker tokens into one stream, so a single 1B model does both cloning and reference-free voice creation (2025).
- [Vevo: Controllable Zero-Shot Voice Imitation with Self-Supervised Disentanglement](https://arxiv.org/abs/2502.07243) — Progressive self-supervised decoupling of content/style/timbre lets you drive style and timbre from *separate* reference clips (2025).
- [Vevo2: A Unified and Controllable Framework for Speech and Singing Voice Generation](https://arxiv.org/abs/2508.16332) — Extends Vevo's disentanglement to unify spoken and singing voice generation under one controllable tokenizer stack (2025).
- [IndexTTS2: A Breakthrough in Emotionally Expressive and Duration-Controlled Auto-Regressive Zero-Shot TTS](https://arxiv.org/abs/2506.21619) — Bilibili; the first AR TTS with explicit token-count/duration control while disentangling timbre from emotion (2025).
- [IndexTTS 2.5 Technical Report](https://arxiv.org/abs/2601.03888) — The 2026 iteration of IndexTTS, adding semantic-codec compression and broader multilingual coverage (2026).
- [Chatterbox](https://github.com/resemble-ai/chatterbox) — Resemble AI's MIT-licensed open SoTA model: first to ship built-in exaggeration control plus a Perth neural watermark on every output, at just 0.5B (2025).
- [GPT-SoVITS](https://github.com/RVC-Boss/GPT-SoVITS) — 5 s zero-shot / 1-min few-shot cloning with a huge community ecosystem; the practical go-to for hobbyist voice cloning (2024).

## 🎭 Expressive, Controllable & Emotional TTS

- [Parler-TTS: Natural language guidance of high-fidelity TTS with synthetic annotations](https://arxiv.org/abs/2402.01912) — Fully open reproduction with prompt-controllable style (pitch, reverb, background noise) driven by a text *description* rather than reference audio (2024).
- [Step-Audio: Unified Understanding and Generation in Intelligent Speech Interaction](https://arxiv.org/abs/2502.11946) — StepFun's 130B unified model distills a deployable 3B TTS with instruction control over dialect, emotion, singing, and rap (2025).
- [Marco-Voice Technical Report](https://arxiv.org/abs/2508.02038) — Speaker–emotion disentanglement via in-batch contrastive learning plus rotational emotion embeddings for smooth control; ships the CSEMOTIONS dataset (2025).
- [CoCoEmo: Composable and Controllable Human-Like Emotional TTS via Activation Steering](https://arxiv.org/abs/2602.03420) — First systematic use of activation steering for emotion control, enabling *composable mixed-emotion* synthesis rather than single-label tags (2026).
- [Toward Natural Emotional Text-To-Speech System with Fine-Grained Non-Verbal Expression Control](https://arxiv.org/abs/2605.25504) — Targets the non-verbal vocalizations (sighs, laughs) that prosody-only emotional TTS routinely ignores (2026).
- [Sparse Autoencoders for Interpretable Emotion Control in Text-to-Speech](https://arxiv.org/abs/2606.01479) — Applies SAEs to make emotion directions in LLM-based TTS interpretable and individually steerable (2026).
- [Maya1](https://huggingface.co/maya-research/maya1) — A 3B expressive open TTS with inline emotion tags and natural-language voice design (2025).
- [LLaDA-TTS: Unifying Speech Synthesis and Zero-Shot Editing via Masked Diffusion Modeling](https://arxiv.org/abs/2603.26364) — Converts an AR LLM-TTS into a masked-diffusion model, unifying synthesis and editing with a ~2x speedup on the LLM stage (2026).
- [Dia-1.6B](https://github.com/nari-labs/dia) — Nari Labs; generates whole multi-speaker dialogue in one pass with nonverbals, an unusually conversational-first open model (2025).
- [Orpheus-TTS](https://github.com/canopyai/Orpheus-TTS) — Canopy; a Llama-3B backbone with tag-guided emotion and ~100-200 ms streaming, Apache-licensed LLM-as-TTS (2025).
- [EmotiVoice](https://github.com/netease-youdao/EmotiVoice) — NetEase; 2000+ voices with prompt-based emotion tags, an early and still-popular controllable open engine (2023).

## ⚡ Streaming, Real-time & Efficient TTS

- [Moshi: a speech-text foundation model for real-time dialogue](https://arxiv.org/abs/2410.00037) — True full-duplex (parallel user/model streams, ~200 ms latency) with an "inner monologue" text stream anchoring quality; also home of the Mimi codec (2024).
- [LLaMA-Omni: Seamless Speech Interaction with Large Language Models](https://arxiv.org/abs/2409.06666) — Speech-in/speech-out on Llama-3.1 with a streaming decoder at ~226 ms and no transcription step; an influential cheap-to-train open baseline (2024).
- [LLaMA-Omni2: LLM-based Real-time Spoken Chatbot with Autoregressive Streaming Speech Synthesis](https://arxiv.org/abs/2505.02625) — Moves to a fully autoregressive streaming decoder over Qwen2.5 (0.5B-14B) with strong spoken-QA from just 200K dialogues (2025).
- [Mini-Omni: Language Models Can Hear, Talk While Thinking in Streaming](https://arxiv.org/abs/2408.16725) — First fully end-to-end open real-time speech-interaction model; its "Any Model Can Talk" recipe made small speech LLMs reproducible (2024).
- [SyncSpeech: Efficient and Low-Latency TTS based on Temporal Masked Transformer](https://arxiv.org/abs/2502.11094) — Consumes streaming text from an LLM and decodes all tokens per text token in one step for ~5.8x lower first-packet latency; a clean AR/NAR hybrid (2025).
- [FlashSpeech: Efficient Zero-Shot Speech Synthesis](https://arxiv.org/abs/2404.14700) — Adversarial consistency training cuts zero-shot synthesis to ~one or two sampling steps (~20x faster), a key reference for the "kill the sampling steps" line (2024).
- [VoXtream: Full-Stream Text-to-Speech with Extremely Low Latency](https://arxiv.org/abs/2509.15969) — ICASSP 2026; fully autoregressive zero-shot streaming that starts speaking from the first word, with the lowest reported public initial delay (102 ms on GPU) (2025).
- [FlashTTS: Fast Streaming TTS with MTP Acceleration and X-pred Mean Flow Distillation](https://arxiv.org/abs/2606.09141) — Interspeech 2026; pairs multi-token prediction with mean-flow distillation to synthesize in two function evaluations at ~325 ms first-packet latency (2026).
- [dots.tts Technical Report](https://arxiv.org/abs/2606.07080) — A 2B continuous-autoregressive TTS foundation model claiming SoTA multilingual quality with efficient inference; a fresh large open AR-TTS report (2026).
- [Kyutai TTS / Delayed Streams Modeling](https://github.com/kyutai-labs/delayed-streams-modeling) — Kyutai's open low-latency streaming TTS (and STT) built on delayed-streams modeling; production-grade real-time open weights (2025).
- [Hertz-dev](https://github.com/Standard-Intelligence/hertz-dev) — The first open base full-duplex audio model (~120 ms theoretical latency); a foundation for two-way conversational speech (2024).
- [NeuTTS Air](https://huggingface.co/neuphonic/neutts-air) — On-device, CPU-real-time TTS paired with NeuCodec; the practical edge-deployment option (2025).

## 🌍 Multilingual & Low-resource TTS

- [XTTS: a Massively Multilingual Zero-Shot Text-to-Speech Model](https://arxiv.org/abs/2406.04904) — The paper behind Coqui's XTTS-v2: a Tortoise-derived GPT cloning across 16 languages from 6 seconds; still the default open multilingual cloner long after Coqui closed (2024).
- [Scaling Speech Technology to 1,000+ Languages (Meta MMS)](https://arxiv.org/abs/2305.13516) — Scaled ASR/TTS/LID to 1,000+ languages using readings of religious texts, shipping VITS TTS for ~1,100 languages — the broadest language coverage in any open release (2023).
- [ZMM-TTS: Zero-shot Multilingual and Multispeaker Speech Synthesis Conditioned on Self-supervised Discrete Speech Representations](https://github.com/nii-yamagishilab/ZMM-TTS) — Generalizes zero-shot to unseen speakers *and* unseen languages via SSL discrete units; a clean NII/Yamagishi academic baseline (2023).
- [Spirit LM: Interleaved Spoken and Written Language Model](https://github.com/facebookresearch/spiritlm) — Meta interleaves speech and text tokens, picking up TTS/ASR/classification few-shot; the LM-native alternative to dedicated pipelines (2024).
- [Habibi: Laying the Open-Source Foundation of Unified-Dialectal Arabic Speech Synthesis](https://arxiv.org/abs/2601.13802) — Open system covering 30+ Arabic spoken varieties; rare dialect-level coverage for a major but heavily fragmented language family (2026).
- [OpenBibleTTS: Large-Scale Speech Resources and TTS Models for Low-Resource Languages](https://arxiv.org/abs/2606.09553) — Releases datasets, alignments, and trained TTS across 37 underrepresented languages (strong on African languages); the most substantial low-resource drop of 2026 so far (2026).
- [UR-BERT: Scaling Text Encoders for Massively Multilingual TTS Through Universal Romanization and Speech Token Prediction](https://arxiv.org/abs/2606.11681) — Interspeech 2026; scales a text encoder to 495 languages by unifying all writing systems into shared Romanization — a fresh attack on the multilingual front-end bottleneck (2026).

## 🔊 Neural Audio Codecs

- [SoundStream: An End-to-End Neural Audio Codec](https://arxiv.org/abs/2107.03312) — Kicked off the modern RVQ era: jointly trained conv encoder/decoder + residual vector quantizer, streamable on a phone CPU; the template every later codec reacts to (2021).
- [EnCodec: High Fidelity Neural Audio Compression](https://github.com/facebookresearch/encodec) — Meta's EnCodec is the de-facto baseline tokenizer for audio LMs (MusicGen, VALL-E descendants), with clean open 24k/48k models (2022).
- [Descript Audio Codec (DAC): High-Fidelity Audio Compression with Improved RVQGAN](https://github.com/descriptinc/descript-audio-codec) — ~90x compression at 8 kbps across speech/music/ambient; the universal-domain quality bar and a common drop-in EnCodec replacement (2023).
- [SpeechTokenizer: Unified Speech Tokenizer for Speech Large Language Models](https://github.com/ZhangXInFD/SpeechTokenizer) — Distills semantics into RVQ layer 1 so the first token is "semantic" and the rest acoustic; the canonical disentangled tokenizer for speech LMs (2023).
- [WavTokenizer: an Efficient Acoustic Discrete Codec Tokenizer for Audio Language Modeling](https://github.com/jishengpeng/WavTokenizer) — Pushes to a single quantizer at 40/75 tokens/sec with SoTA UTMOS; the extreme-compression single-codebook option for LM-friendly audio (2024).
- [SNAC: Multi-Scale Neural Audio Codec](https://github.com/hubertsiuzdak/snac) — Runs RVQ quantizers at different temporal resolutions (coarse-to-fine) for cheaper low-bitrate coding; the codec behind several open TTS stacks like Orpheus (2024).
- [X-Codec: Codec Does Matter — Exploring the Semantic Shortcoming of Codec for Audio Language Model](https://github.com/zhenye234/xcodec) — Fuses semantic + acoustic features in one RVQ to directly lift downstream audio-LM quality; the original X-Codec (2024).
- [X-Codec 2.0](https://github.com/zhenye234/X-Codec-2.0) — A single-VQ 1D semantic+acoustic tokenizer built to slot straight into a LLaMA-style AR TTS (it powers Llasa); the most LLM-native of the X-Codec line (2025).
- [Stable Codec: Scaling Transformers for Low-Bitrate High-Quality Speech Coding](https://github.com/Stability-AI/stable-codec) — Stability AI's transformer codec with an FSQ bottleneck hitting clean speech at 400-700 bps; pushes the bitrate floor well below RVQ baselines (2024).
- [TS3-Codec: Transformer-Based Simple Streaming Single Codec](https://arxiv.org/abs/2411.18803) — First convolution-free, transformer-only streaming codec; matches/beats BigCodec at ~12% of the compute and 77% of the bitrate (2024).
- [SemantiCodec: An Ultra Low Bitrate Semantic Audio Codec for General Sound](https://arxiv.org/abs/2405.00233) — Dual encoder (AudioMAE semantic + acoustic) with a diffusion decoder at 0.31-1.40 kbps; unusually semantic-rich for *general* audio, not just speech (2024).
- [NeuCodec](https://huggingface.co/neuphonic/neucodec) — Neuphonic's 0.8 kbps FSQ codec whose baked-in redundancy stays robust over noisy channels; a practical FSQ-over-RVQ argument for real-world pipelines (2025).
- [UniSRCodec: Unified and Low-Bitrate Single Codebook Codec with Sub-Band Reconstruction](https://arxiv.org/abs/2601.02776) — A high-sample-rate single-codebook codec using mel + sub-band reconstruction, closing the "single codebook yet high fidelity at high sample rate" gap (2026).
- [Scaling Speech Tokenizers with Diffusion Autoencoders](https://arxiv.org/abs/2602.06602) — ICLR 2026; replaces the usual GAN/RVQ recipe with a scaled diffusion-autoencoder tokenizer, arguing the diffusion decoder is what unlocks quality at scale (2026).
- [Mimi (Kyutai)](https://huggingface.co/kyutai/mimi) — The 12.5 Hz / ~1.1 kbps streaming semantic+acoustic codec behind Moshi; a foundational low-latency tokenizer for speech LMs (2024).
- [FocalCodec: Low-Bitrate Speech Coding via Focal Modulation](https://arxiv.org/abs/2502.04465) — A single binary-codebook ultra-low-bitrate codec (NeurIPS 2025) that pushes the single-codebook frontier (2025).

## 🎤 Singing Voice Synthesis

- [DiffSinger: Singing Voice Synthesis via Shallow Diffusion Mechanism](https://github.com/openvpi/DiffSinger) — The canonical open singing-voice synthesis system (shallow-diffusion acoustic model); the de-facto base for the open SVS ecosystem (2022).

## 📊 Benchmarks & Datasets

### Datasets

- [LibriSpeech](https://www.openslr.org/12) — 1000-hour read-English corpus from LibriVox; the universal speech baseline (2015).
- [LibriTTS](https://www.openslr.org/60/) — Google's 24 kHz sentence-segmented multi-speaker LibriSpeech derivative; a near-universal TTS training set (2019).
- [LibriTTS-R](https://www.openslr.org/141/) — LibriTTS cleaned with Miipher restoration: same transcripts, higher audio quality, the preferred drop-in today (2023).
- [Emilia: An Extensive, Multilingual, and Diverse Speech Dataset for Large-Scale Speech Generation](https://arxiv.org/abs/2407.05361) — 101k+ hours of *in-the-wild* speech across six languages plus the open Emilia-Pipe stack; pushed TTS toward spontaneous, expressive speech (2024).
- [GigaSpeech: 10,000 Hours of Transcribed Audio](https://arxiv.org/abs/2106.06909) — 10k labeled hours of audiobooks/podcasts/YouTube; a varied natural-speech source (2021).
- [Multilingual LibriSpeech (MLS)](https://arxiv.org/abs/2012.03411) — ~50k hours across 8 languages; the standard open multilingual training corpus (2020).
- [CSTR VCTK Corpus](https://datashare.ed.ac.uk/handle/10283/3443) — 110 English speakers, diverse accents, studio quality; the canonical small multi-speaker set for cloning/adaptation (2019).
- [The LJ Speech Dataset](https://keithito.com/LJ-Speech-Dataset/) — ~24 hours of a single public-domain voice; the "hello world" of single-speaker TTS (2017).
- [Common Voice (Mozilla)](https://commonvoice.mozilla.org/en/datasets) — The largest crowdsourced openly-licensed multilingual corpus, 100+ languages (2017–ongoing).

### Benchmarks & Metrics

- [Seed-TTS-eval](https://github.com/BytedanceSpeech/seed-tts-eval) — ByteDance's 3,000-sample objective test set (EN Common Voice + ZH DiDiSpeech-2) with WER + speaker-SIM scripts; the de-facto standard for zero-shot WER/SIM reporting (2024).
- [TTSDS — Text-to-Speech Distribution Score](https://arxiv.org/abs/2407.12707) — A reference-free metric scoring distributional closeness to real speech; benchmarked 35 systems with strong human correlation (2024).
- [TTSDS2: Resources and Benchmark for Evaluating Human-Quality TTS Systems](https://arxiv.org/abs/2506.19441) — Robust multilingual successor across 14 languages with 11k+ MOS ratings; the only one of 16 metrics it tested to correlate >0.50 in every domain (2025).
- [EmergentTTS-Eval: Evaluating TTS Models on Complex Prosodic, Expressiveness, and Linguistic Challenges Using Model-as-a-Judge](https://arxiv.org/abs/2505.23009) — 1,645 LLM-expanded hard cases judged by an audio LLM; targets the expressiveness gaps that plain MOS misses (2025).
- [Codec-SUPERB: An In-Depth Analysis of Sound Codec Models](https://arxiv.org/abs/2402.13071) — Community benchmark and leaderboard for neural audio codecs; essential now that codec tokens underpin modern TTS (2024).
- [DNSMOS P.835](https://arxiv.org/abs/2110.01763) — Microsoft's reference-free SIG/BAK/OVRL predictor, widely repurposed as a quick TTS quality proxy (2021).
- [UTMOS: UTokyo-SaruLab System for VoiceMOS Challenge 2022](https://arxiv.org/abs/2204.02152) — The VoiceMOS-2022-winning ensemble MOS predictor; the most-cited automatic naturalness estimator for TTS (2022).

## 🛠️ Open-source Toolkits & Implementations

- [coqui-ai/TTS](https://github.com/coqui-ai/TTS) — The de-facto open TTS library (Tacotron2, VITS, XTTS); upstream is now in maintenance mode after Coqui shut down but still heavily used (ongoing).
- [espnet/espnet](https://github.com/espnet/espnet) — End-to-end speech toolkit (ASR/TTS/ST) with hundreds of reproducible recipes; the academic reference implementation (ongoing).
- [NVIDIA-NeMo/NeMo](https://github.com/NVIDIA-NeMo/NeMo) — NVIDIA's scalable generative-AI framework with production-grade ASR/TTS; the canonical path is now `NVIDIA-NeMo/NeMo` (old `NVIDIA/NeMo` redirects) (ongoing).
- [speechbrain/speechbrain](https://github.com/speechbrain/speechbrain) — A clean, modular PyTorch all-in-one toolkit with 200+ recipes and 100+ pretrained models (ongoing).
- [open-mmlab/Amphion](https://github.com/open-mmlab/Amphion) — Audio/music/speech generation toolkit for reproducible research; consolidates many modern TTS/VC systems (MaskGCT, Vevo) in one place (ongoing).
- [SWivid/F5-TTS](https://github.com/SWivid/F5-TTS) — Reference implementation of F5-TTS; the leading 2024-era open flow-matching cloner (weights CC-BY-NC) (2024).
- [FunAudioLLM/CosyVoice](https://github.com/FunAudioLLM/CosyVoice) — Alibaba's multilingual large voice-generation model with a full train/infer/deploy stack and active v3 releases (ongoing).
- [fishaudio/fish-speech](https://github.com/fishaudio/fish-speech) — Multilingual dual-autoregressive TTS trained on 10M+ hours; strong quality under a restrictive research license (ongoing).
- [resemble-ai/chatterbox](https://github.com/resemble-ai/chatterbox) — Resemble AI's MIT-licensed SoTA TTS: 23+ languages plus low-latency turbo variants and built-in watermarking (ongoing).
- [hexgrad/kokoro](https://github.com/hexgrad/kokoro) — Inference library for Kokoro-82M, a tiny Apache-licensed model punching far above its weight; a favorite for edge/local TTS (2025).
- [neonbjb/tortoise-tts](https://github.com/neonbjb/tortoise-tts) — Quality-first autoregressive multi-voice TTS; slow but historically influential for expressive cloning (2022).
- [suno-ai/bark](https://github.com/suno-ai/bark) — Transformer text-to-audio generating speech plus nonverbal sounds/music; MIT-licensed and widely forked (2023).
- [OHF-Voice/piper1-gpl](https://github.com/OHF-Voice/piper1-gpl) — Actively-maintained successor to Piper, a fast fully-local neural TTS engine (the legacy `rhasspy/piper` is archived) (ongoing).

## 💼 Commercial & Closed Systems

Closed but field-defining — listed for completeness; no weights, API-only.

- [ElevenLabs Eleven v3](https://elevenlabs.io/blog/eleven-v3) — The most expressive commercial TTS of the cycle: inline audio tags for emotion/delivery and 70+ languages (2025).
- [OpenAI gpt-realtime / next-gen audio](https://openai.com/index/introducing-our-next-generation-audio-models/) — OpenAI's steerable speech-to-speech and `gpt-4o-mini-tts` models powering real-time voice agents (2025).
- [Cartesia Sonic 3](https://www.cartesia.ai/sonic) — State-space-model TTS with sub-100 ms streaming; the latency leader for voice agents (2025).
- [SpeechifyAI Simba 3.2](https://speechify.ai/models) — Streaming-native English TTS with SSML prosody and emotion control, with Simba 3.0 covering six languages; Coval's independent benchmark measured a 106 ms median time to first audio, the range real-time voice agents need (2026).

## 📑 Related Awesome Lists

- [ishandutta2007/Awesome-Text-to-Speech](https://github.com/ishandutta2007/Awesome-Text-to-Speech) — Product-oriented list of TTS tools, APIs, and open models; maintained into 2025/2026.
- [wenet-e2e/speech-synthesis-paper](https://github.com/wenet-e2e/speech-synthesis-paper) — The most comprehensive academic TTS paper list on GitHub (frontend, acoustic models, vocoders, VC, singing).
- [ga642381/speech-trident](https://github.com/ga642381/speech-trident) — Up-to-date survey of speech/audio LLMs, representation models, and neural codecs; the best fit for the codec/spoken-LLM angle.
- [dreamtheater123/Awesome-SpeechLM-Survey](https://github.com/dreamtheater123/Awesome-SpeechLM-Survey) — Companion to an ACL 2025 SpeechLM survey, cataloging SpeechLMs, tokenizers, codecs, datasets, and benchmarks.
- [liusongxiang/Large-Audio-Models](https://github.com/liusongxiang/Large-Audio-Models) — Tracker for large audio models (spoken LMs, prompt-based synthesis, audio SSL); last major update ~late 2024.
- [JeffC0628/awesome-voice-conversion](https://github.com/JeffC0628/awesome-voice-conversion) — Dedicated voice-conversion list (parallel/non-parallel, singing VC, VCC datasets); maintained into 2025.
- [wildminder/awesome-ai-voice](https://github.com/wildminder/awesome-ai-voice) — Practitioner list of open TTS/voice-cloning/music models with comparison tables and HF links; very current, with entries into early 2026.

---

## 🤝 Contributing

Contributions are welcome! See [CONTRIBUTING.md](CONTRIBUTING.md). In short: add your entry to the right section using `- [Title](URL) — note (year).`, verify the link resolves, and open a PR.

## 📄 License

[MIT](LICENSE) for the curation itself. Linked resources remain under their own licenses.

---

**Star ⭐ this repo if it helps you keep up with text-to-speech.**
