# Icon Component Documentation

This document serves as a complete reference for the **Icon** component. The Icon component is used to represent a concept or meaning through a visual symbol. It improves user experience by providing intuitive, user-friendly applications. This file details the component's purpose, usage examples, API parameters, available enumerations, and feedback options.

---

## Overview

The **Icon** component is designed to visually communicate ideas or actions. It is highly customizable with respect to its color, size, variant, style, and additional HTML attributes. Icons are used throughout the Bit BlazorUI framework to enhance the overall user interface and user experience.

---

## Usage

The Icon component can be used in different ways depending on your needs. Below are several usage examples.

### Basic Usage

The basic usage shows how to display icons using default settings. For instance, you might render several icons with primary styling, and also demonstrate a disabled state:

```html
<!-- Basic Icon examples -->
<i role="img" class="bit-ico bit-ico-pri bit-icon bit-icon--Accept bit-ico-md bit-ico-txt"></i>
&nbsp;
<i role="img" class="bit-ico bit-ico-pri bit-icon bit-icon--Bus bit-ico-md bit-ico-txt"></i>
&nbsp;
<i role="img" class="bit-ico bit-ico-pri bit-icon bit-icon--Pinned bit-ico-md bit-ico-txt"></i>
<br/><br/>
<div>Disabled</div>
<br/>
<i role="img" class="bit-ico bit-dis bit-ico-pri bit-icon bit-icon--Accept bit-ico-md bit-ico-txt"></i>
&nbsp;
<i role="img" class="bit-ico bit-dis bit-ico-pri bit-icon bit-icon--Bus bit-ico-md bit-ico-txt"></i>
&nbsp;
<i role="img" class="bit-ico bit-dis bit-ico-pri bit-icon bit-icon--Pinned bit-ico-md bit-ico-txt"></i>
```

### Variant

Icons can adopt different visual variants. The following example shows how to use the Fill, Outline, and Text (default) variants:

```html
<!-- Variant Examples -->
<div>Fill</div>
<br/>
<i role="img" class="bit-ico bit-ico-pri bit-icon bit-icon--Accept bit-ico-md bit-ico-fil"></i>
<br/><br/>
<div>Outline</div>
<br/>
<i role="img" class="bit-ico bit-ico-pri bit-icon bit-icon--Accept bit-ico-md bit-ico-out"></i>
<br/><br/>
<div>Text (default)</div>
<br/>
<i role="img" class="bit-ico bit-ico-pri bit-icon bit-icon--Accept bit-ico-md bit-ico-txt"></i>
```

### Size

Icons can be displayed in multiple sizes. This example demonstrates small, medium, and large icon sizes:

```html
<!-- Size Examples -->
<div>Small</div>
<br/>
<i role="img" class="bit-ico bit-ico-pri bit-icon bit-icon--Accept bit-ico-sm bit-ico-txt"></i>
&nbsp;
<i role="img" class="bit-ico bit-ico-pri bit-icon bit-icon--Bus bit-ico-sm bit-ico-txt"></i>
&nbsp;
<i role="img" class="bit-ico bit-ico-pri bit-icon bit-icon--Pinned bit-ico-sm bit-ico-txt"></i>
<br/><br/>
<div>Medium</div>
<br/>
<i role="img" class="bit-ico bit-ico-pri bit-icon bit-icon--Accept bit-ico-md bit-ico-txt"></i>
&nbsp;
<i role="img" class="bit-ico bit-ico-pri bit-icon bit-icon--Bus bit-ico-md bit-ico-txt"></i>
&nbsp;
<i role="img" class="bit-ico bit-ico-pri bit-icon bit-icon--Pinned bit-ico-md bit-ico-txt"></i>
<br/><br/>
<div>Large</div>
<br/>
<i role="img" class="bit-ico bit-ico-pri bit-icon bit-icon--Accept bit-ico-lg bit-ico-txt"></i>
&nbsp;
<i role="img" class="bit-ico bit-ico-pri bit-icon bit-icon--Bus bit-ico-lg bit-ico-txt"></i>
&nbsp;
<i role="img" class="bit-ico bit-ico-pri bit-icon bit-icon--Pinned bit-ico-lg bit-ico-txt"></i>
```

### Color

A wide range of color variants is available to provide visual cues corresponding to specific actions or states. The following examples show different color variants:

