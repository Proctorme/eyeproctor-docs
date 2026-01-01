# Installation

Eye By Proctorme is delivered as a lightweight browser-based widget.  
Installation requires **adding a single script tag** to your application.

```html
<script src="https://widget.proctorme.com/proctormewidget-widget-init.js"></script>
```

## Where to place the script

The script should be added:
- Inside the `<head>` tag or
- Just before the closing `</body>` tag

For most applications, placing it before </body> is recommended to avoid blocking page rendering.

**Example (recommended)**

```html hl_lines="8"
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
  </head>
  <body>
    <!-- Your application markup -->
    <script src="https://widget.proctorme.com/proctormewidget-widget-init.js"></script>     
  </body>
</html>
```

### How the Widget Loads

- The widget loads asynchronously
- It does not block your application
- Once loaded, it exposes a global function `LoadProctormeWidget()`.

This function returns a Promise that resolves to the Proctorme widget instance.


[Quick start →](quick-start.md){ .md-button }