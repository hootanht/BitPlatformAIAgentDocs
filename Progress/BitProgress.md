# Bit Blazor UI Progress Component (`BitProgress`)

**Version:** (Based on the provided HTML snapshot)
**Purpose:** This document provides a reference guide for using the `BitProgress` component (which functions as both a linear ProgressBar and a circular ProgressIndicator) in the Bit Blazor UI library. It covers basic usage, different modes (linear, circular, indeterminate), customization options (labels, descriptions, colors, thickness, styling), and includes detailed API information.

---

## Overview

The `BitProgress` component is used to visually represent the completion status of an operation or task. It can be displayed as a standard linear progress bar or as a circular progress indicator. It supports both determinate (showing a specific percentage) and indeterminate (showing activity without a known completion percentage) states.

---

## Usage Examples

Below are examples demonstrating how to use and customize the `BitProgress` component.

### 1. Basic Linear Progress

Displays a standard linear progress bar with a label, description, and a specific percentage complete.

```cshtml
<BitProgress Label="Basic Progress"
             Description="Example description"
             Percent="42" />
```

*(Note: Renders a horizontal bar filled to 42%, with the label "Basic Progress" above and "Example description" below.)*

### 2. Circular Progress

Use the `Circular` attribute to render the progress indicator as a circle.

```cshtml
<BitProgress Circular
             Label="Basic Circular Progress"
             Description="Example description"
             Percent="42" />
```

*(Note: Renders a circular track with an arc filled to 42%, with the label and description positioned similarly to the linear version.)*

### 3. Showing the Percentage Number (`ShowPercentNumber`)

Display the numerical percentage value alongside the indicator using the `ShowPercentNumber` attribute. You can format this number using `PercentNumberFormat`.

```cshtml
@* Default formatting (rounds to nearest integer) *@
<BitProgress Label="Show Percent Number"
             Percent="85.69"
             ShowPercentNumber />

@* Custom formatting (two decimal places) *@
<BitProgress Label="Percent Number Format"
             Percent="85.69"
             PercentNumberFormat="{0:F2} %"
             ShowPercentNumber />

@* Circular with default formatting *@
<BitProgress Circular
             Label="Show Percent Number"
             Percent="85.69"
             ShowPercentNumber />

@* Circular with custom formatting *@
<BitProgress Circular
             Label="Percent Number Format"
             Percent="85.69"
             PercentNumberFormat="{0:F2} %"
             ShowPercentNumber />
```

*(Note: Renders progress indicators (linear and circular) showing the percentage value text (e.g., "86 %" or "85.69 %") near the indicator.)*

### 4. Adjusting Thickness (`Thickness`)

Control the thickness (height of the linear bar or stroke width of the circular indicator) using the `Thickness` parameter (value in pixels). The `Radius` parameter specifically controls the size of the circular indicator.

```csharp
@page "/progress"
@using Microsoft.AspNetCore.Components.Web

<BitSlider @bind-Value="barThickness" Max="50" Min="1" />
<br /><br />

<BitProgress ShowPercentNumber Percent="69" Thickness="(int)barThickness" />
<br />

<BitProgress Circular ShowPercentNumber Percent="69" Thickness="(int)barThickness" Radius="30" /> @* Example: Fixed radius *@

@code {
    private double barThickness = 10;
}
```

*(Note: Shows a slider controlling the `Thickness` variable. The linear progress bar's height changes, and the circular progress's stroke width changes. The `Radius` parameter would be used to change the overall diameter of the circular progress.)*

### 5. Indeterminate Progress (`Indeterminate`)

Use the `Indeterminate` attribute when the progress percentage is unknown. This displays an animation indicating activity. `Percent` is ignored in this mode.

```cshtml
@* Linear Indeterminate *@
<BitProgress Indeterminate />
<br />

@* Circular Indeterminate *@
<BitProgress Circular Indeterminate />
```

*(Note: Renders animating linear and circular indicators without showing a specific percentage fill.)*

### 6. Setting Color (`Color`)

You can specify a custom color for the progress bar/indicator using the `Color` parameter, providing a valid CSS color string.

```cshtml
@* Determinate Linear with custom color *@
<BitProgress Color="#c10606" Percent="69" />
<br />

@* Indeterminate Linear with custom color *@
<BitProgress Color="#ffba17" Indeterminate />
<br /><br />

@* Determinate Circular with custom color *@
<BitProgress Color="#c10606" Circular Percent="69" />
<br />

@* Indeterminate Circular with custom color *@
<BitProgress Color="#ffba17" Circular Indeterminate />
```

*(Note: Renders progress indicators using the specified hex colors for the filled/active portion.)*

### 7. Custom Styling (`Style`, `Class`, `Styles`, `Classes`)

Apply custom styles and classes to the component:

* `Style` / `Class`: Apply directly to the root element of the component.
* `Styles` / `Classes`: Target specific internal elements (like the bar, track, label) using the `BitProgressClassStyles` object.

