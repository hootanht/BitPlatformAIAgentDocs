# BitTooltip Component Reference

This document provides a comprehensive reference for the **BitTooltip** component. The Tooltip is used to briefly describe unlabeled controls or to provide additional information about labeled controls. It supports various usage scenarios including basic hover, position customization, custom content, advanced interactions, and right-to-left (RTL) support.

---

## Overview

The **Tooltip** component helps improve the accessibility and usability of your UI by displaying extra context when a user hovers or interacts with a control. It can be attached to any element (e.g., a button) to reveal supplementary information.

---

## Usage

### Basic Example

A simple tooltip example shows how to attach a tooltip to a button. Hovering over the button displays the tooltip text.

```html
<!-- Basic Tooltip Usage -->
<div class="tooltips-container">
  <div class="bit-ttp">
    <!-- Tooltip anchor element -->
    <button class="bit-btn bit-btn-otl bit-btn-pri bit-btn-md" type="button">
      <div class="bit-btn-tcn">
        <div class="bit-btn-prt">Hover over me</div>
      </div>
    </button>
    <!-- Tooltip content positioned above the anchor -->
    <div class="bit-ttp-wrp bit-ttp-top">
      <div class="bit-ttp-ctn">This is the tooltip text</div>
      <div class="bit-ttp-arw"></div>
    </div>
  </div>
</div>
```

---

### Position

The **BitTooltip** allows you to customize its position relative to the anchor element. The following example demonstrates different positions (top, right, left, bottom).

```html
<!-- Tooltip with different positions -->
<div class="tooltips-container center">
  <!-- Top positioned Tooltip -->
  <div class="bit-ttp">
    <button class="bit-btn bit-btn-otl bit-btn-pri bit-btn-md" type="button">
      <div class="bit-btn-tcn">
        <div class="bit-btn-prt">Top</div>
      </div>
    </button>
    <div class="bit-ttp-wrp bit-ttp-vis bit-ttp-top">
      <div class="bit-ttp-ctn">Text</div>
      <div class="bit-ttp-arw"></div>
    </div>
  </div>

  <!-- Right positioned Tooltip -->
  <div class="bit-ttp">
    <button class="bit-btn bit-btn-otl bit-btn-pri bit-btn-md" type="button">
      <div class="bit-btn-tcn">
        <div class="bit-btn-prt">Right</div>
      </div>
    </button>
    <div class="bit-ttp-wrp bit-ttp-vis bit-ttp-rgt">
      <div class="bit-ttp-ctn">Text</div>
      <div class="bit-ttp-arw"></div>
    </div>
  </div>

  <!-- Left positioned Tooltip -->
  <div class="bit-ttp">
    <button style="width: 100%;" class="bit-btn bit-btn-otl bit-btn-pri bit-btn-md" type="button">
      <div class="bit-btn-tcn">
        <div class="bit-btn-prt">Left</div>
      </div>
    </button>
    <div class="bit-ttp-wrp bit-ttp-vis bit-ttp-lft">
      <div class="bit-ttp-ctn">Text</div>
      <div class="bit-ttp-arw"></div>
    </div>
  </div>

  <!-- Bottom positioned Tooltip -->
  <div class="bit-ttp">
    <button class="bit-btn bit-btn-otl bit-btn-pri bit-btn-md" type="button">
      <div class="bit-btn-tcn">
        <div class="bit-btn-prt">Bottom</div>
      </div>
    </button>
    <div class="bit-ttp-wrp bit-ttp-vis bit-ttp-btm">
      <div class="bit-ttp-ctn">Text</div>
      <div class="bit-ttp-arw"></div>
    </div>
  </div>
</div>
```

---

### Custom Content

You can also provide custom content inside the tooltip. This is useful if you want to display a list or formatted information.

```html
<!-- Custom Content Example -->
<div class="tooltips-container">
  <div class="bit-ttp">
    <button class="bit-btn bit-btn-otl bit-btn-pri bit-btn-md" type="button">
      <div class="bit-btn-tcn">
        <div class="bit-btn-prt">Hover over me</div>
      </div>
    </button>
    <div class="bit-ttp-wrp bit-ttp-top">
      <div class="bit-ttp-ctn">
        <ul style="padding: 0.5rem; margin: 0;">
          <li>1. One</li>
          <li>2. Two</li>
        </ul>
      </div>
      <div class="bit-ttp-arw"></div>
    </div>
  </div>
</div>
```

