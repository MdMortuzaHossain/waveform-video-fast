# Waveform Video Fast

Live app: https://mdmortuzahossain.github.io/waveform-video-fast/

Single-file GitHub Pages app. Upload audio to silently render an animated waveform video with WebCodecs and Mediabunny 1.61.4. No real-time playback is required. Automatic download has a manual fallback.

## Controls

All nine styles remain: bars, line, center-out, bottom, circle, radial rays, twin wave, layered ribbon, and dots. Videos contain no text. Customize two waveform colors, width, solid/gradient/image backgrounds, 360p/720p/1080p, and 6/8/12/24/30 FPS.

Small (default), Balanced, and High control video bitrate. High preserves previous video bitrate budgets. Audio offers 64/96/128/192 kbps; default 96. Select Auto (MP4 preferred), explicit MP4, or WebM (VP9 preferred, VP8 fallback). Unsupported explicit formats report an error. Small at 360p/12 FPS targets 240 kbps video plus 96 kbps audio, versus the previous 700+128 kbps. Estimates are bitrate budgets, not guaranteed file sizes. Image backgrounds and complex motion can affect compression.

## Implementation and limits

- Two streaming decode passes; compact peak envelope and frequency-band arrays.
- Reused FFT buffers, precomputed window/twiddles, media-time smoothing.
- Audio/video encoded concurrently in bounded quarter-second batches.
- Variable video bitrate and six-second keyframe spacing.
- Progress, cancellation, retry, and local-only file processing.
- Final output held in RAM; estimated outputs over 850 MiB rejected. Inputs limited to 500 MiB and eight hours. Device memory can impose lower limits.
- Use current desktop Chrome/Edge. Encoding speed and codec support depend on hardware/browser. VP9 may be slower.

Choose settings before uploading, or change settings and use the retry button afterward. Start with 360p/12 FPS/Small for long audio. No speed or exact size guarantee.

Deploy main branch root with GitHub Pages; no build or server required. Tailwind and pinned Mediabunny load from CDNs.

Documentation: https://mediabunny.dev/guide/writing-media-files
