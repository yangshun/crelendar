Post Caption
🚨 Most JS devs misunderstand Hoisting, here’s what’s really going on.
What is Hoisting?
Hoisting is JavaScript’s default behavior of moving declarations to the top of the current scope (global or function). But only declarations, not initializations.
What gets hoisted?
 ✔ var declarations
 ✔ function declarations
 ✘ let, const, class (they are hoisted but stay in temporal dead zone)
 ✘ function expressions and arrow functions (only the variable name is hoisted)

How it works under the hood (example):
console.log(a); // undefined
var a = 5;

JS engine interprets this as:
var a;
console.log(a); // undefined
a = 5;


Key Differences:
Only var and function declarations are hoisted in a way that lets you use them before they're defined.
let, const, and arrow functions are technically hoisted too, but they can’t be used before declaration because they stay in the Temporal Dead Zone (TDZ), accessing them early causes a ReferenceError.



Why it matters for you:
	•	Avoid bugs from undefined values.

	•	Predict how your code runs line-by-line.

	•	Better understand closures and scope behavior.


🔍 Mental model tip:
Declarations are hoisted. Assignments stay in place.

#JavaScript #WebDevelopment #FrontendTips #ByteSizedLearning #JSFundamentals #HoistingExplained #GreatFrontend #LearnJS

Design Brief
🎨 Layout Structure:
	•	Title (Top):
 Bold text: “JavaScript Hoisting: What’s Really Happening?”

Left Side: “What is Hoisting?” Box
 Use a small code snippet + arrow + explanation:

console.log(x);
var x = 10;
 ↓
 Interpreted as:

var x;
console.log(x);
x = 10;

	•	Right Side: Comparison Table
 Compact table:

Keyword
Hoisted?
Usable Before?
Initializes?
var
✅
✅
❌
let
✅
❌ (TDZ)
❌
const
✅
❌ (TDZ)
❌
function
✅
✅
✅
arrow fn
partial
❌
❌
	•	
Use green ticks/red crosses or ✅❌ for visual clarity.

	•	Bottom Box: “Why it matters”
 Bullet points with icons:

	•	✅ Predict execution order

	•	🐛 Avoid bugs from TDZ

	•	🧠 Improve understanding of closures
