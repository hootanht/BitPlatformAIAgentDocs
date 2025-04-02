# BitColorPicker Component Reference (`.NET Blazor - Bit Blazor UI`)

## Overview

**Component Name:** `BitColorPicker`

The `BitColorPicker` component provides an interactive UI for selecting colors. It allows users to browse colors visually using a color spectrum (saturation/value rectangle and hue slider) and optionally adjust the alpha (transparency). It typically displays the selected color and can be bound to a string representing the color in various formats (Hex, RGB, RGBA).

## Core Concepts & Features

*   **Color Selection:** Visual selection via a saturation/value rectangle and a hue slider.
*   **Alpha Channel:** Optional alpha slider (`ShowAlphaSlider`) to control transparency.
*   **Color Preview:** Optional preview box (`ShowPreview`) displaying the currently selected color with its alpha value.
*   **Color Representation:** Works with color strings in CSS-compatible formats (e.g., `#FFFFFF`, `rgb(255,0,0)`, `rgba(255,0,0,0.5)`). The component maintains consistency with the format of the initially bound `Color` value.
*   **Data Binding:** Supports two-way binding (`@bind-Color`) to a `string` variable representing the selected color. Also provides read-only access to specific formats (`Hex`, `Rgb`, `Rgba`, `Hsv`) via component reference (`@ref`).
*   **Events:** Provides an `OnChange` event that fires when the color value changes, returning both the color string and the alpha value (`BitColorChangeEventArgs`).
*   **Customization:** Allows styling via standard `Style` and `Class` attributes, as well as detailed customization through the `Styles` and `Classes` parameters targeting internal elements.
*   **Accessibility:** Includes ARIA attributes (`role="group"`, `aria-label`, `role="slider"`) for screen reader compatibility.

## Usage Examples

Below are examples demonstrating common configurations and features of the `BitColorPicker`.

---

### Example 1: Basic Usage

Displays the default `BitColorPicker` with the color spectrum rectangle and hue slider.

```cshtml
<BitColorPicker />
```

---

### Example 2: Alpha Slider & Preview

Shows the color picker with the optional alpha (transparency) slider and the color preview box enabled.

```cshtml
<BitColorPicker ShowAlphaSlider ShowPreview />
```

---

### Example 3: Data Binding

Demonstrates binding the selected color to C# string variables using `@bind-Color`. The component respects the initial format (RGB or Hex) of the bound variable for subsequent updates. It also shows binding a value that includes alpha and interacting with it via a `BitTextField`.

```cshtml
<BitColorPicker @bind-Color="rgbColor" />
<div>Color: @rgbColor</div>

<br/>

<BitColorPicker @bind-Color="hexColor" />
<div>Color: @hexColor</div>

<br/>

<BitColorPicker @bind-Color="twoWayColor" ShowAlphaSlider ShowPreview />
<BitTextField Label="Enter Color (Hex or Rgb)" @bind-Value="twoWayColor" Style="width: 200px;" />
```

```csharp
@code {
    private string rgbColor = "rgb(255,255,255)";
    private string hexColor = "#FFFFFF";
    private string twoWayColor = "#FFFFFFAA"; // Example with alpha
}
```

*Note: The component attempts to maintain the format (Hex/RGB) of the initial `Color` value.*

---

### Example 4: Handling Change Events

Illustrates using the `OnChange` event callback to capture the selected color string and alpha value separately when the user modifies the color.

```cshtml
<BitColorPicker OnChange="v => (changedColor, changedAlpha) = v" ShowAlphaSlider />
<div>Color: @changedColor</div>
<div>Alpha: @changedAlpha</div>
```

```csharp
@code {
    private string? changedColor;
    private double changedAlpha; // Alpha is returned as a double (0.0 to 1.0)
}
```

---

### Example 5: Accessing Public API / Color Formats

Shows how to use `@ref` to get a reference to the component instance and access its public properties, which provide the current color in different formats (`Hex`, `Rgb`, `Rgba`, `Hsv`).

```cshtml
<BitColorPicker @ref="colorPickerRef" @bind-Color="boundColor" ShowAlphaSlider ShowPreview />
<div>Color: @boundColor</div>
<div>Hex: @colorPickerRef?.Hex</div>
<div>Rgb: @colorPickerRef?.Rgb</div>
<div>Rgba: @colorPickerRef?.Rgba</div>
<div>Hsv: @colorPickerRef?.Hsv</div>
```

