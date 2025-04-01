# ActionButton Component Reference

The **ActionButton** is a specialized button component with pre-defined visual styles, behavior, and API properties. It can function as a standard button or an anchor element when a URL is provided. This reference covers all aspects of the component—from basic usage to advanced customization options and API details.

---

## Overview

The `ActionButton` component is designed to streamline the creation of interactive buttons that integrate seamlessly into your application. It supports:

- **Standard Button Behavior:** Clickable, form-integrated buttons.
- **Hyperlink Functionality:** Renders as an anchor tag when an `Href` is provided.
- **Icon Support:** Easily include icons with optional reversed order.
- **Multiple Visual Variants:** Change colors, sizes, and styles with built-in classes.
- **Accessibility Features:** ARIA properties, customizable tooltips, and more.
- **RTL Support:** Full support for right-to-left languages.

---

## Usage

### Basic Usage

A basic example of an ActionButton renders as a standard clickable button with an icon and text:

```html
<button class="bit-acb bit-acb-pri bit-acb-md">
  <i class="bit-acb-ico bit-icon bit-icon--AddFriend"></i>
  <div class="bit-acb-con">Create account</div>
</button>
```

---

### Using ActionButton as a Link

By providing an `Href` attribute, the button is rendered as an anchor element, which can open in a new tab or the same window:

```html
<a class="bit-acb bit-acb-pri bit-acb-md" href="https://bitplatform.dev" target="_blank">
  <i class="bit-acb-ico bit-icon bit-icon--Globe"></i>
  <div class="bit-acb-con">Open bitplatform.dev</div>
</a>
```

---

### Specifying a `Rel` Attribute

For security and SEO purposes, you may need to include a `rel` attribute:

```html
<a class="bit-acb bit-acb-pri bit-acb-md" href="https://bitplatform.dev" target="_blank" rel="nofollow noreferrer">
  <i class="bit-acb-ico bit-icon bit-icon--Globe"></i>
  <div class="bit-acb-con">Open bitplatform.dev (nofollow &amp; noreferrer)</div>
</a>
```

---

### Color Variants

ActionButton comes with a set of predefined color themes. For example, a primary button can be rendered as follows:

```html
<button class="bit-acb bit-acb-pri bit-acb-md">
  <i class="bit-acb-ico bit-icon bit-icon--ColorSolid"></i>
  <div class="bit-acb-con">Primary</div>
</button>
```

Other available color classes include:

- **Secondary:** `bit-acb-sec`
- **Tertiary:** `bit-acb-ter`
- **Info:** `bit-acb-inf`
- **Success:** `bit-acb-suc`
- **Warning:** `bit-acb-wrn`
- **SevereWarning:** `bit-acb-swr`
- **Error:** `bit-acb-err`

In addition, background and foreground variations can be applied with classes such as `bit-acb-pbg` (Primary Background), `bit-acb-sfg` (Secondary Foreground), etc.

---

### Size Variants

ActionButton supports different sizes to fit various UI needs. Below are examples for small, medium, and large buttons:

```html
<button class="bit-acb bit-acb-pri bit-acb-sm">
  <i class="bit-acb-ico bit-icon bit-icon--FontSize"></i>
  <div class="bit-acb-con">Small</div>
</button>

<button class="bit-acb bit-acb-pri bit-acb-md">
  <i class="bit-acb-ico bit-icon bit-icon--FontSize"></i>
  <div class="bit-acb-con">Medium</div>
</button>

<button class="bit-acb bit-acb-pri bit-acb-lg">
  <i class="bit-acb-ico bit-icon bit-icon--FontSize"></i>
  <div class="bit-acb-con">Large</div>
</button>
```

---

### Style & Class Customization

Customize the appearance of the ActionButton by overriding styles or adding custom CSS classes:

```html
<button style="font-size: 1.5rem;" class="bit-acb bit-acb-pri bit-acb-md">
  <i style="color: blueviolet;" class="bit-acb-ico bit-icon bit-icon--Brush"></i>
  <div style="text-shadow: aqua 0 0 1rem;" class="bit-acb-con">
    Action Button Styles
  </div>
</button>
```

You can also apply custom CSS classes for the root element, icon, or content using the `Classes` and `Styles` properties.

---

### Template Customization

Integrate custom templates within the ActionButton to include complex layouts or additional elements:

