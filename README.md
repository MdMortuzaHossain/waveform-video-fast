# Waveform Video Fast

Live app: https://mdmortuzahossain.github.io/waveform-video-fast/

A single-file static app that turns uploaded audio into an animated, scrolling amplitude waveform video. Uses WebCodecs through Mediabunny 1.61.4 to encode frames directly, without audio playback or real-time MediaRecorder capture.

## Use

Open the app in a current desktop Chrome or Edge browser. Choose colors, background, title, resolution, and frame rate before selecting an audio file. File selection starts processing automatically. When the video is complete, an automatic download is requested; a manual download link remains available if the browser blocks it.

For long audio, start with 360p / 12 FPS. Higher resolution and frame rate increase encoding time. Processing speed is measured and displayed; no fixed completion time is guaranteed.

## Implementation

- Reads audio via a BlobSource and AudioBufferSink in two passes.
- Stores a compact 200 Hz peak amplitude envelope, rather than retaining the entire decoded audio track.
- Generates timestamped canvas frames and encodes audio/video concurrently in quarter-second chunks with backpressure.
- Tries H.264/AAC MP4 first, then VP8/Opus WebM depending on codec availability.
- Preserves audible audio in the resulting video. Processing itself is silent.
- Supports cancellation, progress, reusable export, gradients, and uploaded images.

The final encoded file is held in memory for download. Estimated outputs above 850 MiB are rejected; actual memory limits depend on the device. Input limit: 500 MiB. No file is sent to a server. Tailwind and the pinned media library load from CDNs.

## Hosting

GitHub Pages: deploy main branch / root. No build step, backend, API key, cross-origin isolation, or installation is required.

Media library documentation: https://mediabunny.dev/guide/writing-media-files
