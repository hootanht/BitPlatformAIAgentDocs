# Layout Component Documentation

The **Layout** component provides a base UI structure for your application. It allows you to define a consistent framework that includes a header, main content area, footer, and optionally a navigation panel. This documentation serves as a comprehensive reference, outlining usage examples, API parameters, inherited properties, and customization options.

---

## Overview

The **Layout** component is designed to:
- Create a base structure for UI applications.
- Organize content into defined sections: **Header**, **Main**, **Footer**, and optionally a **NavPanel**.
- Support customization via CSS classes and styles.
- Enable features like sticky header/footer positioning and reversible navigation panels.

---

## Usage Examples

### Basic Layout

This example demonstrates a simple layout with a header, main content area, and footer.

```html
<div class="container">
  <div class="bit-lyt">
    <header class="bit-lyt-hdr">
      <div class="header">Header</div>
    </header>
    <main class="bit-lyt-man">
      <div class="bit-lyt-mcn">
        <div class="main">Main</div>
      </div>
    </main>
    <footer class="bit-lyt-ftr">
      <div class="footer">Footer</div>
    </footer>
  </div>
</div>
```

### Layout with NavPanel

This example shows how to incorporate a navigation panel into your layout. A toggle button is provided to hide or show the NavPanel.

```html
<!-- Toggle button to hide/show NavPanel -->
<div class="bit-tgl">
  <label for="BitToggle-nav-button" class="bit-tgl-lbl">Hide NavPanel</label>
  <div class="bit-tgl-cnt">
    <button role="switch" type="button" id="BitToggle-nav-button" class="bit-tgl-btn" data-ktp-target="true" aria-checked="false">
      <span class="bit-tgl-sta"></span>
    </button>
  </div>
  <input type="checkbox" class="bit-input-hidden" value="false">
</div>

<!-- Layout with NavPanel included -->
<div class="container">
  <div class="bit-lyt">
    <header class="bit-lyt-hdr">
      <div class="header">Header</div>
    </header>
    <main class="bit-lyt-man">
      <div class="bit-lyt-nmn">
        <div class="nav-menu">NavPanel</div>
      </div>
      <div class="bit-lyt-mcn" style="width:calc(100% - 0px);">
        <div class="main">Main</div>
      </div>
    </main>
    <footer class="bit-lyt-ftr">
      <div class="footer">Footer</div>
    </footer>
  </div>
</div>
```

### Custom Styles & Classes

Customize your layout by applying custom CSS classes and styles to specific sections.

```html
<div class="container">
  <div class="bit-lyt">
    <header class="bit-lyt-hdr header2">Header</header>
    <main class="bit-lyt-man main2" style="height: 19rem;">
      <div class="bit-lyt-nmn nav-menu2">NavPanel</div>
      <div class="bit-lyt-mcn main-content2" style="width:calc(100% - 0px);">Main</div>
    </main>
    <footer class="bit-lyt-ftr footer2">Footer</footer>
  </div>
</div>
```

---

## API Reference

### BitLayout Parameters

| Name              | Type                         | Default Value | Description                                                             |
|-------------------|------------------------------|---------------|-------------------------------------------------------------------------|
| **Classes**       | `BitLayoutClassStyles?`       | `null`        | Custom CSS classes for different parts of the Layout.                   |
| **Footer**        | `RenderFragment?`             | `null`        | The content of the footer section.                                      |
| **Header**        | `RenderFragment?`             | `null`        | The content of the header section.                                      |
| **HideNavPanel**  | `bool`                       | `false`       | Hides the NavPanel content when set to true.                            |
| **Main**          | `RenderFragment?`             | `null`        | The content of the main section.                                        |
| **NavPanel**      | `RenderFragment?`             | `null`        | The content of the nav panel section.                                   |
| **NavPanelWidth** | `int`                        | `0`           | The width of the nav panel section in pixels.                           |
| **ReverseNavPanel**| `bool`                      | `false`       | Reverses the position of the nav panel inside the main container.         |
| **Styles**        | `BitLayoutClassStyles?`       | `null`        | Custom CSS styles for different parts of the Layout.                    |
| **StickyFooter**  | `bool`                       | `false`       | Enables sticky positioning of the footer at the bottom of the viewport.   |
| **StickyHeader**  | `bool`                       | `false`       | Enables sticky positioning of the header at the top of the viewport.      |

### Inherited from BitComponentBase

The Layout component inherits these properties from `BitComponentBase`:

| Name             | Type                         | Default Value                           | Description                                                                      |
|------------------|------------------------------|-----------------------------------------|----------------------------------------------------------------------------------|
| **AriaLabel**    | `string?`                    | `null`                                  | The aria-label for the component, enhancing accessibility.                     |
| **Class**        | `string?`                    | `null`                                  | Custom CSS class for the root element.                                           |
| **Dir**          | `BitDir?`                    | `null`                                  | Determines the text direction (e.g., left-to-right or right-to-left).            |
| **HtmlAttributes** | `Dictionary<string, object>` | `new Dictionary<string, object>()`     | Additional HTML attributes to apply to the root element.                       |
| **Id**           | `string?`                    | `null`                                  | Custom id for the root element; if `null`, a unique id is generated automatically.|
| **IsEnabled**    | `bool`                       | `true`                                  | Indicates whether the component is enabled.                                    |
| **Style**        | `string?`                    | `null`                                  | Custom CSS styles for the root element.                                          |
| **Visibility**   | `BitVisibility`              | `BitVisibility.Visible`                 | Controls whether the component is visible, hidden, or collapsed.               |

### Public Members from BitComponentBase

| Name         | Type             | Default Value    | Description                                                              |
|--------------|------------------|------------------|--------------------------------------------------------------------------|
| **UniqueId** | `Guid`           | `Guid.NewGuid()` | Read-only unique identifier for the root element, generated on creation. |
| **RootElement** | `ElementReference` | -          | Reference to the root DOM element of the component.                      |

### BitLayoutClassStyles Properties

These properties enable custom styling for specific layout sections:

| Name          | Type      | Default Value | Description                                                     |
|---------------|-----------|---------------|-----------------------------------------------------------------|
| **Root**      | `string?` | `null`        | Custom CSS classes/styles for the root element of the Layout.   |
| **Header**    | `string?` | `null`        | Custom CSS classes/styles for the header section.               |
| **Main**      | `string?` | `null`        | Custom CSS classes/styles for the main section.                 |
| **NavPanel**  | `string?` | `null`        | Custom CSS classes/styles for the nav-menu section.             |
| **MainContent** | `string?` | `null`      | Custom CSS classes/styles for the main-content section.         |
| **Footer**    | `string?` | `null`        | Custom CSS classes/styles for the footer section.               |

---

## Enumerations

### BitVisibility Enum

Defines the visibility states for a component.

| Name      | Value | Description                                                                               |
|-----------|-------|-------------------------------------------------------------------------------------------|
| **Visible**   | `0`   | The component is fully visible.                                                         |
| **Hidden**    | `1`   | The component is hidden, but its space remains (using `visibility:hidden`).              |
| **Collapsed** | `2`   | The component is hidden and does not occupy any space (using `display:none`).             |

### BitDir Enum

Specifies the text direction.

| Name   | Value | Description                                                                                                            |
|--------|-------|------------------------------------------------------------------------------------------------------------------------|
| **Ltr**| `0`   | Left-to-right. Use for languages written from left to right (e.g., English).                                          |
| **Rtl**| `1`   | Right-to-left. Use for languages written from right to left (e.g., Arabic).                                           |
| **Auto**| `2`  | Automatically determines text direction based on the content’s character analysis.                                   |

---