# ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
# BRIEF INFO
# ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

# HTML5 Media APIs: Capturing Video & Audio in the Browser

- **Date:** 2026-03-25
- **Topic:** Browser-native media capture APIs — getUserMedia, MediaRecorder, getDisplayMedia, and Picture-in-Picture
- **Pillar:** 🔍 Deep Dive / Technical Education
- **Format:** Carousel
- **Format rationale:** 4 distinct APIs, each requiring a code snippet and explanation. Carousel supports code-per-slide at readable mobile size. The previous post (Tue Tools 2) was also carousel, but this topic mechanically requires it for code blocks. 8 slides (hook + 4 APIs + security + gotchas + CTA).
- **Key angle:** You don't need a library to capture video, record audio, or share your screen. The browser has built-in APIs for all of it — and most devs have never used them. This post shows the code for each, plus the security model that makes it safe.
- **GFE tie-in:** CTA slide + caption link to GFE HTML interview questions.
- **Design inspiration:** Codemia coding concept style — dark bg, syntax-highlighted code, clean code editor aesthetic
- **Color theme:** Dark (navy/black bg)
- **Accent color:** HTML orange (#E34C26) for primary accents. Green for "working" code, red for common mistakes.


# ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
# CAPTION
# ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

## LinkedIn Caption
You can access the camera, record video, capture the screen, and play Picture-in-Picture — all with browser-native APIs. No libraries.

You probably know `<video>` and `<audio>`, but have you used `getUserMedia()`, `MediaRecorder`, or `getDisplayMedia()`? These APIs ship in every modern browser and they're simpler than you think.

Here's the code for each one, plus the security gotcha you need to know (hint: it won't work without HTTPS).

Which API are you going to try first?

#HTML5 #JavaScript #WebDevelopment #FrontEnd #MediaAPIs #GreatFrontEnd

Practice HTML interview questions with detailed solutions by ex-FAANG interviewers: https://www.greatfrontend.com/questions/html-interview-questions?utm_source=linkedin&utm_medium=social&utm_campaign=html5-media_mar+2026


# ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
# CONTENT BRIEF — Format A: Carousel
# ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

## Slide 1 — Hook
**Title:** HTML5 Media APIs You Should Know
**Subtitle:** Camera, microphone, screen capture, recording — no libraries needed
**Visual direction:**
- Layout: Large title centered, subtitle below. Camera/microphone/screen icons.
- Key elements: HTML5 logo or shield. Media device icons.
- Style notes: Dark bg, code editor aesthetic. "No libraries" emphasized.

## Slide 2 — getUserMedia: Access the Camera
**Headline:** getUserMedia(): Access Camera & Mic
- Browser-native access to camera and microphone. Returns a MediaStream.
- Code snippet:
  ```javascript
  const stream = await navigator.mediaDevices
    .getUserMedia({ video: true, audio: true });

  const video = document.querySelector("video");
  video.srcObject = stream;
  ```