```css
/* Example CSS */
.custom-root-class {
    padding: 0.2rem;
    margin-bottom: 1rem;
    border-radius: 0.5rem;
    background-color: midnightblue; /* Applied to root */
}

.custom-track {
    background-color: #ffae00 !important; /* Style linear track */
}

.custom-bar {
    background-image: linear-gradient(45deg, #ff2700, #ff6a00) !important; /* Style linear bar */
}

.custom-circle-track {
    stroke: #ffae00 !important; /* Style circular track */
}

.custom-circle-bar {
    stroke: url(#gradient) #ff2700 !important; /* Style circular bar - gradient needs SVG def */
}

.custom-label {
    color: cyan !important;
}
```

```cshtml
@* Define SVG gradient if needed for circular bar styling *@
<svg width="0" height="0">
  <defs>
    <linearGradient id="gradient" x1="0%" y1="0%" x2="100%" y2="0%">
      <stop offset="0%" style="stop-color:#ff2700;" />
      <stop offset="100%" style="stop-color:#ff6a00;" />
    </linearGradient>
  </defs>
</svg>

@* Inline style on root *@
<BitProgress Indeterminate Style="background-color: #e687dc; border-radius: 0.5rem; padding: 0.2rem;" Thickness="10" />
<br />

@* CSS class on root *@
<BitProgress Class="custom-root-class" Percent="69" Thickness="10" />
<br />

@* Targeting internal elements with Styles (inline) *@
<BitProgress Indeterminate Thickness="10"
             Styles="@(new() { Bar = "background: linear-gradient(to right, green 0%, yellow 50%, green 100%);",
                              Track = "background-color: darkgreen;" })" />
<br />

@* Targeting internal elements with Classes (CSS) *@
<BitProgress Percent="69" Thickness="10"
             Classes="@(new() { Bar = "custom-bar", Track = "custom-track", Label = "custom-label" })"
             Label="Styled Label" />
<br />

@* --- Circular Examples --- *@

@* Circular with inline style on root *@
<BitProgress Circular Indeterminate Style="background-color: #e687dc; border-radius: 50%; padding: 0.5rem; display: inline-block;" Radius="30" Thickness="5" />
<br />

@* Circular with CSS class on root *@
<BitProgress Circular Class="custom-root-class" Percent="69" Radius="30" Thickness="5" />
<br />

@* Circular targeting internal elements with Styles (inline) *@
<BitProgress Circular Indeterminate Radius="30" Thickness="5"
             Styles="@(new() { Bar = "stroke: greenyellow;", Track = "stroke: darkgreen;" })" />
<br />

@* Circular targeting internal elements with Classes (CSS) *@
<BitProgress Circular Percent="69" Radius="30" Thickness="5"
             Classes="@(new() { Bar = "custom-circle-bar", Track = "custom-circle-track", Label = "custom-label" })"
             Label="Styled Label" />

```

*(Note: Demonstrates various ways to apply custom appearances using inline styles, CSS classes applied to the root, and specific styles/classes targeting the internal track and bar elements for both linear and circular types.)*

### 8. Right-to-Left (`Dir`)

Set the component's directionality for RTL languages using `Dir="BitDir.Rtl"`.

```cshtml
@* Indeterminate RTL *@
<BitProgress Dir="BitDir.Rtl"
             Thickness="10"
             Indeterminate />
<br />

@* Determinate RTL with Persian text *@
<BitProgress Label="لیبل تست"
             Description="توضیحات تست"
             Dir="BitDir.Rtl"
             Percent="69"
             Thickness="10"
             ShowPercentNumber /> @* Corrected: ShowPercentNumber used in HTML, not ShowPercent *@
```

*(Note: Renders the progress indicators with layout and text direction appropriate for RTL languages. The indeterminate animation might also reverse direction.)*

---

## API Reference

### `BitProgress` Parameters

| Name                | Type                         | Default Value | Description                                                                                           |
| :------------------ | :--------------------------- | :------------ | :---------------------------------------------------------------------------------------------------- |
| `AriaValueText`     | `string?`                    | `null`        | Text alternative of the progress status, used by screen readers for reading the value of the progress. |
| `Classes`           | `BitProgressClassStyles?`    | `null`        | Custom CSS classes for different internal parts of the BitProgress (uses `BitProgressClassStyles`).   |
| `Color`             | `string?`                    | `null`        | Custom CSS color string for the progress bar/indicator.                                               |
| `Circular`          | `bool`                       | `false`       | Renders the component as a circular indicator instead of a linear bar.                                |
| `Description`       | `string?`                    | `null`        | Text displayed below the indicator to supplement the operation status.                                |
| `DescriptionTemplate`| `RenderFragment?`          | `null`        | Custom Razor content for the description area (overrides `Description`).                                |
| `Indeterminate`     | `bool`                       | `false`       | Displays an indeterminate animation when progress percentage is unknown. Ignores `Percent`.           |
| `Label`             | `string?`                    | `null`        | Text displayed above the indicator.                                                                   |
| `LabelTemplate`     | `RenderFragment?`          | `null`        | Custom Razor content for the label area (overrides `Label`).                                          |
| `Percent`           | `double`                     | `0`           | Percentage of completion (0-100). Used only when `Indeterminate` is `false`.                          |
| `PercentNumberFormat`| `string`                   | `"{0:F0} %"`  | The .NET format string used to display the percentage when `ShowPercentNumber` is true.               |
| `Radius`            | `int`                        | `6`           | The radius (in pixels) of the circular progress indicator. Only applies when `Circular` is true.      |
| `ShowPercentNumber` | `bool`                       | `false`       | Whether to display the numerical percentage value.                                                    |
| `Styles`            | `BitProgressClassStyles?`    | `null`        | Custom inline CSS styles for different internal parts of the BitProgress (uses `BitProgressClassStyles`). |
| `Thickness`         | `int`                        | `2`           | Thickness (in pixels) of the progress bar (height) or circular indicator stroke.                    |

