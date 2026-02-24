Content Brief
Chrome 135 introduces a fully customizable <select> — without sacrificing accessibility
Native HTML just got a serious glow-up. Chrome 135 now lets you fully customize the <select> element using standard CSS — no JavaScript rewrites, no third-party libraries. It keeps everything you’d expect: keyboard support, screen reader accessibility, built-in behavior.
Traditionally, developers had to rebuild dropdowns from scratch or reach for Select2 or React Select — just to get design control. That’s no longer necessary.
Here’s what’s new:
	•	Use the CSS property appearance: base-select to unlock styling control of <select>

	•	Use the Popover API to build the dropdown content

	•	You can position the dropdown precisely using modern CSS, like the anchor() function

	•	Enjoy native focus and accessibility without extra effort

Why this matters:
	•	No more juggling ARIA roles

	•	No more polyfills. If unsupported on other browsers or old Chrome versions, it degrades successfully and just renders the default <select>

	•	Full design freedom with minimal code

	•	Built-in performance and accessibility wins

Take note that this is supported in Chrome 135+ with built-in progressive enhancement — other browsers gracefully fall back to the classic `<select>` rendering. 
🔍 Have you explored the new customizable <select> yet? You can read all about it here! Does this feel like a drop-in replacement for your current React or JS-based dropdowns — or are cross-browser concerns still a blocker for you?
<tags>
#FrontendDevelopment #Chrome135 #Accessibility #GreatFrontEnd #WebDev 

Design Brief
Option A
@graphic designer, can we include snippets from the following video which shows the customizable <select> element in action>? If we could perhaps include the first 5-10 seconds as a gif? 
https://developer.chrome.com/static/blog/a-customizable-select/select-explorations.mp4



If we can’t do that, I think a good design could look like this:
Option B
2 page carousel
Page 1

Title: Chrome 135: The <select> element can now be customized with CSS 
Images:
Borrow any 5 cool looking frames from the video above. This way, we kind of introduce the user to the potential of customizable select elements using examples from the Google blog itself. 



Page 2:


Something similar to this but with this information:

Title: Chrome 135: The <select> element can now be customized with CSS 
1. 
Headline:
 Style <select> with just CSS (Chrome 135)
Subtext:
 Use appearance: base-select to fully control dropdown styles — no more default browser look.
Icon Idea:
 CSS paintbrush + form field combo
2.
Headline:
 Keeps native accessibility + keyboard support
Subtext:
 Enjoy keyboard nav, focus handling, and screen reader support — no extra JS or ARIA required.
Icon Idea:
 Keyboard + accessibility icon
3. 
Headline:
 No polyfills. No breakage.
Subtext:
 If unsupported, the browser just falls back to a classic <select>. Clean, progressive enhancement.
Icon Idea:
 Fallback icon (like a browser icon switching to default view) or checkmark beside older browser
