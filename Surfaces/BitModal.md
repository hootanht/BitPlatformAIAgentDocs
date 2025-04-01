# BitModal Component Reference

This document serves as a complete reference for the **BitModal** component from bit BlazorUI. A Modal is a temporary pop-up that takes focus from your main content and requires user interaction. It is ideal for hosting lengthy content (such as privacy statements or license agreements) or for prompting users to perform complex actions (such as adjusting settings).

---

## Overview

**BitModal** provides a flexible and customizable modal dialog that can be configured for various scenarios:
- **Basic Usage:** Open a simple modal with default settings.
- **Custom Content:** Host any custom HTML or components within the modal.
- **Advanced Options:** Control behaviors like blocking, auto toggle of scroll, and modeless display.
- **Absolute & Relative Positioning:** Customize where the modal appears on the screen.
- **Draggable Modals:** Allow users to reposition the modal.
- **FullScreen Options:** Expand the modal to full height, full width, or both.
- **Event Handling:** Listen to events like dismiss, overlay click, and more.
- **Styling & RTL Support:** Apply custom styles, classes, and support right-to-left layouts.

---

## Usage Examples

### 1. Basic Modal

A simple modal that opens when a button is clicked.

```razor
<!-- Button to trigger the modal -->
<button class="bit-btn bit-btn-fil bit-btn-pri bit-btn-md" type="button">
  <div class="bit-btn-tcn">
    <div class="bit-btn-prt">Open Modal</div>
  </div>
</button>

<!-- BitModal component definition -->
<BitModal IsOpen="true">
  <div class="modal-content">
    <h4>bit BlazorUI</h4>
    <p>bit BlazorUI components are native, easy-to-customize, and...</p>
    <a href="https://blazorui.bitplatform.dev" target="_blank">Learn more</a>
  </div>
</BitModal>
```

*This example shows a basic modal that appears when triggered.*

---

### 2. Customizing Content

Customize the modal content by changing the inner markup.

```razor
<BitModal IsOpen="true">
  <div class="custom-modal-content">
    <h4>Customized Modal</h4>
    <p>This modal contains custom HTML and can host any complex content.</p>
    <a href="https://blazorui.bitplatform.dev" target="_blank">Discover more</a>
  </div>
</BitModal>
```

*Here you can insert any HTML or Blazor components as the modal's content.*

---

### 3. Advanced Options

BitModal offers advanced behaviors such as blocking, auto toggling scroll, and modeless modes.

```razor
<!-- Blocking Modal: prevents dismissal by clicking the overlay -->
<button class="bit-btn bit-btn-fil bit-btn-pri bit-btn-md" type="button">
  <div class="bit-btn-tcn">
    <div class="bit-btn-prt">Open Modal (Blocking)</div>
  </div>
</button>

<BitModal IsOpen="true" Blocking="true">
  <!-- Modal content goes here -->
</BitModal>

<!-- Modal with AutoToggleScroll: automatically toggles scroll behavior -->
<button class="bit-btn bit-btn-fil bit-btn-pri bit-btn-md" type="button">
  <div class="bit-btn-tcn">
    <div class="bit-btn-prt">Open Modal (AutoToggleScroll)</div>
  </div>
</button>

<BitModal IsOpen="true" AutoToggleScroll="true">
  <!-- Modal content goes here -->
</BitModal>

<!-- Modeless Modal: does not dismiss when clicking outside -->
<button class="bit-btn bit-btn-fil bit-btn-pri bit-btn-md" type="button">
  <div class="bit-btn-tcn">
    <div class="bit-btn-prt">Open Modal (Modeless)</div>
  </div>
</button>

<BitModal IsOpen="true" Modeless="true">
  <!-- Modal content goes here -->
</BitModal>
```

*These examples illustrate how to enable advanced modal behaviors.*

---

### 4. Absolute Positioning

Set the modal’s position absolutely on the screen.

```razor
<button class="bit-btn bit-btn-fil bit-btn-pri bit-btn-md" type="button">
  <div class="bit-btn-tcn">
    <div class="bit-btn-prt">Open Modal (AbsolutePosition)</div>
  </div>
</button>

<BitModal IsOpen="true" AbsolutePosition="true">
  <!-- Modal content with absolute positioning -->
</BitModal>
```

*This mode allows the modal to be positioned relative to the document instead of the viewport.*

---

### 5. Position Options

Customize where the modal appears using the Position parameter. A radio group is often used to select among options such as Top Left, Center, Bottom Right, etc.

