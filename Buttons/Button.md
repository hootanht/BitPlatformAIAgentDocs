# Button Component Reference

The **Button** component provides users with a simple way to trigger actions via a single tap or click. It is used throughout applications—in forms, dialogs, navigation, and repeated actions. This reference covers every aspect of the Button component including usage examples, API parameters, styling options, and available enumerations.

---

## Overview

Buttons allow users to initiate actions. The component supports multiple variants, including primary and secondary styles, different visual variants (Fill, Outline, Text), and built‐in features such as icons, loading states, and hyperlink behavior. Additionally, the Button component supports full customization through templates, custom classes, and inline styles.

---

## Usage

### Basic

A simple button with default styling:

```html
<button class="bit-btn bit-btn-fil bit-btn-pri bit-btn-md" type="button">
  <div class="bit-btn-tcn">
    <div class="bit-btn-prt">Button</div>
  </div>
</button>
```

### Primary & Secondary

Buttons can be used with different text sections. For example, a primary button might include only the primary text, while a secondary button adds a secondary text section:

```html
<!-- Primary Text Button -->
<button class="bit-btn bit-btn-fil bit-btn-pri bit-btn-md" type="button">
  <div class="bit-btn-tcn">
    <div class="bit-btn-prt">Primary text</div>
  </div>
</button>

<!-- Button with Primary and Secondary Text -->
<button class="bit-btn bit-btn-hsc bit-btn-fil bit-btn-pri bit-btn-md" type="button">
  <div class="bit-btn-tcn">
    <div class="bit-btn-prt">Primary text</div>
    <div class="bit-btn-sct">this is the secondary text</div>
  </div>
</button>
```

### Variant

The Button supports three visual variants:

- **Fill (default)**
- **Outline**
- **Text**

```html
<!-- Fill Variant -->
<button class="bit-btn bit-btn-fil bit-btn-pri bit-btn-md" type="button">
  <div class="bit-btn-tcn">
    <div class="bit-btn-prt">Fill</div>
  </div>
</button>

<!-- Outline Variant -->
<button class="bit-btn bit-btn-otl bit-btn-pri bit-btn-md" type="button">
  <div class="bit-btn-tcn">
    <div class="bit-btn-prt">Outline</div>
  </div>
</button>

<!-- Text Variant -->
<button class="bit-btn bit-btn-txt bit-btn-pri bit-btn-md" type="button">
  <div class="bit-btn-tcn">
    <div class="bit-btn-prt">Text</div>
  </div>
</button>
```

### Icon

Buttons may include icons. The icon can be rendered in a default (start) or reversed (end) position. They also support using a custom image URL as the icon.

```html
<!-- Button with Icon at Start (default) -->
<button class="bit-btn bit-btn-fil bit-btn-pri bit-btn-md" type="button">
  <i class="bit-btn-icn bit-icon bit-icon--Emoji"></i>
  <div class="bit-btn-tcn">
    <div class="bit-btn-prt">Start</div>
  </div>
</button>

<!-- Button with Icon at End (reversed) -->
<button class="bit-btn bit-btn-fil bit-btn-pri bit-btn-md bit-btn-rvi" type="button">
  <i class="bit-btn-icn bit-icon bit-icon--Emoji2"></i>
  <div class="bit-btn-tcn">
    <div class="bit-btn-prt">End</div>
  </div>
</button>

<!-- Button with Custom Icon URL -->
<button class="bit-btn bit-btn-hsc bit-btn-otl bit-btn-pri bit-btn-md" type="button">
  <img src="/_content/Bit.BlazorUI.Demo.Client.Core/images/bit-logo.svg" class="bit-btn-icnu">
  <div class="bit-btn-tcn">
    <div class="bit-btn-prt">IconUrl</div>
  </div>
</button>
```

### Loading

Demonstrate the dynamic loading state by using the `IsLoading` property. When active, the button can show a spinner along with a custom label.

```html
<!-- Simple Loading Button -->
<button style="min-width: 11rem" class="bit-btn bit-btn-fil bit-btn-pri bit-btn-md" type="button">
  <div class="bit-btn-tcn">
    <div class="bit-btn-prt">Click me</div>
  </div>
</button>

<!-- Button with Secondary Text in Loading State -->
<button style="min-width: 11rem" class="bit-btn bit-btn-hsc bit-btn-fil bit-btn-pri bit-btn-md" type="button">
  <div class="bit-btn-tcn">
    <div class="bit-btn-prt">Click me</div>
    <div class="bit-btn-sct">this is the secondary text</div>
  </div>
</button>
```

