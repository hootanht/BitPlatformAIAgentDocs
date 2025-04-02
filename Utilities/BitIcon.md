# BitIcon Component 

**Purpose:** This document provides a detailed reference for the `BitIcon` Blazor UI component. It is intended to be used by an AI agent (like GitHub Copilot, Cursor, etc.) to understand the component's functionality, usage patterns, and API, enabling the agent to provide accurate code suggestions and assistance related to `BitIcon`.

**Source:** This information is derived from the Bit Blazor UI documentation for the `BitIcon` component.

---

## Overview

*   **Component:** `BitIcon`
*   **Purpose:** Renders an icon element (typically an `<i>` tag with appropriate classes) to visually represent concepts, actions, or objects, enhancing user experience and application clarity. It utilizes a predefined set of icons available through the `BitIconName` static class.
*   **Library:** Bit Blazor UI (`Bit.BlazorUI`)

---

## Usage Examples

### 1. Basic Usage

To display an icon, use the `BitIcon` component and specify the desired icon using the `IconName` parameter, referencing constants from the `BitIconName` static class. The `IsEnabled` parameter can be used to render the icon in a disabled state.

```cshtml
@* Enabled Icons *@
<BitIcon IconName="@BitIconName.Accept" />
<BitIcon IconName="@BitIconName.Bus" />
<BitIcon IconName="@BitIconName.Pinned" />

<br /><br />
<div>Disabled</div>
@* Disabled Icons *@
<BitIcon IconName="@BitIconName.Accept" IsEnabled="false" />
<BitIcon IconName="@BitIconName.Bus" IsEnabled="false" />
<BitIcon IconName="@BitIconName.Pinned" IsEnabled="false" />
```

* **Note:** A list of available `BitIconName` constants can typically be found in the Bit Blazor UI documentation or explored via IntelliSense.

### 2. Variant

The `Variant` parameter controls the visual style of the icon (Fill, Outline, or Text) using the `BitVariant` enum. The default is `BitVariant.Text`.

```cshtml
@* Fill Variant *@
<BitIcon IconName="@BitIconName.Accept" Variant="BitVariant.Fill" />
<br /><br />

@* Outline Variant *@
<BitIcon IconName="@BitIconName.Accept" Variant="BitVariant.Outline" />
<br /><br />

@* Text Variant (Default) *@
<BitIcon IconName="@BitIconName.Accept" Variant="BitVariant.Text" /> @* Or simply <BitIcon IconName="@BitIconName.Accept" /> *@
```

### 3. Size

Adjust the icon size using the `Size` parameter with values from the `BitSize` enum (`Small`, `Medium`, `Large`). The default size is typically `Medium`.

```cshtml
@* Small Size *@
<BitIcon Size="BitSize.Small" IconName="@BitIconName.Accept" />
<BitIcon Size="BitSize.Small" IconName="@BitIconName.Bus" />
<BitIcon Size="BitSize.Small" IconName="@BitIconName.Pinned" />
<br /><br />

@* Medium Size (Default) *@
<BitIcon Size="BitSize.Medium" IconName="@BitIconName.Accept" />
<BitIcon Size="BitSize.Medium" IconName="@BitIconName.Bus" />
<BitIcon Size="BitSize.Medium" IconName="@BitIconName.Pinned" />
<br /><br />

@* Large Size *@
<BitIcon Size="BitSize.Large" IconName="@BitIconName.Accept" />
<BitIcon Size="BitSize.Large" IconName="@BitIconName.Bus" />
<BitIcon Size="BitSize.Large" IconName="@BitIconName.Pinned" />
```

### 4. Color

Apply semantic colors to the icon using the `Color` parameter with values from the `BitColor` enum. This helps convey meaning (e.g., success, error, warning).