```razor
<!-- Example radio group for selecting modal position -->
<div role="radiogroup">
  <button class="position-button" type="button">Top Left</button>
  <button class="position-button" type="button">Top Center</button>
  <button class="position-button" type="button">Top Right</button>
  <button class="position-button" type="button">Center Left</button>
  <button class="position-button" type="button">Center</button>
  <button class="position-button" type="button">Center Right</button>
  <button class="position-button" type="button">Bottom Left</button>
  <button class="position-button" type="button">Bottom Center</button>
  <button class="position-button" type="button">Bottom Right</button>
</div>

<BitModal IsOpen="true" Position="BitPosition.Center">
  <!-- Modal content positioned in the center -->
</BitModal>
```

---

### 6. Draggable Modal

Enable the modal to be dragged around by setting the Draggable parameter. You can also specify a custom drag element using the DragElementSelector property.

```razor
<button class="bit-btn bit-btn-fil bit-btn-pri bit-btn-md" type="button">
  <div class="bit-btn-tcn">
    <div class="bit-btn-prt">Open Modal (Draggable)</div>
  </div>
</button>

<BitModal IsOpen="true" Draggable="true" DragElementSelector=".custom-drag-handle">
  <!-- Modal content goes here -->
  <div class="custom-drag-handle">Drag me!</div>
  <div>
    <p>Content inside a draggable modal.</p>
  </div>
</BitModal>
```

*This allows users to reposition the modal as needed.*

---

### 7. FullSize Modal

Make the modal occupy the full screen using the FullSize, FullWidth, or FullHeight properties.

```razor
<button class="bit-btn bit-btn-fil bit-btn-pri bit-btn-md" type="button">
  <div class="bit-btn-tcn">
    <div class="bit-btn-prt">Open FullSize Modal</div>
  </div>
</button>

<BitModal IsOpen="true" FullSize="true">
  <!-- Full-screen modal content -->
</BitModal>
```

*Alternatively, set `FullWidth` or `FullHeight` to control one dimension only.*

---

### 8. Modal Events

Monitor modal events like OnDismiss and OnOverlayClick.

```razor
<BitModal IsOpen="true" OnDismiss="@HandleDismiss" OnOverlayClick="@HandleOverlayClick">
  <!-- Modal content goes here -->
</BitModal>

@code {
  private void HandleDismiss(MouseEventArgs args)
  {
      // Code to run when modal is dismissed
  }

  private void HandleOverlayClick(MouseEventArgs args)
  {
      // Code to run when the overlay is clicked
  }
}
```

*These event handlers help manage modal behavior when users interact with the overlay or dismiss the modal.*

---

### 9. Style & Class Customization

Customize the appearance of the modal by using CSS classes and inline styles.

```razor
<button class="bit-btn bit-btn-fil bit-btn-pri bit-btn-md" type="button">
  <div class="bit-btn-tcn">
    <div class="bit-btn-prt">Open Styled Modal</div>
  </div>
</button>

<BitModal IsOpen="true" Class="custom-modal-class" Styles="max-width:800px; background-color: #f0f0f0;">
  <!-- Modal content goes here -->
</BitModal>
```

*This example shows how to override default styles with your custom CSS.*

---

### 10. RTL (Right-to-Left) Modal

Use the RTL mode for languages that read right-to-left.

```razor
<button class="bit-btn bit-rtl bit-btn-fil bit-btn-pri bit-btn-md" type="button" dir="rtl">
  <div class="bit-btn-tcn">
    <div class="bit-btn-prt">باز کردن مُدال</div>
  </div>
</button>

<BitModal IsOpen="true" Class="bit-rtl" Dir="BitDir.Rtl">
  <!-- Modal content in RTL -->
  <h4>عنوان مدال</h4>
  <p>متن مدال به زبان فارسی...</p>
</BitModal>
```

*This example demonstrates how to configure the modal for RTL languages.*

---

## API Reference

### BitModal Component Parameters

