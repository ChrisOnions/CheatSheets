# CSS

```css
/* ID Of unique-header */
#unique-header {
  text-align: center;
}

/* Class with color red */
.class {
  color: red;
}

/* apply to all Divs and p tags  */
div,
p {
  background-color: blue;
}

/* Solid black border unless specified elsewhere */
* {
  border: 1px solid black;
}
```

# Frequently used elements

```Css
.frequent {
  color: aliceblue;
  background-color: aqua;
  background-image: none;
  display: flex; /* grid or none */
  height: auto;
  width: auto;
  min-width: none;
  max-height: none;
  margin: auto;
  margin-top: auto; /* bottom, left, right */
  padding: 1px;
  border: solid red 1px; /* style color and sixe  */
  border-radius: 5px; /* For rouded corners */
  /* Fonts */
  font: 600;
  font-family: "Lucida Sans", "Lucida Sans Regular", "Lucida Grande",
    "Lucida Sans Unicode", Geneva, Verdana, sans-serif; /* Defines fonts */
  font-style: italic;
  font-weight: 800; /* Thickness of font */
  /* Postion */
  position: absolute;
  position: relative;
  position: sticky;
  /* Priority */
  z-index: 1;
  z-index: 999;
}
```

# Media Querys

BreakPoints

```text
320px — 480px: Mobile devices.
481px — 768px: iPads, Tablets.
769px — 1024px: Small screens, laptops.
1025px — 1200px: Desktops, large screens.
1201px and more — Extra large screens, TV.
```

```Css
@media screen and (min-width: 320px) {
  }
}
@media screen and (min-width: 481px) {
  }
}
@media screen and (min-width: 769px) {
  }
}
@media screen and (min-width: 1025px) {
  }
}
@media screen and (min-width: 1201px) {
  }
}
```

# Psuedo Classes

```css
/* The user's cursor is positioned over the element */
button:hover {
  background-color: #772014;
  color: #fff;
}

/* The user is actively pressing down on the element */
button:active {
  font-size: 180%;
  box-shadow: 0 0 10px #000 inset;
}

/* The element is currently in focus, either by tabbing to or clicking on it */
button:focus {
  outline: none;
  border-color: #8ac4ff;
}
```

```css
/* Added symbols before and after the nav links */
nav li::before,
nav li::after {
  content: "\2766";
  color: #8ac4ff;
  padding: 1%;
  font-family: cursive;
}
```

# Variables

```Css
:root {
  --dark: #13293d;
  --light: #fff;
  --navlink-color: #b9c6ae;
}
```

<!--  -->

### Referance

![img](../Assets/Content.jpg "Title")