```cshtml
@* Primary Color *@
<BitIcon Color="BitColor.Primary" IconName="@BitIconName.Accept" />
<BitIcon Color="BitColor.Primary" IconName="@BitIconName.Bus" />
<BitIcon Color="BitColor.Primary" IconName="@BitIconName.Pinned" />
<br /><br />

@* Secondary Color *@
<BitIcon Color="BitColor.Secondary" IconName="@BitIconName.Accept" />
<BitIcon Color="BitColor.Secondary" IconName="@BitIconName.Bus" />
<BitIcon Color="BitColor.Secondary" IconName="@BitIconName.Pinned" />
<br /><br />

@* Tertiary Color *@
<BitIcon Color="BitColor.Tertiary" IconName="@BitIconName.Accept" />
<BitIcon Color="BitColor.Tertiary" IconName="@BitIconName.Bus" />
<BitIcon Color="BitColor.Tertiary" IconName="@BitIconName.Pinned" />
<br /><br />

@* Info Color *@
<BitIcon Color="BitColor.Info" IconName="@BitIconName.Accept" />
<BitIcon Color="BitColor.Info" IconName="@BitIconName.Bus" />
<BitIcon Color="BitColor.Info" IconName="@BitIconName.Pinned" />
<br /><br />

@* Success Color *@
<BitIcon Color="BitColor.Success" IconName="@BitIconName.Accept" />
<BitIcon Color="BitColor.Success" IconName="@BitIconName.Bus" />
<BitIcon Color="BitColor.Success" IconName="@BitIconName.Pinned" />
<br /><br />

@* Warning Color *@
<BitIcon Color="BitColor.Warning" IconName="@BitIconName.Accept" />
<BitIcon Color="BitColor.Warning" IconName="@BitIconName.Bus" />
<BitIcon Color="BitColor.Warning" IconName="@BitIconName.Pinned" />
<br /><br />

@* SevereWarning Color *@
<BitIcon Color="BitColor.SevereWarning" IconName="@BitIconName.Accept" />
<BitIcon Color="BitColor.SevereWarning" IconName="@BitIconName.Bus" />
<BitIcon Color="BitColor.SevereWarning" IconName="@BitIconName.Pinned" />
<br /><br />

@* Error Color *@
<BitIcon Color="BitColor.Error" IconName="@BitIconName.Accept" />
<BitIcon Color="BitColor.Error" IconName="@BitIconName.Bus" />
<BitIcon Color="BitColor.Error" IconName="@BitIconName.Pinned" />
```

### 5. Style & Class

Apply custom inline styles using the `Style` parameter or add custom CSS classes using the `Class` parameter for fine-grained control over the icon's appearance.

```cshtml
<style>
    .icon-class {
        padding: 4px;
        font-size: 3rem; /* Overrides default size */
        margin-left: 1rem;
        background-color: aquamarine;
        color: darkblue; /* Overrides default color */
        border-radius: 50%;
    }
</style>

@* Applying inline style *@
<BitIcon IconName="@BitIconName.Accept" Size="BitSize.Large"
         Style="background-color: brown; border-radius: 4px; color: white; padding: 2px;" />

@* Applying a custom CSS class *@
<BitIcon IconName="@BitIconName.Accept" Class="icon-class" />
```

---

## API Reference

### `BitIcon` Parameters

| Name     | Type         | Default Value | Description                                 |
| :------- | :----------- | :------------ | :------------------------------------------ |
| `Color`  | `BitColor?`  | `null`        | The semantic color of the icon.             |
| `IconName`| `string`     | *Required*    | The name of the icon to display (from `BitIconName`). |
| `Size`   | `BitSize?`   | `null` (Medium) | The size of the icon (`Small`, `Medium`, `Large`). |
| `Variant`| `BitVariant?`| `null` (Text)   | The visual variant (`Fill`, `Outline`, `Text`). |

### Inherited Parameters (`BitComponentBase`)

These parameters provide common functionality inherited from the base class.

| Name             | Type                          | Default Value              | Description                                                                                    |
| :--------------- | :---------------------------- | :------------------------- | :--------------------------------------------------------------------------------------------- |
| `AriaLabel`      | `string?`                     | `null`                     | Provides an accessible label for screen readers, especially for non-decorative icons.        |
| `Class`          | `string?`                     | `null`                     | Custom CSS class(es) applied to the root `<i>` element.                                       |
| `Dir`            | `BitDir?`                     | `null`                     | Sets the directionality (`Ltr`, `Rtl`, `Auto`). Useful if the icon itself implies direction. |
| `HtmlAttributes` | `Dictionary<string, object>`  | `new Dictionary<>()`       | Captures and renders additional HTML attributes (like `title`) on the root `<i>` element.     |
| `Id`             | `string?`                     | `null`                     | Custom `id` attribute for the root `<i>` element. If `null`, a unique ID (`UniqueId`) is used. |
| `IsEnabled`      | `bool`                        | `true`                     | Renders the icon in a disabled visual state (typically greyed out).                          |
| `Style`          | `string?`                     | `null`                     | Custom inline CSS style(s) applied to the root `<i>` element.                                 |
| `Visibility`     | `BitVisibility`               | `BitVisibility.Visible`    | Controls the element's visibility using CSS (`Visible`, `Hidden`, `Collapsed`). See enum below. |

### Public Members (`BitComponentBase`)

These are public properties available on the component instance.

| Name          | Type               | Default Value    | Description                                                                           |
| :------------ | :----------------- | :--------------- | :------------------------------------------------------------------------------------ |
| `UniqueId`    | `string`           | `Guid.NewGuid()` | Readonly unique identifier generated for the component instance. Used if `Id` is null. |
| `RootElement` | `ElementReference` |                  | A reference to the rendered root `<i>` element (available after rendering).             |

### Supporting Enums