### `BitComponentBase` Parameters (Inherited)

These parameters are common to all Bit Blazor UI components.

| Name           | Type                            | Default Value                        | Description                                                                                     |
| :------------- | :------------------------------ | :----------------------------------- | :---------------------------------------------------------------------------------------------- |
| `AriaLabel`    | `string?`                       | `null`                               | The `aria-label` attribute for accessibility.                                                   |
| `Class`        | `string?`                       | `null`                               | Custom CSS class(es) to apply to the root element.                                              |
| `Dir`          | `BitDir?`                       | `null`                               | Sets the component's text direction (LTR/RTL/Auto) using the `BitDir` enum.                   |
| `HtmlAttributes`| `Dictionary<string, object>`  | `new Dictionary<string, object>()` | Captures and renders additional HTML attributes on the root element.                              |
| `Id`           | `string?`                       | `null`                               | Custom `id` attribute for the root element. If `null`, a unique ID (`UniqueId`) is generated. |
| `IsEnabled`    | `bool`                          | `true`                               | Whether the component is visually/functionally enabled.                                         |
| `Style`        | `string?`                       | `null`                               | Custom inline CSS styles to apply to the root element.                                          |
| `Visibility`   | `BitVisibility`                 | `BitVisibility.Visible`              | Controls the component's visibility (`Visible`, `Hidden`, `Collapsed`) using the `BitVisibility` enum. |

### `BitComponentBase` Public Members (Inherited)

| Name          | Type               | Default Value      | Description                                                                               |
| :------------ | :----------------- | :----------------- | :---------------------------------------------------------------------------------------- |
| `UniqueId`    | `Guid`             | `Guid.NewGuid()`   | A read-only unique identifier generated for the component instance upon construction.      |
| `RootElement` | `ElementReference` | *(N/A)*            | Provides a reference to the component's root HTML element (useful for JavaScript interop). |

---

## Supporting Types

### `BitProgressClassStyles` Class

Used by the `Styles` and `Classes` parameters to target specific elements within the `BitProgress` component.

| Property       | Type      | Description                                            |
| :------------- | :-------- | :----------------------------------------------------- |
| `Root`         | `string?` | Styles/classes for the root container element.         |
| `Label`        | `string?` | Styles/classes for the label element.                  |
| `PercentNumber`| `string?` | Styles/classes for the percentage number text element. |
| `BarContainer` | `string?` | Styles/classes for the container holding the bar/track. |
| `Track`        | `string?` | Styles/classes for the background track element.       |
| `Bar`          | `string?` | Styles/classes for the progress bar/indicator element. |
| `Description`  | `string?` | Styles/classes for the description text element.       |

### `BitVisibility` Enum

Controls the component's rendering and visibility.

| Name      | Value | Description                                                         |
| :-------- | :---- | :------------------------------------------------------------------ |
| `Visible` | `0`   | Component is rendered and visible.                                |
| `Hidden`  | `1`   | Component is hidden (`visibility: hidden`), but preserves space. |
| `Collapsed`| `2`   | Component is not rendered (`display: none`), consumes no space.    |

### `BitDir` Enum

Controls the component's text and layout direction.

| Name | Value | Description                                                   |
| :--- | :---- | :------------------------------------------------------------ |
| `Ltr`| `0`   | Left-to-right direction (e.g., English).                    |
| `Rtl`| `1`   | Right-to-left direction (e.g., Arabic, Hebrew).             |
| `Auto`| `2`   | Browser automatically determines direction based on content. |

---

## Feedback & Source Code

* **Report Issues:** [File an Issue on GitHub](https://github.com/bitfoundation/bitplatform/issues/new/choose)
* **Start Discussions:** [Start a Discussion on GitHub](https://github.com/bitfoundation/bitplatform/discussions/new/choose)
* **View/Edit Page Source:** [Progress Demo Page Source](https://github.com/bitfoundation/bitplatform/blob/develop/src/BlazorUI/Demo/Client/Bit.BlazorUI.Demo.Client.Core/Pages/Components/Progress/Progress/BitProgressDemo.razor)
* **View/Edit Component Source:** [BitProgress Component Source](https://github.com/bitfoundation/bitplatform/blob/develop/src/BlazorUI/Bit.BlazorUI/Components/Progress/Progress/BitProgress.razor)