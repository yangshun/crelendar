# Research Notes: HTML5 Media APIs — Capturing Video & Audio in the Browser
**Date:** TBD (publish date)
**Researched:** 2026-02-25

## Manager Requirements
From parent task description:
- Introduce how HTML5 provides built-in APIs to interact with media and UI without plugins
- Using `<video>` and `<audio>`, devs can capture and play streams from the user's camera or microphone
- Focus on how these elements work, how to access device streams securely, and how to handle fallback scenarios
- CTA: "Practice HTML Interview Questions by ex-FAANG interviewers" — https://www.greatfrontend.com/questions/html-interview-questions

**Sanity-check notes:**
- The title says "HTML5" but these are really Web APIs (Media Capture and Streams API, MediaRecorder API, Screen Capture API, etc.). "HTML5" is the colloquial umbrella. Will use "HTML5" in framing but be precise about API names.
- `<video>` and `<audio>` are display/playback elements — they don't "capture" anything. The capture is done by `getUserMedia()`. Will clarify this distinction without being pedantic.
- CTA URL verified live. Page offers 70+ HTML coding and quiz questions by ex-FAANG interviewers.

---

## 1. Core APIs — Technical Facts & Verified Code Snippets

### 1A. navigator.mediaDevices.getUserMedia()

**What it does:** Prompts the user for permission to use a media input (camera/microphone), returns a Promise that resolves to a `MediaStream`.

**Baseline status:** Widely available since September 2017. Supported in all modern browsers.

**Basic camera access (7 lines):**
```javascript
async function startCamera() {
  const stream = await navigator.mediaDevices.getUserMedia({
    video: true,
    audio: true,
  });
  document.querySelector('video').srcObject = stream;
}
```

**With constraints:**
```javascript
const stream = await navigator.mediaDevices.getUserMedia({
  video: {
    width: { min: 1024, ideal: 1280, max: 1920 },
    height: { min: 576, ideal: 720, max: 1080 },
    frameRate: { ideal: 30, max: 60 },
  },
  audio: {
    echoCancellation: true,
    noiseSuppression: true,
  },
});
```

**Switching front/back camera (mobile):**
```javascript
// Front camera (selfie)
const frontStream = await navigator.mediaDevices.getUserMedia({
  video: { facingMode: 'user' },
});

// Back camera (environment) — 'exact' = fail if unavailable
const backStream = await navigator.mediaDevices.getUserMedia({
  video: { facingMode: { exact: 'environment' } },
});
```

**Important:** You must stop all tracks on the current stream before switching cameras. Failing to do this is a common source of bugs.

```javascript
async function switchCamera(currentStream, facingMode) {
  // Stop existing tracks first
  currentStream.getTracks().forEach((track) => track.stop());

  // Request new stream
  return navigator.mediaDevices.getUserMedia({
    video: { facingMode: { exact: facingMode } },
  });
}
```

