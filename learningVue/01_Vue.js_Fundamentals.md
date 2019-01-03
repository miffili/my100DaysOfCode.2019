## Vue.js Fundamentals

www.vueschool.io | 10 lessons | 26 minutes

### Getting started

- including Vue.js possible via CDN
- initialize new vue instance via `var shoppingList = new Vue({});`
- object takes properties for this instance
	```javascript
	var shoppingList = new Vue({
		el: '#shopping-list',
		data: {
			header: 'Vue.js is awesome'
		},
	});
	```
- templating syntax using `{{ ... }}`
	- **!** takes only _ONE expression_
	- variables / data
	``` html
	<div id="shopping-list">
		<h1>{{ header }}</h1>
	</div>
	```
	- turnary operators for simple if-statements
	``` html
	<div id="shopping-list">
		<h1>{{ header ? header : 'Hello Vue.js!' }}</h1>
	</div>
	```

- binding data to input-field via `v-model` directive (2-way) ➡ instant reactivity
	```html
	<div id="shopping-list">
		<h1>{{ header ? header : 'Hello Vue.js!' }}</h1>
		<input type="text" v-model="header">
	</div>
	```
	
### Loops

- via directive `v-for`, which is also reactive
- add data to loop over
	```javascript
	var shoppingList = new Vue({
		el: '#shopping-list',
		data: {
			header: 'Vue.js is awesome',
			items: [
				'10 party hats',
				'2 board games',
				'20 cups'
			]
		},
	});
	```
- loop over `data.items`
	```html
	<ul>
		<li v-for="item in items">{{ item }}</li>
	</ul>
	```
	
### user inputs
	
- add newItem to vue instance
	```javascript
	var shoppingList = new Vue({
		el: '#shopping-list',
		data: {
			header: 'Vue.js is awesome',
			newItems: '',
			items: [
				'10 party hats',
				'2 board games',
				'20 cups'
			]
		},
	});
	```
- bind newItem to input field via `v-model` directive
	```html
	<input
		type="text"
		placeholder="Add new item"
		v-model="newItem">
	```
	
### user events
	
- add event listener to html tags via `v-on` directive
	```html
	<div class="add-item-form">
		<input
			type="text"
			placeholder="Add new item"
			v-model="newItem"
			v-on:keyup.enter="items.push(newItem)">
		<button v-on:click="items.push(newItem)">Save</button>
	</div>
	```
	
### methods
	
- used to alter instance data
- add event method to vue instance
	```javascript
	var shoppingList = new Vue({
		// ...
		methods: {
			saveItem: function( ) {
				this.items.push(this.newItem);
				this.newItem = '';
			}
		},
	});
	```
- add method to template
	```html
		<input
			type="text"
			placeholder="Add new item"
			v-model="newItem"
			v-on:keyup.enter="saveItem">
			<button v-on:click="saveItem">Save</button>
	```

### conditional rendering

- using directive `v-if` & `v-else` (always preceded by a `v-if`!) to conditional render elements
	```html
	<div class="add-item-form" v-if="state === 'edit'">
		<input
			type="text"
			placeholder="Add new item"
			v-model="newItem"
			v-on:keyup.enter="items.push(newItem)">
			<button v-on:click="items.push(newItem)">Save</button>
		</div>
	```
	```javascript
	var shoppingList = new Vue({
		// ...
		data: {
			state: 'default',
			// ...
		}
		// ...
	});
	```

### attribute bindings

- using the `v-bind` directive it's possible to bind data to any html attribute
	```html
	<a v-bind:href="newItem" target="_blank">Dynamic Link</a>
	```

### shorthand directives

- `@` for `v-on:`
- `:` for `v-bind:`
	```html
	<button v-on:click="items.push(newItem)" v-bind:disabled>Save</button>

	<button @click="items.push(newItem)" :disabled>Save</button>
	```

### dynamic classes

- common need & use case for attribute bindings
	```html
	<ul>
		<li v-for="item in items" :style="{strikeout: item.purchased}">{item.label}</li>
	</ul>
	```
	```javascript
	var shoppingList = new Vue({
		// ...
		data: {
		  // ...
			items: [
				{
					label: '10 party hats',
					purchased: false,
				},
				{
					label: '2 board games',
					purchased: true,
				},
				{
					label: '20 cups',
					purchased: false,
				},
			]
		}
		// ...
	});
	```
- possible to use different syntax'
	- object
	```html
	<li :class="{ strikethrough: item.purchased, ... }"> items.label </li>
	```
	- array
	```html
	<li :class="[ item.purchased ? 'strikethrough' : '', ... ]"> items.label </li>
	```
- for static classes
	- simple `class` attribute
	```html
	<li :class="[ item.purchased ? 'strikethrough' : '', ... ]" class="priority"> items.label </li>
	```
	- include in array
	```html
	<li :class="[ item.purchased ? 'strikethrough' : '', 'priority', ... ]"> items.label </li>
	```
	
### computed properties

- for transformations or calculations of instance data for presentation layer
- _never_ alter data in computed properties
- computed properties need to return a value
```html
<ul>
	<li v-for="item in reversedItems" :style="{strikeout: item.purchased}">{item.label}</li>
</ul>
```
```javascript
var shoppingList = new Vue({
	// ...
	computed: {
		reversedItems: function() {
			return this.items.slice(0).reverse();
		}
	},
	methods: {
		//...
	}
});
```
**!** when you need to change data **use methods**, when you need to change the presentation of existing data use **computed properties**

---

see full sample project: [vue-projects/01_to-do-list](https://github.com/Miffili/vue-projects#01-to-do-list) | [live demo](https://www.klarafleischmann.de/vue-projects/01_to-do-list/) | [code](https://github.com/Miffili/vue-projects/tree/master/01_to-do-list)