| Name                 | Type                                | Default Value | Description                                                                          |
| -------------------- | ----------------------------------- | ------------- | ------------------------------------------------------------------------------------ |
| AutoToggleScroll     | bool                                | false         | Enables auto-toggle behavior for the modal’s scroll.                               |
| AbsolutePosition     | bool                                | false         | If true, the modal uses absolute positioning instead of fixed.                     |
| Blocking             | bool                                | false         | Determines whether clicking outside dismisses the modal (light dismiss).           |
| ChildContent         | RenderFragment?                     | null          | The content of the modal.                                                            |
| Classes              | BitModalClassStyles?                | null          | Custom CSS classes for different parts of the modal.                               |
| DragElementSelector  | string?                             | null          | CSS selector for the element that acts as the drag handle.                          |
| Draggable            | bool                                | false         | Allows the modal to be dragged around the screen.                                  |
| FullHeight           | bool                                | false         | Sets the modal’s height to 100% of its parent container.                             |
| FullSize             | bool                                | false         | Sets both width and height to 100% of the parent container.                          |
| FullWidth            | bool                                | false         | Sets the modal’s width to 100% of its parent container.                              |
| IsAlert              | bool?                               | null          | Determines the ARIA role (alertdialog vs. dialog) for accessibility.                 |
| IsOpen               | bool                                | false         | Controls whether the modal is displayed.                                             |
| Modeless             | bool                                | false         | When true, the modal is modeless and will not dismiss when clicking outside.         |
| OnDismiss            | EventCallback<MouseEventArgs>       | –             | Callback function invoked when the modal is dismissed.                             |
| OnOverlayClick       | EventCallback<MouseEventArgs>       | –             | Callback function invoked when the modal overlay is clicked.                         |
| Position             | BitPosition?                        | null          | Specifies the modal’s position on the screen.                                        |
| ScrollerSelector     | string                              | "body"        | Selector for the element whose scroll is affected by the modal.                      |
| Styles               | BitModalClassStyles?                | null          | Custom CSS styles for different parts of the modal.                                  |
| SubtitleAriaId       | string?                             | null          | ARIA id for the modal subtitle.                                                      |
| TitleAriaId          | string?                             | null          | ARIA id for the modal title.                                                         |

### BitComponentBase Parameters

| Name           | Type                           | Default Value                             | Description                                                          |
| -------------- | ------------------------------ | ----------------------------------------- | -------------------------------------------------------------------- |
| AriaLabel      | string?                        | null                                      | Aria-label for screen readers.                                       |
| Class          | string?                        | null                                      | Custom CSS class for the component’s root element.                   |
| Dir            | BitDir?                        | null                                      | Sets the reading direction (LTR, RTL, or Auto).                        |
| HtmlAttributes | Dictionary<string, object>     | new Dictionary<string, object>()          | Additional HTML attributes for the component.                        |
| Id             | string?                        | null                                      | Custom id attribute; if null, a unique id is generated.                |
| IsEnabled      | bool                           | true                                      | Determines if the component is enabled.                              |
| Style          | string?                        | null                                      | Custom inline style for the component’s root element.                |
| Visibility     | BitVisibility                  | BitVisibility.Visible                     | Controls the visibility state of the component.                      |

### Public Members of BitComponentBase

| Name        | Type             | Default Value    | Description                                                       |
| ----------- | ---------------- | ---------------- | ----------------------------------------------------------------- |
| UniqueId    | Guid             | Guid.NewGuid()   | A unique identifier assigned when the component is constructed. |
| RootElement | ElementReference | –                | Reference to the root HTML element of the component.             |

---

## Enumerations

### BitModalClassStyles Properties

| Name    | Type    | Default Value | Description                                                    |
| ------- | ------- | ------------- | -------------------------------------------------------------- |
| Root    | string? | null          | Custom CSS classes/styles for the root modal container.        |
| Overlay | string? | null          | Custom CSS classes/styles for the modal overlay.               |
| Content | string? | null          | Custom CSS classes/styles for the modal content area.          |

### BitPosition Enum

Defines possible positions for the modal on the screen.

| Name         | Value | Description  |
| ------------ | ----- | ------------ |
| Center       | 0     | Center of the screen. |
| TopLeft      | 1     | Top-left corner.      |
| TopCenter    | 2     | Top-center.           |
| TopRight     | 3     | Top-right corner.     |
| CenterLeft   | 4     | Center-left.          |
| CenterRight  | 5     | Center-right.         |
| BottomLeft   | 6     | Bottom-left corner.   |
| BottomCenter | 7     | Bottom-center.        |
| BottomRight  | 8     | Bottom-right corner.  |

### BitVisibility Enum

| Name      | Value | Description                                                      |
| --------- | ----- | ---------------------------------------------------------------- |
| Visible   | 0     | The component is visible.                                        |
| Hidden    | 1     | The component is hidden (visibility: hidden) but occupies space.   |
| Collapsed | 2     | The component is not rendered (display: none).                    |

### BitDir Enum

| Name | Value | Description                                                                                     |
| ---- | ----- | ----------------------------------------------------------------------------------------------- |
| Ltr  | 0     | Left-to-right direction, used for languages that are read from left to right (e.g., English).      |
| Rtl  | 1     | Right-to-left direction, used for languages that are read from right to left (e.g., Arabic).       |
| Auto | 2     | Automatically determines the direction based on the content.                                   |

---