---

### Advanced

Advanced usage examples allow you to customize the tooltip’s behavior and integrate it with other components such as dropdowns or toggle switches. The example below shows a tooltip with advanced customizations and additional controls.

```html
<!-- Advanced Tooltip Example -->
<div class="tooltips-container center">
  <div class="bit-ttp">
    <button style="width: 8rem;" class="bit-btn bit-btn-otl bit-btn-pri bit-btn-md" type="button">
      <div class="bit-btn-tcn">
        <div class="bit-btn-prt">Anchor</div>
      </div>
    </button>
    <div class="bit-ttp-wrp bit-ttp-vis bit-ttp-top">
      <div class="bit-ttp-ctn">Text</div>
      <div class="bit-ttp-arw"></div>
    </div>
  </div>

  <!-- Additional controls: Dropdown to select position, numeric input to adjust hide delay, toggle options -->
  <div style="width: 8rem;" class="bit-drp bit-drp-hvl">
    <label class="bit-drp-lbl" id="Dropdown-position-label">Tooltip positions</label>
    <div role="combobox" id="Dropdown-position" class="bit-drp-wrp" tabindex="0" aria-haspopup="listbox" aria-expanded="false" aria-labelledby="Dropdown-position-label Dropdown-position-text-container">
      <span id="Dropdown-position-text-container" class="bit-drp-tcn" aria-live="polite" aria-atomic="true" aria-invalid="false">Top</span>
      <span class="bit-drp-icn"><i aria-hidden="true" class="bit-icon bit-icon--ChevronRight bit-ico-r90"></i></span>
    </div>
    <div style="display:none;" class="bit-drp-ovl"></div>
    <div id="Dropdown-position-callout" tabindex="0" role="listbox" class="bit-drp-cal" aria-labelledby="Dropdown-position-label">
      <!-- Options list here -->
    </div>
    <select class="bit-input-hidden" multiple>
      <option value="Top" selected>Top</option>
    </select>
  </div>
  <!-- Toggle switches for showing/hiding arrow and controlling show behavior -->
  <div class="bit-tgl bit-tgl-chk">
    <div class="bit-tgl-cnt">
      <button role="switch" type="button" id="Toggle-ShowState" class="bit-tgl-btn" aria-checked="true" aria-labelledby="Toggle-ShowState-label">
        <span class="bit-tgl-sta"></span>
      </button>
      <label class="bit-tgl-stx" for="Toggle-ShowState">Toggle tooltip state</label>
    </div>
    <input type="checkbox" class="bit-input-hidden" value="true">
  </div>
  <div class="bit-tgl">
    <div class="bit-tgl-cnt">
      <button role="switch" type="button" id="Toggle-HideArrow" class="bit-tgl-btn" aria-checked="false" aria-labelledby="Toggle-HideArrow-label">
        <span class="bit-tgl-sta"></span>
      </button>
      <label class="bit-tgl-stx" for="Toggle-HideArrow">Hide tooltip arrow</label>
    </div>
    <input type="checkbox" class="bit-input-hidden" value="false">
  </div>
  <div class="bit-tgl bit-tgl-chk">
    <div class="bit-tgl-cnt">
      <button role="switch" type="button" id="Toggle-ShowOnClick" class="bit-tgl-btn" aria-checked="true" aria-labelledby="Toggle-ShowOnClick-label">
        <span class="bit-tgl-sta"></span>
      </button>
      <label class="bit-tgl-stx" for="Toggle-ShowOnClick">Show tooltip on click</label>
    </div>
    <input type="checkbox" class="bit-input-hidden" value="true">
  </div>
  <div class="bit-tgl">
    <div class="bit-tgl-cnt">
      <button role="switch" type="button" id="Toggle-ShowOnHover" class="bit-tgl-btn" aria-checked="false" aria-labelledby="Toggle-ShowOnHover-label">
        <span class="bit-tgl-sta"></span>
      </button>
      <label class="bit-tgl-stx" for="Toggle-ShowOnHover">Show tooltip on hover</label>
    </div>
    <input type="checkbox" class="bit-input-hidden" value="false">
  </div>
</div>
```