```html
<!-- Color Examples -->
<div>Primary</div>
<br/>
<i role="img" class="bit-ico bit-ico-pri bit-icon bit-icon--Accept bit-ico-md bit-ico-txt"></i>
&nbsp;
<i role="img" class="bit-ico bit-ico-pri bit-icon bit-icon--Bus bit-ico-md bit-ico-txt"></i>
&nbsp;
<i role="img" class="bit-ico bit-ico-pri bit-icon bit-icon--Pinned bit-ico-md bit-ico-txt"></i>
<br/><br/>
<div>Secondary</div>
<br/>
<i role="img" class="bit-ico bit-ico-sec bit-icon bit-icon--Accept bit-ico-md bit-ico-txt"></i>
&nbsp;
<i role="img" class="bit-ico bit-ico-sec bit-icon bit-icon--Bus bit-ico-md bit-ico-txt"></i>
&nbsp;
<i role="img" class="bit-ico bit-ico-sec bit-icon bit-icon--Pinned bit-ico-md bit-ico-txt"></i>
<br/><br/>
<div>Tertiary</div>
<br/>
<i role="img" class="bit-ico bit-ico-ter bit-icon bit-icon--Accept bit-ico-md bit-ico-txt"></i>
&nbsp;
<i role="img" class="bit-ico bit-ico-ter bit-icon bit-icon--Bus bit-ico-md bit-ico-txt"></i>
&nbsp;
<i role="img" class="bit-ico bit-ico-ter bit-icon bit-icon--Pinned bit-ico-md bit-ico-txt"></i>
<br/><br/>
<div>Info</div>
<br/>
<i role="img" class="bit-ico bit-ico-inf bit-icon bit-icon--Accept bit-ico-md bit-ico-txt"></i>
&nbsp;
<i role="img" class="bit-ico bit-ico-inf bit-icon bit-icon--Bus bit-ico-md bit-ico-txt"></i>
&nbsp;
<i role="img" class="bit-ico bit-ico-inf bit-icon bit-icon--Pinned bit-ico-md bit-ico-txt"></i>
<br/><br/>
<div>Success</div>
<br/>
<i role="img" class="bit-ico bit-ico-suc bit-icon bit-icon--Accept bit-ico-md bit-ico-txt"></i>
&nbsp;
<i role="img" class="bit-ico bit-ico-suc bit-icon bit-icon--Bus bit-ico-md bit-ico-txt"></i>
&nbsp;
<i role="img" class="bit-ico bit-ico-suc bit-icon bit-icon--Pinned bit-ico-md bit-ico-txt"></i>
<br/><br/>
<div>Warning</div>
<br/>
<i role="img" class="bit-ico bit-ico-wrn bit-icon bit-icon--Accept bit-ico-md bit-ico-txt"></i>
&nbsp;
<i role="img" class="bit-ico bit-ico-wrn bit-icon bit-icon--Bus bit-ico-md bit-ico-txt"></i>
&nbsp;
<i role="img" class="bit-ico bit-ico-wrn bit-icon bit-icon--Pinned bit-ico-md bit-ico-txt"></i>
<br/><br/>
<div>SevereWarning</div>
<br/>
<i role="img" class="bit-ico bit-ico-swr bit-icon bit-icon--Accept bit-ico-md bit-ico-txt"></i>
&nbsp;
<i role="img" class="bit-ico bit-ico-swr bit-icon bit-icon--Bus bit-ico-md bit-ico-txt"></i>
&nbsp;
<i role="img" class="bit-ico bit-ico-swr bit-icon bit-icon--Pinned bit-ico-md bit-ico-txt"></i>
<br/><br/>
<div>Error</div>
<br/>
<i role="img" class="bit-ico bit-ico-err bit-icon bit-icon--Accept bit-ico-md bit-ico-txt"></i>
&nbsp;
<i role="img" class="bit-ico bit-ico-err bit-icon bit-icon--Bus bit-ico-md bit-ico-txt"></i>
&nbsp;
<i role="img" class="bit-ico bit-ico-err bit-icon bit-icon--Pinned bit-ico-md bit-ico-txt"></i>
```

### Style & Class

You can customize the Icon component further by applying custom CSS styles or classes.

```html
<!-- Style & Class Examples -->
<div>
  <!-- Icon with inline style -->
  <i role="img" style="background-color: brown; border-radius: 4px"
     class="bit-ico bit-ico-pri bit-icon bit-icon--Accept bit-ico-lg bit-ico-txt"></i>
  <!-- Icon with a custom CSS class -->
  <i role="img" class="bit-ico bit-ico-pri bit-icon bit-icon--Accept bit-ico-md bit-ico-txt icon-class"></i>
</div>
```

---

## API

The Icon component API is split into two sections: **BitIcon parameters** and **BitComponentBase parameters**.

### BitIcon Parameters

| **Name**   | **Type**        | **Default Value** | **Description**                                         |
| ---------- | --------------- | ----------------- | ------------------------------------------------------- |
| Color      | `BitColor?`     | `null`            | The general color of the icon.                        |
| IconName   | `string`        | *None*            | The icon name to be displayed.                        |
| Size       | `BitSize?`      | `null`            | The size of the icon.                                   |
| Variant    | `BitVariant?`   | `null`            | The visual variant of the icon (Fill, Outline, Text).   |

### BitComponentBase Parameters

