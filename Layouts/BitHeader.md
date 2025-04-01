# BitHeader Component Documentation

The **BitHeader** component is used to display a title (and optionally other interactive elements) in a colored bar at the top of a site or application. It typically uses the current primary background color for its background, creating a consistent look and feel across your application.

---

## Overview

The BitHeader component serves as the top section of your application layout. It can contain:
- A title or logo
- Navigation buttons (e.g., a global nav button)
- User action buttons (e.g., Sign In)
- Overflow menus for additional options

It is highly customizable through its parameters and can be styled using regular CSS.

---

## Usage

### Basic Example

The simplest use of BitHeader involves rendering a header with static text. For example:

```html
<header id="nac8t7" class="bit-hdr">
  <div class="bit-hdr-gut">
    I'm a Header
  </div>
</header>
```

### Advanced Header with Navigation

A more advanced example may include navigation controls, a title, a flexible spacer, and additional buttons with an overflow menu. For instance:

```html
<header id="oxf6jl" style="gap: 1rem;" class="bit-hdr">
  <div class="bit-hdr-gut">
    <!-- Navigation Button -->
    <button id="x8x63y" class="bit-btn bit-btn-ntx bit-btn-txt bit-btn-pri bit-btn-md" type="button" title="Open Navigation">
      <i class="bit-btn-icn bit-icon bit-icon--GlobalNavButton"></i>
    </button>

    <!-- Application Title -->
    <span id="2i55ys" class="bit-txt bit-txt-caption1">My Awesome App</span>

    <!-- Flexible Spacer -->
    <div id="wsa01l" style="flex-grow:1" class="bit-spc"></div>

    <!-- Sign In Button -->
    <button id="habz9e" class="bit-btn bit-btn-ntx bit-btn-txt bit-btn-pri bit-btn-md" type="button" title="Sign in">
      <i class="bit-btn-icn bit-icon bit-icon--Contact"></i>
    </button>

    <!-- Overflow Menu Button -->
    <div title="See more" id="q9xltj" class="bit-mnb bit-mnb-pri bit-mnb-md bit-mnb-nsp bit-mnb-txt">
      <button type="button" tabindex="0" style="padding: 0.5rem;" class="bit-mnb-opb">
        <i class="bit-icon bit-icon--More"></i>
      </button>
      <div style="display:none;" class="bit-mnb-ovl"></div>
      <div id="BitMenuButton-q9xltj-callout" class="bit-mnb-cal">
        <ul role="presentation" class="bit-mnb-cul">
          <li role="presentation">
            <button role="menuitem" type="button" tabindex="0" class="bit-mnb-itm">
              <i class="bit-mnb-iic bit-icon bit-icon--Settings"></i>
              <span class="bit-mnb-btx">Settings</span>
            </button>
          </li>
          <li role="presentation">
            <button role="menuitem" type="button" tabindex="0" class="bit-mnb-itm">
              <i class="bit-mnb-iic bit-icon bit-icon--Info"></i>
              <span class="bit-mnb-btx">About</span>
            </button>
          </li>
          <li role="presentation">
            <button role="menuitem" type="button" tabindex="0" class="bit-mnb-itm">
              <i class="bit-mnb-iic bit-icon bit-icon--Feedback"></i>
              <span class="bit-mnb-btx">Feedback</span>
            </button>
          </li>
        </ul>
      </div>
    </div>
  </div>
</header>
```

---

## API Reference

### BitHeader Parameters

| Name           | Type              | Default Value | Description                                                                       |
|----------------|-------------------|---------------|-----------------------------------------------------------------------------------|
| **ChildContent** | `RenderFragment?` | `null`        | Gets or sets the content to be rendered inside the BitHeader.                     |
| **Height**       | `int?`           | `null`        | Specifies the height of the BitHeader in pixels.                                  |
| **Fixed**        | `bool`           | `false`       | If `true`, renders the header with a fixed position at the top of the page.         |

### Inherited BitComponentBase Parameters

| Name               | Type                         | Default Value                        | Description                                                           |
|--------------------|------------------------------|--------------------------------------|-----------------------------------------------------------------------|
| **AriaLabel**      | `string?`                    | `null`                               | ARIA label for the header, for accessibility.                         |
| **Class**          | `string?`                    | `null`                               | Custom CSS classes for the header container.                          |
| **Dir**            | `BitDir?`                    | `null`                               | Sets the text direction (LTR, RTL, or Auto).                           |
| **HtmlAttributes** | `Dictionary<string, object>` | `new Dictionary<string, object>()`   | Additional HTML attributes for the header container.                  |
| **Id**             | `string?`                    | `null`                               | Custom id for the header; if not provided, a unique id is generated.    |
| **IsEnabled**      | `bool`                       | `true`                               | Determines whether the header is enabled.                             |
| **Style**          | `string?`                    | `null`                               | Inline CSS styles for the header container.                           |
| **Visibility**     | `BitVisibility`              | `BitVisibility.Visible`              | Controls the visibility state of the header (visible, hidden, collapsed).|

---
```