---

### RTL (Right-to-Left)

For languages that use a right-to-left layout (such as Arabic or Hebrew), the Tooltip component can be configured for RTL.

```html
<!-- RTL Tooltip Example -->
<div class="tooltips-container" dir="rtl">
  <div class="bit-ttp bit-rtl" dir="rtl">
    <button class="bit-btn bit-btn-otl bit-btn-pri bit-btn-md" type="button">
      <div class="bit-btn-tcn">
        <div class="bit-btn-prt">نشانگر ماوس را روی من بیاورید</div>
      </div>
    </button>
    <div class="bit-ttp-wrp bit-ttp-top">
      <div class="bit-ttp-ctn">
        <ul style="padding: 0.5rem; margin: 0;">
          <li>۱. یک</li>
          <li>۲. دو</li>
        </ul>
      </div>
      <div class="bit-ttp-arw"></div>
    </div>
  </div>
</div>
```

---

## API Reference

### BitTooltip Parameters

| **Name**        | **Type**                      | **Default Value**  | **Description**                                                                                   |
|-----------------|-------------------------------|--------------------|---------------------------------------------------------------------------------------------------|
| `Anchor`        | `RenderFragment?`             | `null`             | The content of the element that the tooltip will be attached to.                                  |
| `ChildContent`  | `RenderFragment?`             | `null`             | Alternative alias for the anchor content.                                                         |
| `Classes`       | `BitTooltipClassStyles?`      | `null`             | Custom CSS classes for different parts of the tooltip.                                            |
| `DefaultIsShown`| `bool`                        | `false`            | The default visibility state of the tooltip.                                                      |
| `HideArrow`     | `bool`                        | `false`            | If true, the arrow in the tooltip is hidden.                                                      |
| `HideDelay`     | `int`                         | `0`                | Delay in milliseconds before hiding the tooltip.                                                 |
| `IsShown`       | `bool`                        | `false`            | Controls the current visibility state of the tooltip.                                             |
| `IsShownChanged`| `EventCallback<bool>`         | –                  | Callback triggered when the `IsShown` state changes.                                              |
| `Position`      | `BitTooltipPosition`          | `BitTooltipPosition.Top` | Determines where the tooltip appears relative to its anchor.                                |
| `Template`      | `RenderFragment?`             | `null`             | Custom template for the tooltip content.                                                          |
| `Text`          | `string?`                     | `null`             | The text content of the tooltip.                                                                  |
| `ShowOnClick`   | `bool`                        | `false`            | If true, the tooltip is shown on click rather than on hover.                                      |
| `ShowDelay`     | `int`                         | `0`                | Delay in milliseconds before showing the tooltip.                                               |
| `ShowOnFocus`   | `bool`                        | `false`            | Determines if the tooltip appears when its anchor receives focus.                                 |
| `ShowOnHover`   | `bool`                        | `true`             | Determines if the tooltip appears on hover.                                                       |
| `Styles`        | `BitTooltipClassStyles?`      | `null`             | Custom CSS styles for the tooltip.                                                                |

### Inherited BitComponentBase Parameters

| **Name**         | **Type**                       | **Default Value**                  | **Description**                                                                           |
|------------------|--------------------------------|------------------------------------|-------------------------------------------------------------------------------------------|
| `AriaLabel`      | `string?`                      | `null`                             | Aria-label for the tooltip for improved accessibility.                                   |
| `Class`          | `string?`                      | `null`                             | Additional custom CSS class for the root element.                                         |
| `Dir`            | `BitDir?`                      | `null`                             | Determines the text direction (LTR, RTL, or Auto).                                          |
| `HtmlAttributes` | `Dictionary<string, object>`   | `new Dictionary<string, object>()` | Additional HTML attributes to be applied to the tooltip's root element.                   |
| `Id`             | `string?`                      | `null`                             | Custom identifier for the tooltip; if null, a unique id is generated.                      |
| `IsEnabled`      | `bool`                         | `true`                             | Determines if the tooltip is enabled.                                                     |
| `Style`          | `string?`                      | `null`                             | Inline CSS styles for the tooltip's root element.                                         |
| `Visibility`     | `BitVisibility`                | `BitVisibility.Visible`            | Controls the overall visibility of the tooltip.                                           |