| **Name**         | **Type**                      | **Default Value**                        | **Description**                                                                                   |
| ---------------- | ----------------------------- | ---------------------------------------- | ------------------------------------------------------------------------------------------------- |
| AriaLabel        | `string?`                     | `null`                                   | The aria-label of the control for screen readers.                                               |
| Class            | `string?`                     | `null`                                   | Custom CSS class for the root element.                                                          |
| Dir              | `BitDir?`                     | `null`                                   | Determines the component direction (e.g., Ltr, Rtl, Auto).                                      |
| HtmlAttributes   | `Dictionary<string, object>`  | `new Dictionary<string, object>()`       | Additional attributes to render on the root element.                                            |
| Id               | `string?`                     | `null`                                   | Custom id for the root element. If `null`, a unique id will be generated.                        |
| IsEnabled        | `bool`                        | `true`                                   | Indicates whether the component is enabled.                                                     |
| Style            | `string?`                     | `null`                                   | Custom CSS style for the root element.                                                          |
| Visibility       | `BitVisibility`               | `BitVisibility.Visible`                  | Controls whether the component is visible, hidden, or collapsed.                                |

### BitComponentBase Public Members

| **Name**    | **Type**            | **Default Value**      | **Description**                                                                              |
| ----------- | ------------------- | ---------------------- | -------------------------------------------------------------------------------------------- |
| UniqueId    | `Guid`              | `Guid.NewGuid()`       | A read-only unique identifier for the component instance.                                    |
| RootElement | `ElementReference`  | *(none)*               | The reference to the root HTML element of the component.                                     |

---

## Enums

### BitColor Enum

| **Name**              | **Value** | **Description**                     |
| --------------------- | --------- | ----------------------------------- |
| Primary               | `0`       | Info Primary general color.         |
| Secondary             | `1`       | Secondary general color.            |
| Tertiary              | `2`       | Tertiary general color.             |
| Info                  | `3`       | Info general color.                 |
| Success               | `4`       | Success general color.              |
| Warning               | `5`       | Warning general color.              |
| SevereWarning         | `6`       | SevereWarning general color.        |
| Error                 | `7`       | Error general color.                |
| PrimaryBackground     | `8`       | Primary background color.           |
| SecondaryBackground   | `9`       | Secondary background color.         |
| TertiaryBackground    | `10`      | Tertiary background color.          |
| PrimaryForeground     | `11`      | Primary foreground color.           |
| SecondaryForeground   | `12`      | Secondary foreground color.         |
| TertiaryForeground    | `13`      | Tertiary foreground color.          |
| PrimaryBorder         | `14`      | Primary border color.               |
| SecondaryBorder       | `15`      | Secondary border color.             |
| TertiaryBorder        | `16`      | Tertiary border color.              |

### BitSize Enum

| **Name**  | **Value** | **Description**                      |
| --------- | --------- | ------------------------------------ |
| Small     | `0`       | Display icon using small size.       |
| Medium    | `1`       | Display icon using medium size.      |
| Large     | `2`       | Display icon using large size.       |

### BitVariant Enum

| **Name**  | **Value** | **Description**                      |
| --------- | --------- | ------------------------------------ |
| Fill      | `0`       | Fill styled variant.                 |
| Outline   | `1`       | Outline styled variant.              |
| Text      | `2`       | Text styled variant. (Default)       |

### BitVisibility Enum

| **Name**    | **Value** | **Description**                                                      |
| ----------- | --------- | -------------------------------------------------------------------- |
| Visible     | `0`       | The component is visible.                                            |
| Hidden      | `1`       | The component is hidden but occupies space (using `visibility:hidden`).|
| Collapsed   | `2`       | The component is hidden and does not occupy space (`display:none`).    |

### BitDir Enum

| **Name** | **Value** | **Description**                                                                                  |
| -------- | --------- | ------------------------------------------------------------------------------------------------ |
| Ltr      | `0`       | Left-to-right direction for languages such as English.                                           |
| Rtl      | `1`       | Right-to-left direction for languages such as Arabic.                                            |
| Auto     | `2`       | Automatically determines direction based on the content's dominant directionality.                |

---

## Explanation for AI Agent Usage

This Markdown file is intended as a detailed reference for the **Icon** component. An AI agent using this file should be able to:

- **Understand Component Purpose:**  
  Recognize that the Icon component is designed to visually represent actions or states in a user interface.

- **Generate Code Examples:**  
  Use the provided usage examples to generate similar HTML code snippets with appropriate classes and attributes for different visual variants, sizes, and color themes.

- **Extract API Metadata:**  
  Reference the API tables to understand parameter names, types, default values, and descriptions. This is useful for code generation, debugging, or dynamic documentation purposes.

- **Interpret Enumerations:**  
  Utilize the enum definitions (such as for BitColor, BitSize, BitVariant, BitVisibility, and BitDir) to manage visual and layout options in different contexts.

- **Provide Feedback Links:**  
  Direct users to the GitHub pages for reporting issues, reviewing source code, or suggesting improvements.

This comprehensive documentation is designed to empower both human developers and automated systems to effectively work with and extend the Icon component within the Bit BlazorUI framework.

---