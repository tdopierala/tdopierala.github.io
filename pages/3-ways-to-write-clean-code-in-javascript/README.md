## 3+ Ways to Write Clean Code in JavaScript

Coding is an art, so why not make it as clean as possible? In this tutorial, I go over 3 techniques I like to implement to help make my JavaScript code easier to read and extend upon.

#### 01-avoid-else-statements.js

```javascript
function getThemeColors() {
	let currentHour = new Date().getHours();
	let textColor;
	let backgroundColor;

	if (currentHour > 20 && currentHour < 7) {
		textColor = "#ffffff";
		backgroundColor = "#222222";
	} else {
		textColor = "#222222";
		backgroundColor = "#ffffff";
	}

	return {
		textColor: textColor,
		backgroundColor: backgroundColor
	};
}
```

#### 02-skip-loop-iterations.js

```javascript
const numbers = [4, 9, 2, 7, 11];

// Find factors of 12
for (const n of numbers) {
	if (12 % n === 0) {
		console.log(`${n} is a factor of 12!`);
	}
}
```

#### 03-array-map-for-transformations.js

```javascript
const names = ["dom", "peter", "aleisha", "sam"];
const capitalized = [];

for (const n of names) {
	const newName = n[0].toUpperCase() + n.slice(1);

	capitalized.push(newName);
}
```