```html
<button class="bit-acb bit-acb-pri bit-acb-md">
  <i class="bit-acb-ico bit-icon bit-icon--AddFriend"></i>
  <div class="bit-acb-con">
    <div style="display: flex; gap: 0.5rem;">
      <div>This is a custom template</div>
      <!-- Additional custom elements, like a loading spinner, can be placed here -->
    </div>
  </div>
</button>
```

---

### Button Types and Form Integration

ActionButton can act as a submit, reset, or normal button when used inside a form:

```html
<form novalidate>
  <!-- Other form elements -->

  <button type="submit" class="bit-acb bit-acb-pri bit-acb-md">
    <i class="bit-acb-ico bit-icon bit-icon--SendMirrored"></i>
    <div class="bit-acb-con">Submit</div>
  </button>

  <button type="reset" class="bit-acb bit-acb-pri bit-acb-md">
    <i class="bit-acb-ico bit-icon bit-icon--Reset"></i>
    <div class="bit-acb-con">Reset</div>
  </button>

  <button type="button" class="bit-acb bit-acb-pri bit-acb-md">
    <i class="bit-acb-ico bit-icon bit-icon--ButtonControl"></i>
    <div class="bit-acb-con">Button</div>
  </button>
</form>
```

---

### Right-to-Left (RTL) Support

For applications that require RTL language support, the ActionButton can be configured with RTL properties:

```html
<div dir="rtl">
  <button class="bit-acb bit-rtl bit-acb-pri bit-acb-md" type="button" dir="rtl">
    <i class="bit-acb-ico bit-icon bit-icon--AddFriend"></i>
    <div class="bit-acb-con">ساخت حساب</div>
  </button>
</div>
```

---

## API Reference

Below are the key properties and API details for the ActionButton component.

### BitActionButton Parameters

| **Name**             | **Type**                       | **Default** | **Description**                                                                              |
|----------------------|--------------------------------|-------------|----------------------------------------------------------------------------------------------|
| AllowDisabledFocus   | `bool`                         | false       | Allows the button to receive focus even when disabled.                                      |
| AriaDescription      | `string?`                      | null        | Detailed description for assistive technologies.                                             |
| AriaHidden           | `bool`                         | false       | If true, adds `aria-hidden` to exclude the button from screen readers.                         |
| ButtonType           | `BitButtonType`                | null        | Specifies the HTML `type` (e.g., button, submit, reset).                                      |
| ChildContent         | `RenderFragment?`              | null        | The content to be rendered inside the button.                                                |
| Classes              | `BitActionButtonClassStyles?`  | null        | Custom CSS classes for styling different parts of the button.                                |
| Color                | `BitColor?`                    | null        | Sets the overall color theme of the button.                                                  |
| FullWidth            | `bool`                         | false       | Renders the button to fill the full width of its container.                                   |
| Href                 | `string?`                      | null        | When provided, renders the component as an anchor (`<a>`) element.                             |
| IconName             | `string?`                      | null        | The name of the icon to be displayed inside the button.                                      |
| IconOnly             | `bool`                         | null        | Renders only the icon, omitting the text container.                                          |
| OnClick              | `EventCallback<MouseEventArgs>`|             | Callback executed on the button's click event.                                               |
| Styles               | `BitActionButtonClassStyles?`  | null        | Inline CSS styles for customizing different parts of the button.                              |
| ReversedIcon         | `bool`                         | false       | Reverses the positions of the icon and the text.                                             |
| Rel                  | `BitLinkRel?`                  | null        | Specifies the relationship for anchor links when `Href` is provided.                           |
| Size                 | `BitSize?`                     | null        | Sets the size of the button (Small, Medium, or Large).                                         |
| Target               | `string?`                      | null        | Specifies where to open the linked document when using an anchor element.                      |
| Title                | `string?`                      | null        | Tooltip text displayed on hover.                                                             |

---

### BitComponentBase Parameters

| **Name**         | **Type**                            | **Default**                                | **Description**                                                                    |
|------------------|-------------------------------------|--------------------------------------------|------------------------------------------------------------------------------------|
| AriaLabel        | `string?`                           | null                                       | Accessible label for the component.                                              |
| Class            | `string?`                           | null                                       | Custom CSS class for the root element.                                             |
| Dir              | `BitDir?`                           | null                                       | Specifies text direction (LTR/RTL).                                                |
| HtmlAttributes   | `Dictionary<string, object>`        | `new Dictionary<string, object>()`         | Additional HTML attributes to be applied to the root element.                      |
| Id               | `string?`                           | null                                       | Custom id for the root element; if not provided, a unique id is generated.         |
| IsEnabled        | `bool`                              | true                                       | Determines if the component is interactive.                                      |
| Style            | `string?`                           | null                                       | Inline styles for the root element.                                                |
| Visibility       | `BitVisibility`                     | `BitVisibility.Visible`                    | Controls whether the component is visible, hidden, or collapsed.                   |