Buttons also support an **AutoLoading** mode that automatically enters a loading state when the click event is triggered.

### Loading Label

Customize the loading label and its position relative to the spinner icon:

```html
<!-- Loading Label Positioned at the End -->
<button style="min-width: 6.5rem;" class="bit-btn bit-btn-otl bit-btn-pri bit-btn-md" type="button">
  <div class="bit-btn-ldg bit-btn-end">
    <div class="bit-btn-spn"></div>
    <div class="bit-btn-lbl">End...</div>
  </div>
</button>

<!-- Loading Label Positioned at the Start -->
<button style="min-width: 6.5rem;" class="bit-btn bit-btn-otl bit-btn-pri bit-btn-md" type="button">
  <div class="bit-btn-ldg bit-btn-srt">
    <div class="bit-btn-spn"></div>
    <div class="bit-btn-lbl">Start...</div>
  </div>
</button>

<!-- Loading Label Positioned at the Bottom -->
<button style="min-width: 6.5rem;" class="bit-btn bit-btn-otl bit-btn-pri bit-btn-md" type="button">
  <div class="bit-btn-ldg bit-btn-btm">
    <div class="bit-btn-spn"></div>
    <div class="bit-btn-lbl">Bottom...</div>
  </div>
</button>

<!-- Loading Label Positioned at the Top -->
<button style="min-width: 6.5rem;" class="bit-btn bit-btn-otl bit-btn-pri bit-btn-md" type="button">
  <div class="bit-btn-ldg bit-btn-top">
    <div class="bit-btn-spn"></div>
    <div class="bit-btn-lbl">Top...</div>
  </div>
</button>
```

### Href & Rel

The Button can render as an anchor element by providing an `Href` value. It can also accept a `rel` attribute for SEO and security purposes.

```html
<!-- Button as a Link -->
<a class="bit-btn bit-btn-otl bit-btn-pri bit-btn-md" href="https://bitplatform.dev" target="_blank">
  <i class="bit-btn-icn bit-icon bit-icon--Globe"></i>
  <div class="bit-btn-tcn">
    <div class="bit-btn-prt">Open bitplatform.dev</div>
  </div>
</a>

<!-- Button as a Link with a rel attribute -->
<a rel="nofollow" class="bit-btn bit-btn-otl bit-btn-pri bit-btn-md" href="https://bitplatform.dev" target="_blank">
  <i class="bit-btn-icn bit-icon bit-icon--Globe"></i>
  <div class="bit-btn-tcn">
    <div class="bit-btn-prt">Open bitplatform.dev (nofollow)</div>
  </div>
</a>
```

### Float

The Button component supports floating behavior, which allows it to be positioned relative to the viewport or its container. You can adjust the float mode and offset:

```html
<!-- Floating Button Example -->
<div style="position: relative; border: 1px solid gray;">
  <button class="bit-btn bit-btn-ntx bit-btn-fil bit-btn-pri bit-btn-md bit-btn-fab bit-btn-brg" type="button">
    <i class="bit-btn-icn bit-icon bit-icon--Add"></i>
  </button>
  <!-- Additional elements and offset settings can be applied here -->
</div>
```

Additionally, a dropdown control can be used to select a float position (e.g., TopLeft, TopCenter, BottomRight) and an input for float offset.

### Button Type

When used within a form, the Button component supports three types:

- **Submit** – Submits form data.
- **Reset** – Resets form inputs.
- **Button** – A generic clickable button.

```html
<form novalidate>
  <div class="bit-tfl bit-tfl-req">
    <label class="bit-tfl-lbl" for="BitTextField-required">Required</label>
    <div class="bit-tfl-fgp">
      <input id="BitTextField-required" required class="bit-tfl-inp" spellcheck="false">
    </div>
  </div>
  <br>
  <div>
    <button class="bit-btn bit-btn-fil bit-btn-pri bit-btn-md" type="submit">
      <div class="bit-btn-tcn">
        <div class="bit-btn-prt">Submit</div>
      </div>
    </button>
    <button class="bit-btn bit-btn-fil bit-btn-pri bit-btn-md" type="reset">
      <div class="bit-btn-tcn">
        <div class="bit-btn-prt">Reset</div>
      </div>
    </button>
    <button class="bit-btn bit-btn-fil bit-btn-pri bit-btn-md" type="button">
      <div class="bit-btn-tcn">
        <div class="bit-btn-prt">Button</div>
      </div>
    </button>
  </div>
</form>
```

