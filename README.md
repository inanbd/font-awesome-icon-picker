# Font Awesome Icon Picker

An emoji-keyboard-style icon picker built with Font Awesome 6. Drop the HTML file into your site or copy the markup into an existing page — no build step, no dependencies beyond a single CDN link.

## Features

- Trigger button that opens a popup picker, just like an emoji keyboard
- 8 categories: Smileys, People, Nature, Food, Travel, Objects, Symbols, Sports
- Live search across all categories
- Click outside the picker to close it
- Selected icon is reflected back on the trigger button
- Pure HTML, CSS, and vanilla JavaScript — no frameworks

## Quick Start

1. Open `icon-menu.html` directly in a browser, or
2. Copy the contents into a page on your site.

The only external dependency is Font Awesome, loaded from a CDN in the `<head>`:

```html
<link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.5.1/css/all.min.css">
```

If you already load Font Awesome elsewhere on your site, you can remove that line.

## How It Works

The icons are stored in a single `iconData` object near the top of the `<script>` block. Each category has a label, a `tabIcon` (the icon shown on its category tab), and an array of icon class names:

```js
const iconData = {
  smileys: {
    label: "Smileys",
    tabIcon: "fa-face-smile",
    icons: ["fa-face-smile", "fa-face-laugh", "fa-face-grin", ...]
  },
  // ...
};
```

When the user clicks an icon, the trigger button updates to show that icon and its name.

## Customizing

### Add or remove icons in a category

Edit the `icons` array for the relevant category. Use any solid-style Font Awesome 6 class name without the `fa-solid` prefix:

```js
nature: {
  label: "Nature",
  tabIcon: "fa-leaf",
  icons: ["fa-leaf", "fa-tree", "fa-seedling", "fa-cactus"]  // added cactus
}
```

You can browse the full set at [fontawesome.com/icons](https://fontawesome.com/icons) and filter to "Free" if you're using the free CDN build.

### Add a new category

Add a new key to `iconData`:

```js
animals: {
  label: "Animals",
  tabIcon: "fa-paw",
  icons: ["fa-paw", "fa-dog", "fa-cat", "fa-fish", "fa-dove", "fa-horse"]
}
```

The category tab is generated automatically.

### Change the grid size

The grid is set to 8 columns. Edit this in the CSS:

```css
.icon-grid {
  grid-template-columns: repeat(8, 1fr);  /* change 8 to whatever you want */
}
```

### Change the accent color

The accent color (`#4a6cf7`) appears in the trigger icon, hover states, active tab underline, and selected cell background. Find and replace it in the CSS, or extract it to a CSS custom property if you'd like to theme it.

### Hook the selection up to your own code

Inside `renderIcons()`, the click handler sets the trigger's icon and label. Add your own logic there:

```js
cell.onclick = () => {
  selectedIcon.className = `fa-solid ${iconClass}`;
  selectedLabel.textContent = iconClass.replace("fa-", "").replace(/-/g, " ");
  picker.classList.remove("open");

  // your code here — for example:
  document.dispatchEvent(new CustomEvent("icon-picked", { detail: iconClass }));
};
```

## Pro Icons

The default CDN serves the free Font Awesome set. If you have a Font Awesome Pro subscription, replace the `<link>` tag with your Pro kit URL and you can reference Pro-only icons in the `iconData` arrays.

## Browser Support

Works in any modern browser. The picker uses `aspect-ratio`, `grid`, and standard ES6+ JavaScript. No polyfills needed for evergreen browsers.

## File Structure

A single self-contained file:

```
icon-menu.html    # markup, styles, and script all in one
```

## License

The picker code itself is yours to use however you like. Font Awesome icons are subject to the [Font Awesome Free license](https://fontawesome.com/license/free) (CC BY 4.0 for icons, MIT for the toolchain).