### Public Members (BitComponentBase)

| **Name**       | **Type**           | **Default Value**     | **Description**                                                    |
|----------------|--------------------|-----------------------|--------------------------------------------------------------------|
| `UniqueId`     | `Guid`             | `Guid.NewGuid()`      | A read-only unique identifier for the tooltip's root element.      |
| `RootElement`  | `ElementReference` | –                     | A reference to the tooltip’s root HTML element.                    |

---

## Tooltip Class Styles

The `BitTooltipClassStyles` allows you to override the default CSS classes used by the Tooltip. You can target specific parts such as the root container, tooltip wrapper, tooltip itself, and the arrow.

| **Property**      | **Type**  | **Default Value** | **Description**                                                     |
|-------------------|-----------|-------------------|---------------------------------------------------------------------|
| `Root`            | `string?` | `null`            | Custom classes for the root element of the tooltip.                 |
| `TooltipWrapper`  | `string?` | `null`            | Custom classes for the wrapper element that contains the tooltip.     |
| `Tooltip`         | `string?` | `null`            | Custom classes for the tooltip container itself.                    |
| `Arrow`           | `string?` | `null`            | Custom classes for the tooltip arrow element.                       |

---

## Enumerations

### BitTooltipPosition Enum

Specifies the position of the tooltip relative to the anchor element.

| **Name**     | **Value** | **Description**                                                  |
|--------------|-----------|------------------------------------------------------------------|
| `Top`        | `0`       | Displays the tooltip above the anchor.                           |
| `TopLeft`    | `1`       | Positions the tooltip at the top left of the anchor.              |
| `TopRight`   | `2`       | Positions the tooltip at the top right of the anchor.             |
| `RightTop`   | `3`       | Positions the tooltip to the right, near the top of the anchor.     |
| `Right`      | `4`       | Displays the tooltip to the right of the anchor.                  |
| `RightBottom`| `5`       | Positions the tooltip to the right, near the bottom of the anchor.  |
| `BottomRight`| `6`       | Displays the tooltip below and to the right of the anchor.          |
| `Bottom`     | `7`       | Displays the tooltip below the anchor.                             |
| `BottomLeft` | `8`       | Displays the tooltip below and to the left of the anchor.           |
| `LeftBottom` | `9`       | Positions the tooltip to the left, near the bottom of the anchor.   |
| `Left`       | `10`      | Displays the tooltip to the left of the anchor.                    |
| `LeftTop`    | `11`      | Positions the tooltip to the left, near the top of the anchor.      |

### BitVisibility Enum

Defines how the tooltip should be rendered in terms of visibility.

| **Name**    | **Value** | **Description**                                                                   |
|-------------|-----------|-----------------------------------------------------------------------------------|
| `Visible`   | `0`       | The tooltip is visible.                                                           |
| `Hidden`    | `1`       | The tooltip is hidden (using CSS `visibility: hidden`), space is reserved.        |
| `Collapsed` | `2`       | The tooltip is collapsed (using CSS `display: none`), not taking any space.        |

### BitDir Enum

Specifies the text direction for the tooltip component.

| **Name** | **Value** | **Description**                                                               |
|----------|-----------|-------------------------------------------------------------------------------|
| `Ltr`    | `0`       | Left-to-right; use for languages like English.                              |
| `Rtl`    | `1`       | Right-to-left; use for languages like Arabic or Hebrew.                     |
| `Auto`   | `2`       | Automatically detect direction based on the content.                        |

### BitTooltipClassStyles Enum (Reference)

For further customization, you can override the built-in class styles by using the `BitTooltipClassStyles` property.

---