### Templates

Customize the content of the Button by using custom templates. You can override the default primary and secondary sections with your own content and layout.

```html
<button class="bit-btn bit-btn-fil bit-btn-pri bit-btn-md custom-content" type="button">
  <div class="bit-btn-tcn">
    <div class="bit-btn-prt">
      <i class="bit-ico bit-ico-ter bit-icon bit-icon--Airplane"></i>
      <span>A primary template</span>
      <!-- Custom decorative elements can be included here -->
    </div>
  </div>
</button>
```

### RTL

The Button supports right-to-left (RTL) layout for languages such as Arabic. Simply set the `dir="rtl"` attribute and add the `bit-rtl` class:

```html
<div dir="rtl">
  <button class="bit-btn bit-rtl bit-btn-fil bit-btn-pri bit-btn-md" type="button" dir="rtl">
    <i class="bit-btn-icn bit-icon bit-icon--Emoji"></i>
    <div class="bit-btn-tcn">
      <div class="bit-btn-prt">دکمه با آیکن</div>
    </div>
  </button>
</div>
```

---

## API Reference

### BitButton Parameters

| **Name**               | **Type**                         | **Default**        | **Description**                                                                                              |
|------------------------|----------------------------------|--------------------|--------------------------------------------------------------------------------------------------------------|
| AllowDisabledFocus     | `bool`                           | `true`             | Whether the button can receive focus even when disabled.                                                   |
| AriaDescription        | `string?`                        | `null`             | Detailed description for screen readers.                                                                   |
| AriaHidden             | `bool`                           | `false`            | If true, adds an `aria-hidden` attribute so screen readers ignore the element.                               |
| AutoLoading            | `bool`                           | `false`            | Automatically enters loading state on click and prevents multiple clicks by default.                         |
| ButtonType             | `BitButtonType?`                 | `null`             | Specifies the HTML `type` (Button, Submit, Reset).                                                           |
| ChildContent           | `RenderFragment?`                | `null`             | Content for the primary section of the button (alias of PrimaryTemplate).                                    |
| Classes                | `BitButtonClassStyles?`          | `null`             | Custom CSS classes for various parts of the button.                                                         |
| Color                  | `BitColor?`                      | `null`             | Overall color theme of the button.                                                                           |
| FixedColor             | `bool`                           | `false`            | Fixes the foreground color regardless of hover/focus state.                                                  |
| Float                  | `bool`                           | `false`            | Enables floating behavior so the button can be positioned relative to the viewport.                          |
| FloatAbsolute          | `bool`                           | `false`            | Positions the floating button relative to its container.                                                   |
| FloatOffset            | `string?`                        | `null`             | Specifies the offset for the floating button.                                                                |
| FloatPosition          | `BitPosition?`                   | `false`            | Determines the float position (e.g., TopLeft, BottomRight).                                                  |
| FullWidth              | `bool`                           | `false`            | Expands the button to fill 100% of its container’s width.                                                    |
| Href                   | `string?`                        | `null`             | If provided, renders the button as an anchor element instead of a button.                                    |
| IconName               | `string?`                        | `null`             | The name of the icon to render.                                                                              |
| IconOnly               | `bool`                           | `false`            | If true, only the icon is rendered without any text.                                                         |
| IconUrl                | `string?`                        | `null`             | URL for a custom image to be used as the icon.                                                                 |
| IsLoading              | `bool`                           | `false`            | Indicates whether the button is in a loading state.                                                          |
| LoadingLabel           | `string?`                        | `null`             | Custom text label displayed alongside the spinner when loading.                                              |
| LoadingLabelPosition   | `BitLabelPosition`               | `BitLabelPosition.End` | Position of the loading label relative to the spinner.                                                   |
| LoadingTemplate        | `RenderFragment?`                | `null`             | Custom template to display when the button is in the loading state.                                            |
| OnClick                | `EventCallback<bool>`            |                    | Callback executed when the button is clicked, receiving the current loading state as a parameter.             |
| PrimaryTemplate        | `RenderFragment?`                | `null`             | Custom content for the primary section of the button (alias of ChildContent).                                |
| Reclickable            | `bool`                           | `false`            | Allows the button to be clicked again even when in a loading state (when AutoLoading is enabled).              |
| ReversedIcon           | `bool`                           | `false`            | Reverses the positions of the icon and the main content.                                                     |
| Rel                    | `BitLinkRel?`                    | `null`             | Relationship attribute for anchor links (when Href is provided).                                             |
| SecondaryText          | `string?`                        | `null`             | Text for the secondary section of the button.                                                                |
| SecondaryTemplate      | `RenderFragment?`                | `null`             | Custom content for the secondary section of the button.                                                      |
| Size                   | `BitSize?`                       | `null`             | Size of the button (Small, Medium, or Large).                                                                  |
| Styles                 | `BitButtonClassStyles?`          | `null`             | Inline CSS styles for the button's various parts.                                                            |
| Target                 | `string?`                        | `null`             | Specifies where to open the linked document (when Href is provided).                                           |
| Title                  | `string?`                        | `null`             | Tooltip text to display on hover.                                                                            |
| Variant                | `BitVariant?`                    | `null`             | Visual variant of the button (Fill, Outline, or Text).                                                         |