Sources:
- [MDN — getUserMedia()](https://developer.mozilla.org/en-US/docs/Web/API/MediaDevices/getUserMedia)
- [Addpipe — Getting Started with getUserMedia in 2026](https://blog.addpipe.com/getusermedia-getting-started/)
- [web.dev — Capture audio and video in HTML5](https://web.dev/articles/getusermedia-intro)

---

### 1B. `<video>` and `<audio>` Elements — Displaying Streams

**How they connect to streams:** The `.srcObject` property accepts a `MediaStream` object. This replaced the old `URL.createObjectURL(stream)` pattern (now deprecated for streams).

```html
<video id="preview" autoplay playsinline muted></video>
<audio id="audioPreview" autoplay></audio>
```

```javascript
const video = document.getElementById('preview');
const stream = await navigator.mediaDevices.getUserMedia({ video: true, audio: true });

// Attach live stream to video element
video.srcObject = stream;
```

**Key attributes:**
- `autoplay` — starts playing when stream is attached
- `playsinline` — prevents iOS from going fullscreen (critical for mobile)
- `muted` — required for autoplay to work without user gesture (browser policy); also prevents audio feedback loop when capturing mic

**Note:** `<video>` handles both video-only and video+audio streams. Use `<audio>` only when there's no video track.

Sources:
- [MDN — HTMLMediaElement.srcObject](https://developer.mozilla.org/en-US/docs/Web/API/HTMLMediaElement/srcObject)
- [MDN — Audio and video delivery](https://developer.mozilla.org/en-US/docs/Web/Media/Guides/Audio_and_video_delivery)

---

### 1C. MediaRecorder API — Recording Audio/Video

**Baseline status:** Widely available since April 2021.

**Complete recording + download example:**
```javascript
async function recordVideo() {
  const stream = await navigator.mediaDevices.getUserMedia({
    video: true,
    audio: true,
  });

  const mediaRecorder = new MediaRecorder(stream, {
    mimeType: 'video/webm; codecs=vp9',
  });

  const chunks = [];

  mediaRecorder.ondataavailable = (event) => {
    if (event.data.size > 0) chunks.push(event.data);
  };

  mediaRecorder.onstop = () => {
    const blob = new Blob(chunks, { type: 'video/webm' });
    const url = URL.createObjectURL(blob);
    const a = document.createElement('a');
    a.href = url;
    a.download = 'recording.webm';
    a.click();
    URL.revokeObjectURL(url); // Clean up
  };

  mediaRecorder.start();

  // Stop after 10 seconds
  setTimeout(() => mediaRecorder.stop(), 10000);
}
```

**Key methods:** `start(timeslice?)`, `stop()`, `pause()`, `resume()`, `requestData()`

**Key events:** `dataavailable`, `stop`, `error`, `pause`, `resume`, `start`

**States:** `"inactive"`, `"recording"`, `"paused"`

**Static method for MIME type checking:**
```javascript
MediaRecorder.isTypeSupported('video/webm; codecs=vp9'); // true/false
MediaRecorder.isTypeSupported('video/mp4');               // varies by browser
```

**MIME type support across browsers:**
| MIME Type | Chrome | Firefox | Safari |
|---|---|---|---|
| `video/webm` | Yes | Yes | No |
| `video/webm; codecs=vp9` | Yes | Yes | No |
| `video/mp4` | Yes (Chrome 116+) | No | Yes |
| `audio/webm` | Yes | Yes | No |
| `audio/ogg; codecs=opus` | Yes | Yes | No |
| `audio/mp4` | Yes | No | Yes |

Sources:
- [MDN — MediaRecorder](https://developer.mozilla.org/en-US/docs/Web/API/MediaRecorder)
- [Chrome Developers — Record audio and video with MediaRecorder](https://developer.chrome.com/blog/mediarecorder)
- [Addpipe — MediaRecorder API](https://blog.addpipe.com/mediarecorder-api/)
- [MDN — Using the MediaStream Recording API](https://developer.mozilla.org/en-US/docs/Web/API/MediaStream_Recording_API/Using_the_MediaStream_Recording_API)

---

### 1D. Screen Capture API — getDisplayMedia()

**Baseline status:** NOT Baseline. Not available in all widely-used browsers. Works in Chrome, Edge, Firefox. Safari support is partial.

```javascript
async function startScreenShare() {
  const stream = await navigator.mediaDevices.getDisplayMedia({
    video: {
      displaySurface: 'browser', // "browser" | "window" | "monitor"
    },
    audio: {
      suppressLocalAudioPlayback: true,
    },
    preferCurrentTab: false,
    selfBrowserSurface: 'exclude',
    systemAudio: 'include',
    surfaceSwitching: 'include',
  });

  document.querySelector('video').srcObject = stream;
}
```

**Key difference from getUserMedia():**
- No `facingMode`, `deviceId` constraints
- User picks what to share via browser-native picker (tab, window, or screen)
- Screen sharing sources are NOT enumerable via `enumerateDevices()`
- Requires `display-capture` Permissions Policy

**Stopping screen share properly:**
```javascript
function stopScreenShare(videoElement) {
  const tracks = videoElement.srcObject.getTracks();
  tracks.forEach((track) => track.stop());
  videoElement.srcObject = null;
}
```

**Permissions Policy header:**
```http
Permissions-Policy: display-capture=(self)
```

**iframe allow attribute:**
```html
<iframe src="https://app.example.com" allow="display-capture"></iframe>
```

Sources:
- [MDN — Screen Capture API](https://developer.mozilla.org/en-US/docs/Web/API/Screen_Capture_API)
- [MDN — Using Screen Capture](https://developer.mozilla.org/en-US/docs/Web/API/Screen_Capture_API/Using_Screen_Capture)
- [MDN — getDisplayMedia()](https://developer.mozilla.org/en-US/docs/Web/API/MediaDevices/getDisplayMedia)

---

### 1E. MediaStream API — Working with Tracks

A `MediaStream` contains zero or more `MediaStreamTrack` objects (audio and/or video tracks).

```javascript
const stream = await navigator.mediaDevices.getUserMedia({
  video: true,
  audio: true,
});

// Get individual tracks
const videoTracks = stream.getVideoTracks(); // MediaStreamTrack[]
const audioTracks = stream.getAudioTracks(); // MediaStreamTrack[]
const allTracks = stream.getTracks();        // both

// Mute audio (disable track, not remove)
audioTracks[0].enabled = false;

// Stop a specific track (releases hardware)
videoTracks[0].stop();

// Check track state
console.log(videoTracks[0].readyState); // "live" or "ended"

// Get device capabilities after stream is active
const capabilities = videoTracks[0].getCapabilities();
console.log(capabilities); // { width: {min, max}, height: {min, max}, facingMode: [...], ... }

// Get current settings
const settings = videoTracks[0].getSettings();
console.log(settings); // { width: 1280, height: 720, frameRate: 30, facingMode: "user", ... }

// Apply new constraints mid-stream
await videoTracks[0].applyConstraints({
  width: { ideal: 1920 },
  height: { ideal: 1080 },
});
```

**Track events:**
- `ended` — track ended (device disconnected, user revoked permission, or `stop()` called)
- `mute` / `unmute` — track temporarily muted (e.g., network issue or hardware interrupt)

Sources:
- [MDN — MediaStream](https://developer.mozilla.org/en-US/docs/Web/API/MediaStream)
- [MDN — MediaStream.getVideoTracks()](https://developer.mozilla.org/en-US/docs/Web/API/MediaStream/getVideoTracks)
- [MDN — MediaStream.getAudioTracks()](https://developer.mozilla.org/en-US/docs/Web/API/MediaStream/getAudioTracks)

---

### 1F. Picture-in-Picture API (Bonus)

**Baseline status:** NOT Baseline. Limited availability. Chrome/Edge support strong, Firefox support limited.

```javascript
const video = document.querySelector('video');

// Feature detection
if (document.pictureInPictureEnabled) {
  // Enter PiP
  await video.requestPictureInPicture();
}

// Exit PiP
if (document.pictureInPictureElement) {
  await document.exitPictureInPicture();
}

// Toggle pattern
async function togglePiP(video) {
  if (document.pictureInPictureElement) {
    await document.exitPictureInPicture();
  } else if (document.pictureInPictureEnabled) {
    await video.requestPictureInPicture();
  }
}
```

**Events:** `enterpictureinpicture`, `leavepictureinpicture` (on video element), `resize` (on PictureInPictureWindow)

**CSS pseudo-class:**
```css
:picture-in-picture {
  outline: 3px solid blue;
}
```

**Document Picture-in-Picture API** (experimental, Chrome 116+) allows arbitrary HTML in PiP window — not just `<video>`.

Sources:
- [MDN — Picture-in-Picture API](https://developer.mozilla.org/en-US/docs/Web/API/Picture-in-Picture_API)
- [Chrome Developers — PiP for any element](https://developer.chrome.com/docs/web-platform/document-picture-in-picture)

---

## 2. Security & Permissions Model

### HTTPS Requirement
- `getUserMedia()` and `getDisplayMedia()` are ONLY available in secure contexts
- In insecure contexts (HTTP), `navigator.mediaDevices` is `undefined` — not just the methods, the entire object
- Secure contexts: HTTPS, `file:///`, `localhost`
- This means feature detection catches insecure contexts automatically:
  ```javascript
  if (!navigator.mediaDevices?.getUserMedia) {
    // Either unsupported browser OR insecure context
  }
  ```

### Permission Prompts & States
- Browser MUST prompt the user at least on first use per origin
- Browser MUST display an indicator (icon/badge) when camera/mic is active
- The user can grant, deny, or dismiss the prompt
- **Dismissing is NOT the same as denying** — dismissed means no persistent state saved; Chrome returns `PermissionDismissedError` (non-standard)

### Permissions API Integration
```javascript
// Query permission state WITHOUT triggering a prompt
const cameraPermission = await navigator.permissions.query({ name: 'camera' });
console.log(cameraPermission.state); // "granted" | "denied" | "prompt"

const micPermission = await navigator.permissions.query({ name: 'microphone' });

// Listen for changes
cameraPermission.addEventListener('change', () => {
  console.log('Camera permission changed to:', cameraPermission.state);
});
```

**Browser support for `permissions.query({ name: 'camera' })`:**
- Chrome: Since Chrome 64 (January 2018)
- Firefox: Since Firefox 118/119 (late 2023)
- Safari: NOT supported — `permissions.query()` for camera/microphone is not available

### Handling Denied Permissions Gracefully
```javascript
async function requestCamera() {
  try {
    const stream = await navigator.mediaDevices.getUserMedia({ video: true });
    return stream;
  } catch (err) {
    switch (err.name) {
      case 'NotAllowedError':
        showMessage('Camera access denied. Please enable in browser settings.');
        break;
      case 'NotFoundError':
        showMessage('No camera found on this device.');
        break;
      case 'NotReadableError':
        showMessage('Camera is in use by another application.');
        break;
      case 'OverconstrainedError':
        showMessage('Camera does not meet the requested requirements.');
        // Retry with relaxed constraints
        return navigator.mediaDevices.getUserMedia({ video: true });
      default:
        showMessage(`Camera error: ${err.message}`);
    }
    return null;
  }
}
```

### Permissions Policy (HTTP headers & iframes)
```html
<!-- Allow camera/mic for same-origin iframes -->
<iframe src="https://video-chat.example.com" allow="camera; microphone"></iframe>

<!-- Block camera for embedded content -->
<iframe src="https://untrusted.example.com" allow="camera 'none'; microphone 'none'"></iframe>
```

```http
Permissions-Policy: camera=(self "https://trusted-partner.com"), microphone=(self)
```

### Privacy Considerations
- Browsers are required to show a recording indicator even after the stream is obtained (even if not actively recording)
- Device labels from `enumerateDevices()` are only available AFTER the user grants permission — prevents fingerprinting
- Some browsers deliberately obscure permission state details to reduce fingerprinting surface
- `getUserMedia()` cannot be called from sandboxed iframes without `allow-same-origin`
- Cannot be called from `data://` or `blob://` URLs

Sources:
- [MDN — getUserMedia() Security](https://developer.mozilla.org/en-US/docs/Web/API/MediaDevices/getUserMedia#security)
- [MDN — Permissions API](https://developer.mozilla.org/en-US/docs/Web/API/Permissions_API)
- [Addpipe — Using Permissions API to Detect getUserMedia Responses](https://blog.addpipe.com/using-permissions-api-to-detect-getusermedia-responses/)
- [Addpipe — Common getUserMedia Errors](https://blog.addpipe.com/common-getusermedia-errors/)

---

## 3. Practical Code Examples

### 3A. Basic Camera Access (minimal)
```html
<video id="camera" autoplay playsinline muted></video>
<button id="start">Start Camera</button>
<button id="stop">Stop Camera</button>

<script>
  const video = document.getElementById('camera');

  document.getElementById('start').onclick = async () => {
    video.srcObject = await navigator.mediaDevices.getUserMedia({ video: true });
  };

  document.getElementById('stop').onclick = () => {
    video.srcObject.getTracks().forEach((track) => track.stop());
    video.srcObject = null;
  };
</script>
```

### 3B. Recording Video & Downloading
```javascript
let mediaRecorder;
let chunks = [];

async function startRecording() {
  const stream = await navigator.mediaDevices.getUserMedia({
    video: true,
    audio: true,
  });

  document.querySelector('video').srcObject = stream;

  // Check for best supported format
  const mimeType = MediaRecorder.isTypeSupported('video/webm; codecs=vp9')
    ? 'video/webm; codecs=vp9'
    : 'video/webm';

  mediaRecorder = new MediaRecorder(stream, { mimeType });

  mediaRecorder.ondataavailable = (e) => {
    if (e.data.size > 0) chunks.push(e.data);
  };

  mediaRecorder.onstop = () => {
    const blob = new Blob(chunks, { type: mimeType });
    const url = URL.createObjectURL(blob);

    // Trigger download
    const a = document.createElement('a');
    a.href = url;
    a.download = `recording-${Date.now()}.webm`;
    a.click();

    // Cleanup
    URL.revokeObjectURL(url);
    chunks = [];

    // Stop all tracks (release camera/mic)
    stream.getTracks().forEach((track) => track.stop());
  };

  mediaRecorder.start();
}

function stopRecording() {
  mediaRecorder.stop();
}
```

### 3C. Switching Front/Back Camera
```javascript
let currentStream = null;
let useFrontCamera = true;

async function toggleCamera() {
  // Stop current stream
  if (currentStream) {
    currentStream.getTracks().forEach((track) => track.stop());
  }

  useFrontCamera = !useFrontCamera;

  currentStream = await navigator.mediaDevices.getUserMedia({
    video: { facingMode: useFrontCamera ? 'user' : 'environment' },
  });

  document.querySelector('video').srcObject = currentStream;
}
```

### 3D. Audio Visualization (Bonus)
```javascript
async function visualizeAudio() {
  const stream = await navigator.mediaDevices.getUserMedia({ audio: true });

  const audioCtx = new AudioContext();
  const source = audioCtx.createMediaStreamSource(stream);
  const analyser = audioCtx.createAnalyser();
  analyser.fftSize = 256;

  source.connect(analyser);
  // NOTE: Do NOT connect analyser to destination — prevents feedback loop

  const canvas = document.querySelector('canvas');
  const canvasCtx = canvas.getContext('2d');
  const bufferLength = analyser.frequencyBinCount;
  const dataArray = new Uint8Array(bufferLength);

  function draw() {
    requestAnimationFrame(draw);
    analyser.getByteFrequencyData(dataArray);

    canvasCtx.fillStyle = '#000';
    canvasCtx.fillRect(0, 0, canvas.width, canvas.height);

    const barWidth = (canvas.width / bufferLength) * 2.5;
    let x = 0;

    for (let i = 0; i < bufferLength; i++) {
      const barHeight = dataArray[i] / 2;
      canvasCtx.fillStyle = `hsl(${(i / bufferLength) * 360}, 80%, 50%)`;
      canvasCtx.fillRect(x, canvas.height - barHeight, barWidth, barHeight);
      x += barWidth + 1;
    }
  }

  draw();
}
```

Sources:
- [MDN — Visualizations with Web Audio API](https://developer.mozilla.org/en-US/docs/Web/API/Web_Audio_API/Visualizations_with_Web_Audio_API)
- [DigitalOcean — Front and Rear Camera Access](https://www.digitalocean.com/community/tutorials/front-and-rear-camera-access-with-javascripts-getusermedia)

---

## 4. Browser Support & Fallback Strategies

### Support Tiers

| API | Baseline Status | Available Since | Notes |
|---|---|---|---|
| `getUserMedia()` | Widely available | Sept 2017 | All modern browsers |
| `MediaRecorder` | Widely available | April 2021 | All modern browsers; MIME types vary |
| `MediaStream` | Widely available | Sept 2017 | Core to all media APIs |
| `enumerateDevices()` | Widely available | Sept 2017 | Labels gated behind permission |
| `getDisplayMedia()` | NOT Baseline | Partial | Chrome, Edge, Firefox; Safari partial |
| Picture-in-Picture | NOT Baseline | Partial | Chrome, Edge strong; Firefox limited |
| Document PiP | Experimental | Chrome 116+ | Chrome/Edge only |
| `permissions.query('camera')` | Partial | Varies | Not in Safari |

### Feature Detection Pattern
```javascript
function detectMediaSupport() {
  const support = {
    getUserMedia: !!navigator.mediaDevices?.getUserMedia,
    getDisplayMedia: !!navigator.mediaDevices?.getDisplayMedia,
    mediaRecorder: typeof MediaRecorder !== 'undefined',
    pictureInPicture: !!document.pictureInPictureEnabled,
    audioContext: !!(window.AudioContext || window.webkitAudioContext),
    permissionsQuery: !!navigator.permissions?.query,
  };

  return support;
}
```

### Progressive Enhancement Pattern
```javascript
async function initMedia() {
  // Level 1: Basic feature check
  if (!navigator.mediaDevices?.getUserMedia) {
    showFallbackUI('Your browser does not support camera access.');
    return;
  }

  // Level 2: Try to get stream
  try {
    const stream = await navigator.mediaDevices.getUserMedia({ video: true });
    showLivePreview(stream);

    // Level 3: Enhanced features (if available)
    if (typeof MediaRecorder !== 'undefined') {
      enableRecordingButton();
    }

    if (document.pictureInPictureEnabled) {
      enablePiPButton();
    }

    if (navigator.mediaDevices.getDisplayMedia) {
      enableScreenShareButton();
    }
  } catch (err) {
    showFallbackUI(`Camera error: ${err.message}`);
  }
}
```

### Fallback for Unsupported Browsers
```javascript
if (!navigator.mediaDevices?.getUserMedia) {
  // Option 1: File upload fallback
  showFileUploadInput();

  // Option 2: Pre-recorded video fallback
  video.src = 'fallback-demo.mp4';
}
```

Sources:
- [Can I Use — getDisplayMedia](https://caniuse.com/?search=getDisplayMedia)
- [MDN — getUserMedia Browser Compatibility](https://developer.mozilla.org/en-US/docs/Web/API/MediaDevices/getUserMedia#browser_compatibility)
- [MDN — MediaRecorder Browser Compatibility](https://developer.mozilla.org/en-US/docs/Web/API/MediaRecorder#browser_compatibility)

---

## 5. Content Landscape Research

### Existing Posts (What's Out There)

| Post | Source | Year | Angle |
|---|---|---|---|
| "Getting Started With getUserMedia in 2026" | Addpipe Blog | 2026 | Comprehensive beginner setup guide |
| "Capture audio and video in HTML5" | web.dev (Google) | 2024 update | Original intro, now somewhat dated |
| "Creating Media in the Browser" | Medium (Hajagha Hasanli) | 2025 | Screen capture + MediaRecorder focus |
| "MediaRecorder API in Action" | Addpipe Blog | 2025 | Deep-dive on recording only |
| "Recording Audio in the Browser" | Addpipe Blog | 2025 | Audio-only recording |
| "Front and Rear Camera Access" | DigitalOcean | 2020 | Mobile camera switching |
| "An Introduction to the getUserMedia API" | SitePoint | Older | Basic intro |
| "Using the Media Capture API" | SitePoint | 2024 | getUserMedia starting point |
| MDN tutorials (multiple) | MDN | Ongoing | Reference docs, not tutorial-style |

### What's MISSING / Fresh Angles

1. **No single post covers the full API ecosystem together.** Most posts cover getUserMedia OR MediaRecorder OR Screen Capture in isolation. A unified "here's the full toolbox" post would fill a gap.

2. **Security/permissions model is under-covered.** Most tutorials show `try/catch` with a generic error message. Few cover the Permissions API integration, permission states, or the distinction between denied vs. dismissed.

3. **Track lifecycle management is rarely taught.** The "forgetting to stop tracks" gotcha is mentioned in bug reports but almost never in tutorials.

4. **Mobile-specific considerations are scattered.** `playsinline`, `facingMode`, OS-level permission differences (macOS requiring per-browser camera approval) are rarely consolidated.

5. **Progressive enhancement patterns for media APIs are almost non-existent.** Most posts assume support and skip fallback entirely.

6. **Audio visualization connected to getUserMedia is rare.** Most Web Audio tutorials use file input, not live mic input.

### Recommended Angle for This Post
Position as "the complete practical guide to browser media capture" — covering the APIs as an integrated toolkit, with security-first framing and real gotchas that tutorials skip. The unified coverage + permission model depth + cleanup best practices would differentiate from existing content.

---

## 6. Non-Obvious Insights & Gotchas

### Gotcha 1: Forgetting to Stop Tracks (Most Common Bug)
```javascript
// BAD — camera stays on after closing modal/navigating away
video.srcObject = null; // Clears the display but does NOT release the camera

// GOOD — stop every track, THEN clear srcObject
stream.getTracks().forEach((track) => track.stop());
video.srcObject = null;
```
The camera indicator light stays on until tracks are stopped. In SPAs (React, Vue), this means cleanup must happen in unmount/destroy lifecycle hooks.

### Gotcha 2: React StrictMode Double-Mount
In React 18+ development mode with StrictMode, `useEffect` runs twice. This means:
- `getUserMedia()` is called twice
- The first stream's cleanup may run before the promise resolves
- The `streamRef` is null when cleanup runs, leaking the first stream
- Solution: use an `AbortController` pattern or track the mounted state

### Gotcha 3: `autoplay` Requires `muted` for Live Streams
Browsers block autoplay with audio. If you attach a stream with an audio track to a `<video>` element without `muted`, it won't autoplay. This trips up developers who add `audio: true` to their constraints.

### Gotcha 4: macOS Per-Browser Camera Permission
On macOS, every non-Safari browser needs to be individually granted camera/microphone permission at the OS level (System Preferences > Privacy & Security > Camera). The browser then needs to be restarted. This is separate from the in-browser permission prompt. Users often don't realize this and blame the web app.

### Gotcha 5: `enumerateDevices()` Returns Blank Labels Before Permission
```javascript
// Before getUserMedia() — labels are empty for privacy
const devices = await navigator.mediaDevices.enumerateDevices();
// [{ deviceId: "abc", label: "", kind: "videoinput" }]

// After getUserMedia() grant — labels populated
const devices = await navigator.mediaDevices.enumerateDevices();
// [{ deviceId: "abc", label: "FaceTime HD Camera", kind: "videoinput" }]
```

### Gotcha 6: Permissions API vs. getUserMedia Permission States
- `navigator.permissions.query({ name: 'camera' })` returns `"prompt"` / `"granted"` / `"denied"` — but NOT supported in Safari
- This is a read-only query; it does NOT trigger a permission prompt
- The actual permission request only happens when `getUserMedia()` is called
- Some browsers deliberately return vague states to prevent fingerprinting
- `getUserMedia()` can still fail with `NotAllowedError` even when `permissions.query` says `"granted"` (e.g., OS-level block on macOS)

### Gotcha 7: Memory Leaks with Screen Sharing
Screen sharing via `getDisplayMedia()` can hold ~100MB of memory in heap-unclassified. Stopping tracks before closing the tab doesn't always free this memory immediately.

### Gotcha 8: `NotReadableError` Means "Device Busy"
When another application (Zoom, Teams, FaceTime) has exclusive access to the camera, `getUserMedia()` throws `NotReadableError`, not `NotFoundError`. On Windows, this is particularly common because of exclusive device access.

### Mobile vs. Desktop Differences Summary

| Aspect | Desktop | Mobile |
|---|---|---|
| Camera count | Usually 1 | Usually 2 (front + back) |
| `facingMode` | Mostly ignored | Critical for UX |
| `playsinline` needed | No | Yes (iOS requires it) |
| Permission persistence | Per-origin, persistent | Often per-session (Safari iOS) |
| OS-level permissions | macOS: per-browser | iOS: per-app; Android: per-app |
| Screen sharing | Full support | Very limited (Android Chrome partial, iOS none) |

Sources:
- [Addpipe — Common getUserMedia Errors](https://blog.addpipe.com/common-getusermedia-errors/)
- [MDN — MediaStreamTrack.stop()](https://developer.mozilla.org/en-US/docs/Web/API/MediaStreamTrack/stop)
- [DEV Community — Stopping a Webcam with JavaScript](https://dev.to/morinoko/stopping-a-webcam-with-javascript-4297)
- [Bugzilla — getUserMedia memory leak](https://bugzilla.mozilla.org/show_bug.cgi?id=1053737)
- [Twilio — Choosing Cameras](https://www.twilio.com/en-us/blog/choosing-cameras-javascript-mediadevices-api-html)
- [What Web Can Do Today — Camera](https://whatwebcando.today/articles/choose-front-back-camera-stream/)

---

## 7. GFE CTA Page Analysis

**URL:** https://www.greatfrontend.com/questions/html-interview-questions
**Status:** Live, verified.

**What the page offers:**
- 70+ HTML interview questions (mix of coding + quiz)
- ~29 hours of total practice material
- In-browser coding environment (no local setup needed)
- Automated test cases for code validation
- Expert solutions written by ex-FAANG senior/staff engineers
- Framework options: React, Vue, Angular, Svelte, Vanilla JS
- Difficulty levels: Easy to Hard
- Freemium model: some free questions, premium questions require paid access

**Topics covered:**
- Semantic markup and content structuring
- Forms and user input handling
- Accessibility standards
- Multimedia elements
- Interactive web page creation
- Media handling

**CTA angle for this post:** The page covers multimedia elements and media handling — directly relevant to the HTML5 media APIs topic. A natural bridge: "Now that you understand browser media APIs, practice building with them in interview-style challenges."

**Pipeline rule reminder:** Do NOT hardcode question counts (the "70+" may change).

---

## All Sources

### Primary MDN References
- [getUserMedia()](https://developer.mozilla.org/en-US/docs/Web/API/MediaDevices/getUserMedia)
- [MediaRecorder](https://developer.mozilla.org/en-US/docs/Web/API/MediaRecorder)
- [MediaStream](https://developer.mozilla.org/en-US/docs/Web/API/MediaStream)
- [Screen Capture API](https://developer.mozilla.org/en-US/docs/Web/API/Screen_Capture_API)
- [Using Screen Capture](https://developer.mozilla.org/en-US/docs/Web/API/Screen_Capture_API/Using_Screen_Capture)
- [getDisplayMedia()](https://developer.mozilla.org/en-US/docs/Web/API/MediaDevices/getDisplayMedia)
- [Picture-in-Picture API](https://developer.mozilla.org/en-US/docs/Web/API/Picture-in-Picture_API)
- [Permissions API](https://developer.mozilla.org/en-US/docs/Web/API/Permissions_API)
- [Visualizations with Web Audio API](https://developer.mozilla.org/en-US/docs/Web/API/Web_Audio_API/Visualizations_with_Web_Audio_API)
- [MediaStreamTrack.stop()](https://developer.mozilla.org/en-US/docs/Web/API/MediaStreamTrack/stop)
- [Using the MediaStream Recording API](https://developer.mozilla.org/en-US/docs/Web/API/MediaStream_Recording_API/Using_the_MediaStream_Recording_API)
- [Audio and Video Delivery](https://developer.mozilla.org/en-US/docs/Web/Media/Guides/Audio_and_video_delivery)

### Tutorials & Blog Posts
- [Addpipe — Getting Started with getUserMedia in 2026](https://blog.addpipe.com/getusermedia-getting-started/)
- [Addpipe — Common getUserMedia Errors](https://blog.addpipe.com/common-getusermedia-errors/)
- [Addpipe — MediaRecorder API](https://blog.addpipe.com/mediarecorder-api/)
- [Addpipe — Using Permissions API](https://blog.addpipe.com/using-permissions-api-to-detect-getusermedia-responses/)
- [web.dev — Capture audio and video in HTML5](https://web.dev/articles/getusermedia-intro)
- [Chrome Developers — Record audio and video with MediaRecorder](https://developer.chrome.com/blog/mediarecorder)
- [Chrome Developers — PiP for any element](https://developer.chrome.com/docs/web-platform/document-picture-in-picture)
- [DigitalOcean — Front and Rear Camera Access](https://www.digitalocean.com/community/tutorials/front-and-rear-camera-access-with-javascripts-getusermedia)
- [Twilio — Choosing Cameras](https://www.twilio.com/en-us/blog/choosing-cameras-javascript-mediadevices-api-html)
- [DEV Community — Stopping a Webcam](https://dev.to/morinoko/stopping-a-webcam-with-javascript-4297)
- [What Web Can Do Today — Camera Selection](https://whatwebcando.today/articles/choose-front-back-camera-stream/)

### Browser Support
- [Can I Use — getDisplayMedia](https://caniuse.com/?search=getDisplayMedia)

### Bug Reports & Specs
- [Bugzilla — getUserMedia Memory Leak](https://bugzilla.mozilla.org/show_bug.cgi?id=1053737)
- [Electron — MediaRecorder Memory Leak](https://github.com/electron/electron/issues/41123)
- [W3C — Media Capture and Streams Spec](https://w3c.github.io/mediacapture-main/)
