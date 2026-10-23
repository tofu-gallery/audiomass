> Tofu gallery copy, 2026-10-23: this is the repository-root `THIRD_PARTY_NOTICES.md` of pkalogiros/AudioMass, copied into the app folder (`src`) so the notices travel with the imported app. Changed by Tofu: the leading `src/` is dropped from every path (they are relative to this folder), and the WaveSurfer.js row also names the copies in `vendor/wavesurfer/` that `index.html` loads. The licence and the table are otherwise as upstream wrote them.

# Third-party notices

The bundled third-party files keep their own licenses:

| Project | Files | License |
| --- | --- | --- |
| WaveSurfer.js 2.0.5 and regions plugin | `dist/wavesurfer.js`, `dist/plugin/wavesurfer.regions.js` (also copied byte for byte to `vendor/wavesurfer/`, with the licence text in `vendor/wavesurfer/LICENSE`) | BSD-3-Clause |
| lamejs / LAME MP3 encoder | `lame.js` | LGPL |
| libFLAC 1.3.3 | `flac.js`, `flac.min.js`, `libflac.js`, `libflac.wasm` | Xiph/New BSD |
| RNNoise | `rnn_denoise.js`, `rnn_denoise.wasm` | BSD-3-Clause |
| lz4-wasm | `lzma.js`, `lz4-block-codec-wasm.js`, `lz4-block-codec.wasm` | BSD-2-Clause |