---

### BitComponentBase Parameters

| **Name**         | **Type**                        | **Default**                        | **Description**                                                                      |
|------------------|---------------------------------|------------------------------------|--------------------------------------------------------------------------------------|
| AriaLabel        | `string?`                       | `null`                             | Accessible label for the component.                                                |
| Class            | `string?`                       | `null`                             | Custom CSS class for the root element.                                               |
| Dir              | `BitDir?`                       | `null`                             | Text direction (LTR, RTL, or Auto).                                                  |
| HtmlAttributes   | `Dictionary<string, object>`    | `new Dictionary<string, object>()` | Additional HTML attributes for the root element.                                   |
| Id               | `string?`                       | `null`                             | Custom ID for the component; if omitted, a unique ID is generated.                   |
| IsEnabled        | `bool`                          | `true`                             | Indicates whether the component is enabled for interaction.                        |
| Style            | `string?`                       | `null`                             | Inline styles for the root element.                                                  |
| Visibility       | `BitVisibility`                 | `BitVisibility.Visible`            | Controls whether the component is visible, hidden, or collapsed.                     |

---

### Public Members

| **Name**      | **Type**         | **Default**         | **Description**                                                       |
|---------------|------------------|---------------------|-----------------------------------------------------------------------|
| UniqueId      | `Guid`           | `Guid.NewGuid()`    | Read-only unique identifier assigned at component instantiation.    |
| RootElement   | `ElementReference` |                   | Reference to the component’s root HTML element.                     |

---

### BitButtonClassStyles Properties

These properties allow you to override default CSS classes for various parts of the Button component.

| **Name**       | **Type**  | **Default** | **Description**                                                         |
|----------------|-----------|-------------|-------------------------------------------------------------------------|
| Root           | `string?` | `null`      | Custom CSS classes/styles for the root element of the Button.           |
| Icon           | `string?` | `null`      | Custom classes/styles for the icon element.                             |
| Container      | `string?` | `null`      | Custom classes/styles for the internal container of the Button.         |
| Primary        | `string?` | `null`      | Custom classes/styles for the primary text section.                     |
| Secondary      | `string?` | `null`      | Custom classes/styles for the secondary text section.                   |
| LoadingContainer | `string?` | `null`    | Custom classes/styles for the container shown during the loading state.   |
| Spinner        | `string?` | `null`      | Custom classes/styles for the spinner element.                          |
| LoadingLabel   | `string?` | `null`      | Custom classes/styles for the loading label element.                    |

---

## Enumerations

### BitVariant

| **Name** | **Value** | **Description**                  |
|----------|-----------|----------------------------------|
| Fill     | 0         | Default fill styled variant.     |
| Outline  | 1         | Outline styled variant.          |
| Text     | 2         | Text styled variant.             |

### BitColor