#### `BitColor` Enum

Used for the `Color` parameter.

| Name                | Value | Description                 |
| :------------------ | :---- | :-------------------------- |
| `Primary`           | `0`   | Primary theme color.        |
| `Secondary`         | `1`   | Secondary theme color.      |
| `Tertiary`          | `2`   | Tertiary theme color.       |
| `Info`              | `3`   | Informational color.        |
| `Success`           | `4`   | Success indication color.   |
| `Warning`           | `5`   | Warning indication color.   |
| `SevereWarning`     | `6`   | Severe warning color.       |
| `Error`             | `7`   | Error indication color.     |
| `PrimaryBackground` | `8`   | Primary background color.   |
| `SecondaryBackground`| `9`   | Secondary background color. |
| `TertiaryBackground`| `10`  | Tertiary background color.  |
| `PrimaryForeground` | `11`  | Primary foreground color.   |
| `SecondaryForeground`| `12`  | Secondary foreground color. |
| `TertiaryForeground`| `13`  | Tertiary foreground color.  |
| `PrimaryBorder`     | `14`  | Primary border color.       |
| `SecondaryBorder`   | `15`  | Secondary border color.     |
| `TertiaryBorder`    | `16`  | Tertiary border color.      |

#### `BitSize` Enum

Used for the `Size` parameter.

| Name     | Value | Description                  |
| :------- | :---- | :--------------------------- |
| `Small`  | `0`   | Renders the icon small.      |
| `Medium` | `1`   | Renders the icon medium size (default). |
| `Large`  | `2`   | Renders the icon large.      |

#### `BitVariant` Enum

Used for the `Variant` parameter.

| Name      | Value | Description                        |
| :-------- | :---- | :--------------------------------- |
| `Fill`    | `0`   | Fill styled variant (solid).       |
| `Outline` | `1`   | Outline styled variant (stroked).  |
| `Text`    | `2`   | Text styled variant (default, typically inherits text color). |

#### `BitVisibility` Enum

Used for the inherited `Visibility` parameter.

| Name        | Value | Description                                                        |
| :---------- | :---- | :----------------------------------------------------------------- |
| `Visible`   | `0`   | Element is visible (default).                                      |
| `Hidden`    | `1`   | Element is hidden (`visibility: hidden;`), still occupies space.   |
| `Collapsed` | `2`   | Element is hidden (`display: none;`), does not occupy space.       |

#### `BitDir` Enum

Used for the inherited `Dir` parameter.

| Name   | Value | Description                                     |
| :----- | :---- | :---------------------------------------------- |
| `Ltr`  | `0`   | Left-to-right text direction.                   |
| `Rtl`  | `1`   | Right-to-left text direction.                   |
| `Auto` | `2`   | Browser determines direction based on content. |

---

**End of Reference**

**Explanation of the Markdown File:**

1.  **Standard Header:** Identifies the `BitIcon` component and states the document's purpose as an AI reference.
2.  **Overview:** Provides a concise description of the icon's role in UI/UX.
3.  **Usage Examples:**
    *   Each major feature (`Basic`, `Variant`, `Size`, `Color`, `Style & Class`) is demonstrated in its own subsection (`###`).
    *   Clear explanations introduce each concept (e.g., specifying the icon name, changing visual style, adjusting size, applying color, custom styling).
    *   Relevant code examples (`cshtml`, `css`) are included in fenced blocks with language identifiers.
    *   Key parameters (`IconName`, `Variant`, `Size`, `Color`, `Style`, `Class`, `IsEnabled`) and supporting enums (`BitIconName`, `BitVariant`, `BitSize`, `BitColor`) are highlighted in the explanations or code.
    *   A note clarifies where to find the list of available `BitIconName` values.
4.  **API Reference:**
    *   Structured sections for `BitIcon` parameters, inherited `BitComponentBase` parameters, and public members use Markdown tables.
    *   Parameter details (Name, Type, Default Value, Description) are accurately transcribed from the source HTML. Default values for `Size` and `Variant` are clarified based on observed behavior (Medium, Text). The `IconName` parameter is marked as required.
    *   The `IconName` type is correctly listed as `string` per the API table, but usage typically involves the `BitIconName` static class constants.
5.  **Supporting Enums:**
    *   Dedicated tables clearly define the possible values and descriptions for all relevant enums (`BitColor`, `BitSize`, `BitVariant`, `BitVisibility`, `BitDir`) referenced in the parameters.
6.  **Formatting and Clarity:** Standard Markdown formatting (headings, code blocks, tables, backticks) ensures readability and easy parsing by AI. The structure flows logically from basic usage to more advanced customization and API details.

This format provides a comprehensive yet easy-to-digest reference for an AI agent, covering how to use the `BitIcon` component effectively with its various customization options and detailing its complete API surface.