---

### Public Members

| **Name**      | **Type**         | **Default**         | **Description**                                                       |
|---------------|------------------|---------------------|-----------------------------------------------------------------------|
| UniqueId      | `Guid`           | `Guid.NewGuid()`    | A read-only unique identifier assigned at component instantiation.   |
| RootElement   | `ElementReference`|                     | A reference to the component's root HTML element.                   |

---

### Enumerations

#### BitButtonType

| **Name** | **Value** | **Description**                           |
|----------|-----------|-------------------------------------------|
| Button   | 0         | A standard clickable button.              |
| Submit   | 1         | A button that submits form data.          |
| Reset    | 2         | A button that resets form inputs.         |

---

#### BitColor

| **Name**              | **Value** | **Description**                        |
|-----------------------|-----------|----------------------------------------|
| Primary               | 0         | Primary theme color.                   |
| Secondary             | 1         | Secondary theme color.                 |
| Tertiary              | 2         | Tertiary theme color.                  |
| Info                  | 3         | Informational color.                   |
| Success               | 4         | Success color.                         |
| Warning               | 5         | Warning color.                         |
| SevereWarning         | 6         | Severe warning color.                  |
| Error                 | 7         | Error color.                           |
| PrimaryBackground     | 8         | Primary background color.              |
| SecondaryBackground   | 9         | Secondary background color.            |
| TertiaryBackground    | 10        | Tertiary background color.             |
| PrimaryForeground     | 11        | Primary foreground color.              |
| SecondaryForeground   | 12        | Secondary foreground color.            |
| TertiaryForeground    | 13        | Tertiary foreground color.             |
| PrimaryBorder         | 14        | Primary border color.                  |
| SecondaryBorder       | 15        | Secondary border color.                |
| TertiaryBorder        | 16        | Tertiary border color.                 |

---

#### BitSize

| **Name** | **Value** | **Description**           |
|----------|-----------|---------------------------|
| Small    | 0         | Small sized button.       |
| Medium   | 1         | Medium sized button.      |
| Large    | 2         | Large sized button.       |

---

#### BitLinkRel

| **Name**       | **Value** | **Description**                                                                              |
|----------------|-----------|----------------------------------------------------------------------------------------------|
| Alternate      | 1         | Provides an alternate representation of the document.                                      |
| Author         | 2         | Links to the author of the document.                                                        |
| Bookmark       | 4         | A permanent URL for bookmarking.                                                            |
| External       | 8         | Indicates the linked document is from an external site.                                     |
| Help           | 16        | Provides a link to a help document.                                                         |
| License        | 32        | Provides a link to licensing information.                                                   |
| Next           | 64        | Points to the next document in a series.                                                    |
| NoFollow       | 128       | Instructs search engines not to follow the link.                                              |
| NoOpener       | 256       | Prevents the new browsing context from accessing the originating window.                    |
| NoReferrer     | 512       | Omits the referrer header when the link is followed.                                          |
| Prev           | 1024      | Points to the previous document in a series.                                                |
| Search         | 2048      | Links to a search tool for the document.                                                    |
| Tag            | 4096      | Provides a tag (keyword) for the document.                                                  |

---

#### BitVisibility

| **Name**  | **Value** | **Description**                                                  |
|-----------|-----------|------------------------------------------------------------------|
| Visible   | 0         | The component is visible.                                        |
| Hidden    | 1         | The component is hidden (using `visibility: hidden`) but occupies space. |
| Collapsed | 2         | The component is removed from the layout (using `display: none`).  |

---

#### BitDir

| **Name** | **Value** | **Description**                                                  |
|----------|-----------|------------------------------------------------------------------|
| Ltr      | 0         | Left-to-right text direction (e.g., for English).                |
| Rtl      | 1         | Right-to-left text direction (e.g., for Arabic).                 |
| Auto     | 2         | Automatically determines direction based on content.             |

---