# BitSwiper Component Reference

This document serves as a complete reference for the **BitSwiper** component—a touch-enabled slider (or “Swiper”) designed to present items in a swiping row. The reference includes an overview, usage examples, API parameters, and feedback guidelines. It is intended to be used by an AI agent or developer for understanding, integrating, and customizing the component.

---

## Overview

**BitSwiper** (also known as *TouchSlider*) lets users navigate through a series of items by swiping. It is built with flexibility in mind, offering various configurations such as:
- **Basic sliding**
- **Scrolling multiple items at once**
- **Hiding navigation buttons**
- **RTL (Right-to-Left) support** for languages like Arabic

---

## Usage Examples

### Basic Example

The most basic configuration displays a row of items that can be swiped horizontally.

```html
<div class="bit-swp">
  <!-- Each item is wrapped in a container with the class 'bit-swpi item' -->
  <div class="bit-swpi item">
    <div class="number">Item 1</div>
    <img class="image" src="path/to/image1.jpg" alt="Image 1">
  </div>
  <!-- Add additional items as needed -->
</div>
```

### ScrollItemsCount

Adjust the number of items that scroll with each navigation event by setting the `ScrollItemsCount` property:

```razor
<BitSwiper ScrollItemsCount="3">
  <!-- Items go here -->
</BitSwiper>
```

### HideNextPrev

If you want to hide the navigation buttons (Next/Prev), set the `HideNextPrev` parameter to true:

```razor
<BitSwiper HideNextPrev="true">
  <!-- Items go here -->
</BitSwiper>
```

### RTL (Right-to-Left)

For languages written from right to left, use the RTL configuration by adding the `bit-rtl` class and setting the direction attribute:

```html
<div class="bit-swp bit-rtl" dir="rtl">
  <!-- Items go here -->
</div>
```

---

## API Reference

### BitSwiper Component Parameters

| Name              | Type            | Default Value | Description                                                                          |
| ----------------- | --------------- | ------------- | ------------------------------------------------------------------------------------ |
| AnimationDuration | double          | 0.5           | Duration of the scrolling animation in seconds.                                    |
| ChildContent      | RenderFragment? | null          | The content (items) of the swiper.                                                   |
| HideNextPrev      | bool            | false         | Determines whether the Next/Prev buttons are hidden.                               |
| ScrollItemsCount  | int             | 1             | Number of items that are scrolled on each navigation event.                         |

### BitComponentBase Parameters

| Name           | Type                        | Default Value                         | Description                                                                                 |
| -------------- | --------------------------- | ------------------------------------- | ------------------------------------------------------------------------------------------- |
| AriaLabel      | string?                     | null                                  | Aria-label for accessibility, beneficial for screen readers.                              |
| Class          | string?                     | null                                  | Custom CSS class for the root element of the component.                                     |
| Dir            | BitDir?                     | null                                  | Determines the reading direction (LTR or RTL).                                              |
| HtmlAttributes | Dictionary&lt;string, object&gt; | new Dictionary&lt;string, object&gt;() | Additional HTML attributes for the component.                                               |
| Id             | string?                     | null                                  | Custom id attribute; if null, a unique identifier is auto-assigned.                         |
| IsEnabled      | bool                        | true                                  | Indicates whether the component is enabled.                                                 |
| Style          | string?                     | null                                  | Custom CSS styles for the component’s root element.                                         |
| Visibility     | BitVisibility               | BitVisibility.Visible                 | Controls whether the component is visible, hidden, or collapsed.                            |

### Public Members of BitComponentBase

| Name       | Type              | Default Value   | Description                                                                                           |
| ---------- | ----------------- | --------------- | ----------------------------------------------------------------------------------------------------- |
| UniqueId   | Guid              | Guid.NewGuid()  | Read-only unique identifier assigned at component construction.                                    |
| RootElement| ElementReference  | N/A             | Reference to the root HTML element of the component.                                                |

---

## Enums

### BitVisibility

| Name      | Value | Description                                                                          |
| --------- | ----- | ------------------------------------------------------------------------------------ |
| Visible   | 0     | The component’s content is visible.                                                  |
| Hidden    | 1     | The component is hidden, but the space remains (using `visibility: hidden`).         |
| Collapsed | 2     | The component is hidden and removed from the layout (using `display: none`).         |

### BitDir

| Name | Value | Description                                                                                                              |
| ---- | ----- | ------------------------------------------------------------------------------------------------------------------------ |
| Ltr  | 0     | Left-to-right direction, suitable for languages such as English.                                                       |
| Rtl  | 1     | Right-to-left direction, used for languages such as Arabic.                                                            |
| Auto | 2     | Automatically determines direction based on the content's character directionality.                                    |

---