- Works in all modern browsers. Requires HTTPS (won't even exist on HTTP).
**Visual direction:**
- Layout: Headline top. Code block centered. "Requires HTTPS" callout below.
- Key elements: Code block is the anchor. HTTPS warning badge.
- Style notes: Clean syntax highlighting. Keep the code to 4-5 lines — simplicity is the point.

## Slide 3 — MediaRecorder: Record Video
**Headline:** MediaRecorder: Record & Download
- Records any MediaStream as a video/audio file. No server needed.
- Code snippet:
  ```javascript
  const recorder = new MediaRecorder(stream);
  const chunks = [];

  recorder.ondataavailable = e => chunks.push(e.data);
  recorder.onstop = () => {
    const blob = new Blob(chunks, { type: "video/webm" });
    const url = URL.createObjectURL(blob);
    // Download or play the recording
  };

  recorder.start();
  ```
**Visual direction:**
- Layout: Headline top. Code block centered. "No server needed" callout.
- Key elements: Code showing the record → collect chunks → create blob flow.
- Style notes: The code is slightly longer — ensure readable font size. The flow (start → collect → blob) should be visually clear.

## Slide 4 — getDisplayMedia: Screen Capture
**Headline:** getDisplayMedia(): Screen Sharing
- Capture the user's screen, a window, or a specific tab. Same API pattern as getUserMedia.
- Code snippet:
  ```javascript
  const screen = await navigator.mediaDevices
    .getDisplayMedia({
      video: { displaySurface: "browser" },
      audio: true
    });

  video.srcObject = screen;
  ```
- Combine with MediaRecorder to build screen recording in pure JS.
**Visual direction:**
- Layout: Headline top. Code block centered. "Combine with MediaRecorder" note.
- Key elements: Screen/monitor icon. Code block showing getDisplayMedia call.
- Style notes: Emphasize that this is the same pattern as getUserMedia — the APIs are consistent.

## Slide 5 — Picture-in-Picture
**Headline:** Picture-in-Picture: Float Any Video
- Float a video in a persistent mini-player that stays on top across tabs.
- Code snippet:
  ```javascript
  const video = document.querySelector("video");

  // Enter PiP
  await video.requestPictureInPicture();

  // Exit PiP
  document.exitPictureInPicture();
  ```
- Works with any `<video>` element. Two lines of code.
**Visual direction:**
- Layout: Headline top. Code block centered. "Two lines of code" callout.
- Key elements: PiP floating window icon. Code simplicity is the hook.
- Style notes: Shortest code block — emphasize how simple this is.

## Slide 6 — Security & Gotchas
**Headline:** 3 Things That Trip Everyone Up
- ⚠️ **HTTPS required.** `navigator.mediaDevices` is literally `undefined` on HTTP. No fallback.
- ⚠️ **Stop your tracks.** Forgetting `stream.getTracks().forEach(t => t.stop())` leaves the camera light on. In React, this leaks on unmount.
- ⚠️ **Mobile quirks.** iOS requires `playsinline` attribute on video. Android `facingMode: "environment"` for back camera.
**Visual direction:**
- Layout: Headline top. 3 warning items with orange ⚠️ markers.
- Key elements: Warning triangles. HTTPS, track cleanup, and mobile as 3 compact gotcha rows.
- Style notes: No code block — just punchy text. This is the "save this slide" reference.

## Final Slide — CTA
**Headline:** Want to Practice HTML?
**GFE copy:** HTML interview questions with detailed solutions — from semantic markup to media APIs.
**CTA button text:** greatfrontend.com → HTML Questions
**Visual direction:**
- Layout: Headline centered. GFE logo prominent. CTA text below.
- Key elements: GFE logo, HTML orange accent.
- Style notes: Clean, minimal. Consistent dark bg.

**Target:** 7 slides (Hook + 4 APIs + gotchas + CTA). Within the ideal 7-10 range.


# ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
# SOURCES
# ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

## Sources
- getUserMedia API — https://developer.mozilla.org/en-US/docs/Web/API/MediaDevices/getUserMedia
- MediaRecorder API — https://developer.mozilla.org/en-US/docs/Web/API/MediaRecorder
- getDisplayMedia (Screen Capture) — https://developer.mozilla.org/en-US/docs/Web/API/MediaDevices/getDisplayMedia
- Picture-in-Picture API — https://developer.mozilla.org/en-US/docs/Web/API/Picture-in-Picture_API
- MediaStream API — https://developer.mozilla.org/en-US/docs/Web/API/MediaStream
- HTTPS requirement for secure contexts — https://developer.mozilla.org/en-US/docs/Web/Security/Secure_Contexts
- GFE HTML interview questions — https://www.greatfrontend.com/questions/html-interview-questions

**Planned first comment:** "The combo most devs don't realize: getUserMedia + MediaRecorder + a download link = a complete screen recorder in ~15 lines of pure JS. No libraries, no server. The gotcha that trips everyone up: navigator.mediaDevices is literally undefined on HTTP — not 'returns an error,' undefined. You need HTTPS even for localhost testing (except localhost is special-cased in most browsers). Practice HTML interview questions with detailed solutions: https://www.greatfrontend.com/questions/html-interview-questions?utm_source=linkedin&utm_medium=social&utm_campaign=html5-media_mar+2026. API docs: MDN getUserMedia (mdn.io/getUserMedia), MediaRecorder (mdn.io/MediaRecorder)."
