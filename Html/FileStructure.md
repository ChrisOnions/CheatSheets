# HTML Structure

- Use ! in VScode to add Basic Syntax

```HTML

<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta http-equiv="X-UA-Compatible" content="IE=edge">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Document</title>
</head>
<body>

</body>
</html>
```

# Tags

Tags for Size

[Tag Docs](https://www.w3schools.com/tags/ref_byfunc.asp)

```HTML
<!--  -->
<h1></h1>
  to
<h6></h6>
<!-- Paragraph -->
<p></p>
<!-- Line Break -->
<br />
<!-- Divider -->
<div></div>
<!-- Section -->
<section></section>
<!-- Article -->
<article></article>
<!-- Anchor Tag W/href -->
<a href=""></a>
<!-- Buttons -->
<button></button>
<button type="submit"></button>
<!-- Form Exapmle -->

<form action="" method="get">
  <label for="fname">First name:</label>
  <input type="text" id="fname" name="fname" /><br /><br />
  <label for="lname">Last name:</label>
  <input type="text" id="lname" name="lname" /><br /><br />
  <input type="submit" value="Submit" />
</form>
<!-- Image -->
<img src="" alt="404 Not Found" />
<!-- Links -->
<link rel="stylesheet" href="style.css" />
<link rel="import" href="component.html" />
<!-- List -->
<ul>
  <li></li>
  <li></li>
  <li></li>
</ul>
<ol>
  <li></li>
  <li></li>
  <li></li>
</ol>
<!-- Script -->
<script src=""></script>
```

Typical Encaptulation

```HTML
<!-- Paragraphs and Buttons can be wrapped up in Sections and Divs -->
<section class="upper-level-section">
      <div class="div-Wrapper">
        <h1 class="Header-class another-class">
          <p class="paragrraph-class">Text here</p>
          <button type="submit">Button Text</button>
        </h1>
      </div>
    </section>

```

<section class="upper-level-section">
      <div class="div-Wrapper">
        <h1 class="Header-class another-class">
          <p class="paragrraph-class">Text here</p>
          <!-- <button type="submit">Button Text</button> -->
        </h1>
      </div>
    </section>

# Attributes

- <\*> --- Catch all
  - Everywhere it can see
- <\#> --- Id
  - id="Totally-Unique-Attribute"
- <\.> --- Class
  - class="Used-On-Multiple"
- Body --- Direct
  - All tags of that name

# Span

The <\span> tag is an inline container used to mark up a part of a text, or a part of a document.

```HTML
<!-- Span -->

<span></span>
<button type="submit"><span>Not</span> Button Text</button>
```

<button type="submit"><span>Not</span> Button Text</button>

<!--  -->