| **Name**              | **Value** | **Description**                       |
|-----------------------|-----------|---------------------------------------|
| Primary               | 0         | Primary theme color.                  |
| Secondary             | 1         | Secondary theme color.                |
| Tertiary              | 2         | Tertiary theme color.                 |
| Info                  | 3         | Informational color.                  |
| Success               | 4         | Success color.                        |
| Warning               | 5         | Warning color.                        |
| SevereWarning         | 6         | Severe warning color.                 |
| Error                 | 7         | Error color.                          |
| PrimaryBackground     | 8         | Primary background color.             |
| SecondaryBackground   | 9         | Secondary background color.           |
| TertiaryBackground    | 10        | Tertiary background color.            |
| PrimaryForeground     | 11        | Primary foreground color.             |
| SecondaryForeground   | 12        | Secondary foreground color.           |
| TertiaryForeground    | 13        | Tertiary foreground color.            |
| PrimaryBorder         | 14        | Primary border color.                 |
| SecondaryBorder       | 15        | Secondary border color.               |
| TertiaryBorder        | 16        | Tertiary border color.                |

### BitSize

| **Name** | **Value** | **Description**           |
|----------|-----------|---------------------------|
| Small    | 0         | Small sized button.       |
| Medium   | 1         | Medium sized button.      |
| Large    | 2         | Large sized button.       |

### BitButtonType

| **Name** | **Value** | **Description**                           |
|----------|-----------|-------------------------------------------|
| Button   | 0         | Standard clickable button.                |
| Submit   | 1         | Submits form data.                        |
| Reset    | 2         | Resets form inputs.                       |

### BitLabelPosition

| **Name** | **Value** | **Description**                                  |
|----------|-----------|--------------------------------------------------|
| Top      | 0         | Label appears at the top of the button.          |
| End      | 1         | Label appears at the end of the button.          |
| Bottom   | 2         | Label appears at the bottom of the button.       |
| Start    | 3         | Label appears at the start of the button.        |

### BitLinkRel

| **Name**       | **Value** | **Description**                                                                                       |
|----------------|-----------|-------------------------------------------------------------------------------------------------------|
| Alternate      | 1         | Provides an alternate representation of the document (e.g., print version).                           |
| Author         | 2         | Links to the author of the document.                                                                  |
| Bookmark       | 4         | A permanent URL for bookmarking.                                                                      |
| External       | 8         | Indicates the link is to an external site.                                                            |
| Help           | 16        | Provides a link to a help document.                                                                   |
| License        | 32        | Provides a link to licensing information.                                                             |
| Next           | 64        | Points to the next document in a series.                                                              |
| NoFollow       | 128       | Instructs search engines not to follow the link.                                                      |
| NoOpener       | 256       | Prevents the new browsing context from accessing the originating window.                             |
| NoReferrer     | 512       | Omits the referrer header when the link is clicked.                                                   |
| Prev           | 1024      | Points to the previous document in a series.                                                        |
| Search         | 2048      | Links to a search tool for the document.                                                            |
| Tag            | 4096      | Provides a tag (keyword) for the document.                                                          |

### BitPosition

| **Name**       | **Value** | **Description**              |
|----------------|-----------|------------------------------|
| TopLeft        | 0         | Positioned at the top left.  |
| TopCenter      | 1         | Positioned at the top center.|
| TopRight       | 2         | Positioned at the top right. |
| CenterLeft     | 3         | Positioned at the center left.|
| Center         | 4         | Centered.                    |
| CenterRight    | 5         | Positioned at the center right.|
| BottomLeft     | 6         | Positioned at the bottom left.|
| BottomCenter   | 7         | Positioned at the bottom center.|
| BottomRight    | 8         | Positioned at the bottom right.|

### BitVisibility

| **Name**  | **Value** | **Description**                                        |
|-----------|-----------|--------------------------------------------------------|
| Visible   | 0         | Component is visible.                                  |
| Hidden    | 1         | Component is hidden (using `visibility: hidden`) but occupies space. |
| Collapsed | 2         | Component is removed from the layout (using `display: none`).        |

### BitDir

| **Name** | **Value** | **Description**                                                              |
|----------|-----------|------------------------------------------------------------------------------|
| Ltr      | 0         | Left-to-right text direction (e.g., English).                                |
| Rtl      | 1         | Right-to-left text direction (e.g., Arabic).                                 |
| Auto     | 2         | Automatically determine direction based on content.                        |

---