# Tailwind CSS

## Typography

Tailwind Preflieght will define default rules, kind of normalizing. We want to overwrite some of these rules, e.g. headlines are set to:

```css
h1, h2, h3, h4, h5 {
  font-size: initial;
  line-height: initial;
}
```
These rules can be overridden in your `app.css` as follows:

```css
@tailwind base;

@layer base {
    h1, .h1,
    h2, .h2,
    h3, .h3,
    h4, .h4 {
        font-family: 'Poppins', sans-serif;
        @apply font-semibold text-blue-dark;
    }
    
    h1, .h1 {
        @apply text-xl;
    }
    
    h2, .h2 {
        @apply text-lg;
    }
}
```

