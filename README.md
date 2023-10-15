# 📦 Vue Floating Action Button Component

This project provides a customizable Floating Action Button (FAB) component for Vue applications. The FAB can be customized with different actions and colors, making it a versatile element for any interactive application.

![Vue Logo](https://vuejs.org/images/logo.png)

## 🎁 Features

- Customizable actions: Each action button within the FAB can be tied to a specific function in your Vue application.
- Dynamic colors: The FAB's color can be set programmatically, allowing for a more dynamic user experience.
- Material Design Icons: The component uses Material Design icons.

## 🤔 How to Use

### 👨‍💻 1. Installation

Before you can use the FAB component, you need to ensure that you have Vue installed in your project. You can include it directly in your project using npm or yarn.

```bash
npm install vue@next
# OR
yarn add vue@next
```

### 👨‍🏫 2. Implementing the FAB Component

After installing Vue, you can implement the FAB component in your application. Here's a step-by-step guide on how to use the FAB component in your `App.vue` file.

#### Importing the Component

First, make sure to import the FAB component into your Vue application. You can do this by adding the following line at the top of your script in your `App.vue`:

```javascript
import FabComponent from './components/FabComponent.vue'; // Adjust the import path as needed
```

#### 🙌 Using the Component

Within your template, you can use the FAB component as follows:

```html
<template>
  <div id="app">
    <fab-component 
      :color="fabColor" <!-- takes the color variable or directly declare it here -->
      :fab-actions="actions" <!-- sets the actions declared in script -->
      @click-action="handleAction" <!-- handles the actions on click -->
    />
  </div>
</template>
```

In the script setup section of your `App.vue`, define the color and actions for the FAB:

```javascript
<script setup>
import { ref } from 'vue'
import FabComponent from './fab.vue'

// Define the FAB color
const fabColor = 'brown' // try other color names or hex values colors include (rainbow, red, orange, yellow, green, blue, indigo, violet, brown) or hex for ex: "#f097f5" or don't declare the variable for the default "rainbow" color

// Define FAB actions
const actions = ref([
  { name: 'edit', icon: 'edit', action: () => { console.log("edit clicked") } },
  { name: 'delete', icon: 'delete', action: () => { console.log("delete clicked") } },
  // add more here as for the icons, read the google material design CSS for the icon names !
])

// Handles the actions passes them
const handleAction = (action) => {
  // Find the action by name and call its function
  const selectedAction = actions.value.find(act => act.name === action.name)
  if (selectedAction && selectedAction.action) {
    selectedAction.action()
  }
}
</script>
```

### 👨‍🎨 3. Customization

The FAB component's colors and actions are fully customizable. You can change the color by modifying the `fabColor` value, and you can add or remove actions by updating the `actions` list. Each action requires a name, an icon (referring to the Google Material Design icons), and a function to execute when the action is triggered.

## 🤝 Contributing

Contributions to the component are welcome. Please ensure that you test the component with various scenarios for actions and colors before submitting any changes.

## ✍️ License

This Vue FAB component is licensed under the MIT license. Feel free to use it or modify in your projects as needed.