```csharp
@using Bit.BlazorUI.Demo.Client.Core.Models; // Assuming BitColorPicker is here or similar

@code {
    private string boundColor = "#FFFFFFAA"; // Initial color with alpha
    private BitColorPicker colorPickerRef = default!;

    // No specific methods needed here, just accessing properties via ref
    // Ensure colorPickerRef is not null before accessing properties (e.g., in @code block or after render)
    protected override void OnAfterRender(bool firstRender)
    {
        if (firstRender) { StateHasChanged(); } // Re-render to show initial ref values if needed
    }
}
```

*(Note: The `Hsv` property likely returns a custom type or tuple representing Hue, Saturation, Value)*

---

### Example 6: Style & Class Customization

Demonstrates applying custom dimensions and appearance using inline `Style`, a CSS `Class`, or potentially the `Styles`/`Classes` parameters (though not shown in this specific example's code snippet, the CSS implies they could be used).

```cshtml
<style>
    .custom-class {
        width: 100px;  /* Example: Make the component narrower */
        height: 250px; /* Example: Adjust height */
    }
</style>

<BitColorPicker ShowAlphaSlider Style="width: 250px; height: 150px;" />

<BitColorPicker ShowAlphaSlider Class="custom-class" />
```

*(Note: The API reference below details `Styles` and `Classes` parameters for more granular control over internal elements, similar to `BitTextField`)*

---

## API Reference

### `BitColorPicker` Parameters

| Name            | Type                                  | Default Value | Description                                                                                                                            |
| :-------------- | :------------------------------------ | :------------ | :------------------------------------------------------------------------------------------------------------------------------------- |
| `Alpha`         | `double`                              | `1`           | The alpha value (opacity) of the selected color, ranging from 0 (transparent) to 1 (opaque). Use with `@bind-Alpha` for two-way binding. |
| `Color`         | `string`                              | `#FFFFFFFF`   | The selected color value as a CSS-compatible string (e.g., "#FF0000", "rgb(255,0,0)", "rgba(255,0,0,0.5)"). Use with `@bind-Color`.     |
| `OnChange`      | `EventCallback<BitColorChangeEventArgs>`|               | Callback invoked when the selected color or alpha value changes. Provides `Color` (string) and `Alpha` (double) in event args.         |
| `ShowAlphaSlider`| `bool`                                | `false`       | If `true`, displays the alpha slider control, allowing the user to adjust the color's opacity.                                        |
| `ShowPreview`   | `bool`                                | `false`       | If `true`, displays a preview box showing the currently selected color, including its alpha transparency.                            |
| **Inherited Parameters** |                              |               | *Includes parameters from `BitComponentBase` (see below).*                                                                             |

---

### `BitColorPicker` Public Members

Properties accessible via `@ref` on the component instance.

| Name   | Type                                  | Description                                                                       |
| :----- | :------------------------------------ | :-------------------------------------------------------------------------------- |
| `Alpha`| `double`                              | Gets the current alpha value (0.0 to 1.0).                                        |
| `Color`| `string`                              | Gets the current color value in the format consistent with the bound `Color` value. |
| `Hex`  | `string?`                             | Gets the current color as a 6-digit Hex string (e.g., "#FF0000"). Null if invalid. |
| `Rgb`  | `string?`                             | Gets the current color as an RGB string (e.g., "rgb(255,0,0)"). Null if invalid.  |
| `Rgba` | `string?`                             | Gets the current color as an RGBA string (e.g., "rgba(255,0,0,0.5)"). Null if invalid.|
| `Hsv`  | `BitHsv?` (or similar custom type/tuple)| Gets the current color represented in the Hue-Saturation-Value color space.       |

---

### `BitComponentBase` Parameters (Base for all Bit components, Inherited by `BitColorPicker`)

Common parameters for all Bit Blazor UI components.

| Name             | Type                            | Default Value                       | Description                                                                                                 |
| :--------------- | :------------------------------ | :---------------------------------- | :---------------------------------------------------------------------------------------------------------- |
| `AriaLabel`      | `string?`                       | `null`                              | The `aria-label` attribute for the root element (group) for accessibility. Defaults to a generated label like "Color picker, Red ... Green ... Blue ... selected." |
| `Class`          | `string?`                       | `null`                              | Custom CSS class(es) to apply to the root element of the component.                                         |
| `Dir`            | `BitDir?`                       | `null`                              | Sets the text direction (`ltr`, `rtl`, `auto`) for the component. See `BitDir` enum below.                    |
| `HtmlAttributes` | `Dictionary<string, object>`    | `new Dictionary<string, object>()`  | Allows capturing and rendering arbitrary HTML attributes (splatting) on the root element of the component.  |
| `Id`             | `string?`                       | `null`                              | Custom `id` attribute for the root element. If not provided, the component's `UniqueId` is used.          |
| `IsEnabled`      | `bool`                          | `true`                              | Whether the component is enabled. If `false`, it appears grayed out and interaction is disabled.            |
| `Style`          | `string?`                       | `null`                              | Custom inline CSS style(s) to apply to the root element of the component.                                   |
| `Visibility`     | `BitVisibility`                 | `BitVisibility.Visible`             | Controls whether the component is visible, hidden (occupies space), or collapsed (no space). See `BitVisibility` enum below. |

---

### `BitComponentBase` Public Members (Base for all Bit components, Inherited by `BitColorPicker`)

| Name          | Type               | Default Value    | Description                                                                                                      |
| :------------ | :----------------- | :--------------- | :--------------------------------------------------------------------------------------------------------------- |
| `UniqueId`    | `Guid`             | `Guid.NewGuid()` | A read-only, unique identifier (GUID) generated automatically for each component instance. Useful for `id` refs. |
| `RootElement` | `ElementReference` |                  | Provides a reference to the root HTML element (`div`) of the component.                                          |

---

### `BitColorChangeEventArgs` Properties (Passed to `OnChange` Event)

Details about the color change event.

| Property | Type      | Description                                                                                                     |
| :------- | :-------- | :-------------------------------------------------------------------------------------------------------------- |
| `Color`  | `string?` | The main color value (Hex or RGB string, matching the format of the `Color` parameter) of the newly selected color. |
| `Alpha`  | `double`  | The alpha value (0.0 to 1.0) of the newly selected color.                                                        |

---

### Related Enums

#### `BitVisibility` Enum (for `Visibility` parameter)

Controls the rendering and visibility of the component.

| Name        | Value | Description                                                                        | CSS Effect           |
| :---------- | :---- | :--------------------------------------------------------------------------------- | :------------------- |
| `Visible`   | 0     | The component is rendered and visible (default).                                   | (standard display)   |
| `Hidden`    | 1     | The component is not visible, but still occupies its space in the layout.          | `visibility: hidden` |
| `Collapsed` | 2     | The component is not rendered and does not occupy any space in the layout.         | `display: none`      |

#### `BitDir` Enum (for `Dir` parameter)

Specifies the text directionality of the component's content.

| Name   | Value | Description                                                                                                  | Corresponds to HTML `dir` |
| :----- | :---- | :----------------------------------------------------------------------------------------------------------- | :------------------------ |
| `Ltr`  | 0     | Left-to-right text direction (e.g., English).                                                                | `ltr`                     |
| `Rtl`  | 1     | Right-to-left text direction (e.g., Arabic, Hebrew).                                                         | `rtl`                     |
| `Auto` | 2     | The browser determines the direction based on the text content using a basic algorithm.                        | `auto`                    |

---

## Key Considerations & Best Practices

* **Color Format:** Be aware that the `@bind-Color` parameter works with CSS-compatible strings (`#RRGGBB`, `#RRGGBBAA`, `rgb(r,g,b)`, `rgba(r,g,b,a)`). The component tries to preserve the format you initially provide. If you need a specific format consistently, you might need to handle conversion in your `OnChange` event or when accessing the public properties (`Hex`, `Rgb`, `Rgba`).
* **Alpha Binding:** Use `@bind-Alpha` (or the `OnChange` event) if you need to specifically track or bind the alpha value separately from the main color string.
* **Accessibility:** While the component includes ARIA roles and labels, ensure the context where you place the `BitColorPicker` is understandable. The default `aria-label` dynamically updates with the selected color, which is helpful.
* **Styling:** Use `Style` and `Class` for basic adjustments. For more complex themes or targeting internal parts (like the sliders, thumb, preview box), you'll likely need to use the `Styles` or `Classes` parameters (though their specific structure isn't fully detailed in the provided API table, assume a similar pattern to other Bit components like `BitTextField`).
* **Public API Access:** When using `@ref` to access properties like `Hex`, `Rgb`, etc., ensure the component has rendered at least once before accessing them, or use null-conditional operators (`?.`) to avoid runtime errors.
