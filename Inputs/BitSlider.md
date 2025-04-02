# BitSlider Blazor Component

**Objective:** This document provides context and reference information about the `BitSlider` Blazor component, based *solely* on the provided HTML documentation extract. Use this information to understand the component's purpose, features, parameters, and usage patterns for generating code or explanations.

**Key Component:** `BitSlider`
**Alias:** `Range` (Likely referring to the `IsRanged` mode)

---

## Overview

`BitSlider` is a component that provides a visual way to select a value or a range of values within a defined minimum and maximum. It's suitable for scenarios where users need to set specific values like volume or brightness and benefit from immediate visual feedback.

---

## Usage Examples

**1. Basic**

*   **Description**: Demonstrates fundamental `BitSlider` configurations: a default slider, a disabled slider with a default value, a slider with snapping behavior (`Step`), a slider with custom value formatting (`ValueFormat`), and a slider originating from zero (`IsOriginFromZero`).
*   **Code**:
    ```cshtml
    <BitSlider Label="Basic slider" />

    <BitSlider Label="Disabled slider" DefaultValue="5" IsEnabled="false" />

    <BitSlider Label="Snapping slider" Min="0" Max="50" Step="10" />

    <BitSlider Label="Formatted value" Max="1" Step="0.01" DefaultValue="0.69" ValueFormat="0 %" />

    <BitSlider Label="Origin from zero" Min="-5" Max="5" DefaultValue="0" IsOriginFromZero="true" />
    ```

**2. Visibility**

*   **Description**: Shows how to control the visibility of the slider component using the `Visibility` parameter (`Visible`, `Hidden`, `Collapsed`).
*   **Code**:
    ```cshtml
    Visible: [ <BitSlider Visibility="BitVisibility.Visible" /> ]
    Hidden: [ <BitSlider Visibility="BitVisibility.Hidden" /> ]
    Collapsed: [ <BitSlider Visibility="BitVisibility.Collapsed" /> ]
    ```

**3. Vertical**

*   **Description**: Demonstrates rendering the slider vertically using the `IsVertical` parameter, including basic, disabled, formatted, and origin-from-zero variations.
*   **Code**:
    ```cshtml
    <BitSlider Label="Basic" IsVertical="true" />

    <BitSlider Label="Disabled" IsVertical="true" IsEnabled="false" />

    <BitSlider Label="Formatted value" IsVertical="true" DefaultValue="2" ValueFormat="0 cm" />

    <BitSlider Label="Origin from zero" IsVertical="true" Min="-5" Max="5" DefaultValue="0" IsOriginFromZero="true" />
    ```

**4. Range**

*   **Description**: Shows the ranged slider functionality (`IsRanged="true"`), allowing selection of a lower and upper value. Examples include basic, disabled, formatted, and origin-from-zero variations in ranged mode. `DefaultLowerValue` and `DefaultUpperValue` are used to set initial range values.
*   **Code**:
    ```cshtml
    <BitSlider Label="Basic" IsRanged="true" />

    <BitSlider Label="Disabled" IsRanged="true" DefaultLowerValue="2" DefaultUpperValue="5" IsEnabled="false" />

    <BitSlider Label="Formatted value" IsRanged="true" Step="0.1" ValueFormat="0.0 px"
               DefaultLowerValue="4.2" DefaultUpperValue="8.5" />

    <BitSlider Label="Origin from zero" IsRanged="true" Min="-5" Max="5" DefaultUpperValue="2" IsOriginFromZero="true" />
    ```

**5. Vertical & Range**

*   **Description**: Combines vertical orientation (`IsVertical="true"`) with range selection (`IsRanged="true"`).
*   **Code**:
    ```cshtml
    <BitSlider Label="Basic" IsVertical="true" IsRanged="true"
               DefaultLowerValue="1" DefaultUpperValue="2" />

    <BitSlider Label="Disabled" IsVertical="true" IsRanged="true"
               DefaultUpperValue="1" DefaultLowerValue="3" IsEnabled="false" />

    <BitSlider Label="Formatted value" IsVertical="true" IsRanged="true"
               Step="0.01" ValueFormat="0.00 rem"
               DefaultLowerValue="4.20" DefaultUpperValue="6.9" />

    <BitSlider Label="Origin from zero" IsVertical="true" IsRanged="true"
               Min="-5" Max="5" DefaultUpperValue="3" IsOriginFromZero="true" />
    ```

**6. Style & Class**

*   **Description**: Demonstrates applying custom styling using inline `Style`, root `Class`, and the `Styles`/`Classes` parameters for targeted styling of internal slider elements (e.g., Root, Label, SliderBox, ValueInput, Focused state). Includes examples for both single-value and ranged sliders.
*   **Code**: (Includes CSS for context)
    ```css
    /* Style for custom class example */
    .custom-class {
        overflow: hidden; margin-inline: 1rem; border-radius: 1rem; border: 2px solid brown;
    }
    .custom-class *, .custom-class *::after { border: none; }

    /* Styles for Classes parameter example (range) */
    .custom-slider-box { background: linear-gradient(0deg, seagreen calc(0.5rem * 0.5), transparent 0); }
    .custom-slider-box:hover { background: linear-gradient(0deg, seagreen calc(0.5rem * 0.5), transparent 0); }
    .custom-slider-box:hover::before { background-color: darkgreen; }
    .custom-slider-box::before { background-color: green; }
    .custom-range-input::-webkit-slider-thumb { background-color: white; border: 0.25rem solid green; }
    .custom-range-input:hover::-webkit-slider-thumb { background-color: white; border: 0.25rem solid darkgreen; }

    /* Styles for Classes parameter example (single) */
    .custom-input::-webkit-slider-thumb { width: 1.5rem; height: 1.5rem; border-radius: 50%; margin-top: -0.75rem; border-color: whitesmoke; background-color: whitesmoke; box-shadow: 0 0 0.5rem 0 lightgray; }
    .custom-input:hover::-webkit-slider-thumb { border-color: whitesmoke; background-color: whitesmoke; }
    .custom-input::-webkit-slider-runnable-track { height: 0.125rem; background: linear-gradient(dodgerblue, dodgerblue) 0/var(--sx) 100% no-repeat, whitesmoke; }
    .custom-input:hover::-webkit-slider-runnable-track { background: linear-gradient(dodgerblue, dodgerblue) 0/var(--sx) 100% no-repeat, whitesmoke; }
    ```
    ```cshtml
    <BitSlider DefaultValue="3" Label="Custom styles"
               Styles="@(new() { Root = "text-shadow: aqua 0 0 1rem;",
                                 Label = "font-weight: 900; font-size: 1.25rem;" } )" />

    <BitSlider DefaultValue="5" Label="Custom classes"
               Classes="@(new() { ValueInput = "custom-input" } )" />

    <BitSlider IsRanged="true" Max="100" DefaultLowerValue="54" DefaultUpperValue="84"
               Classes="@(new() { LowerValueInput = "custom-range-input",
                                  UpperValueInput = "custom-range-input",
                                  SliderBox = "custom-slider-box" } )" />
    ```
    *(Note: The example HTML for `Styles` and `Classes` parameters on single value sliders might contain CSS rules intended for range sliders, copied for demonstration.)*

**7. Binding**

*   **Description**: Shows one-way (`Value`) and two-way (`@bind-Value`) data binding with the `BitSlider`, syncing its value with other components like `BitRating` or `BitNumberField`. Also demonstrates the `OnChange` event handler.
*   **Code**:
    ```cshtml
    <BitSlider Label="One-way" AllowZeroStars="true" Value="oneWayBinding" /> @* AllowZeroStars seems misplaced here, likely from Rating component context *@@
    <BitRating Max="10" @bind-Value="oneWayBinding" />

    <BitSlider Label="Two-way" @bind-Value="twoWayBinding" />
    <BitRating Max="10" @bind-Value="twoWayBinding" />

    <BitSlider Label="OnChange" DefaultValue="2" OnChange="v => onChangeValue = v.Value" />
    <BitLabel>OnChange value: @onChangeValue</BitLabel>
    ```
    ```csharp
    @code {
        private double oneWayBinding = 1;
        private double twoWayBinding = 1;
        private double onChangeValue;
    }
    ```

**8. Validation**

*   **Description**: Integrates `BitSlider` within an `EditForm` for validation using data annotations (`[Range]`).
*   **Code**:
    ```cshtml
    @using System.ComponentModel.DataAnnotations;

    <EditForm Model="ValidationModel" OnValidSubmit="HandleValidSubmit" OnInvalidSubmit="HandleInvalidSubmit">
        <DataAnnotationsValidator />

        <BitSlider AllowZeroStars="true" @bind-Value="ValidationModel.Value" /> @* AllowZeroStars likely misplaced *@
        <ValidationMessage For="@(() => ValidationModel.Value)" />

        <BitButton ButtonType="BitButtonType.Submit">Submit</BitButton>
    </EditForm>
    ```
    ```csharp
    @code {
        public class BitRatingDemoFormModel // Note: Class name seems incorrect, likely should be BitSlider...
        {
            [Range(typeof(double), "1", "5", ErrorMessage = "Your rate must be between {1} and {2}")]
            public double Value { get; set; }
        }

        public BitRatingDemoFormModel ValidationModel = new();

        private void HandleValidSubmit() { }
        private void HandleInvalidSubmit() { }
    }
    ```

**9. RTL**

*   **Description**: Demonstrates rendering the slider component in a right-to-left layout using `Dir="BitDir.Rtl"`, applicable to both single-value and ranged sliders.
*   **Code**:
    ```cshtml
    <BitSlider Label="RTL slider" Dir="BitDir.Rtl" />

    <BitSlider IsRanged Label="RTL ranged slider"
               Dir="BitDir.Rtl"
               DefaultLowerValue="2" DefaultUpperValue="5" />
    ```

---

## API Reference

**BitSlider Parameters**

| Name                    | Type                          | Default           | Description                                                                               |
| :---------------------- | :---------------------------- | :---------------- | :---------------------------------------------------------------------------------------- |
| `AriaValueText`         | `Func<double, string>?`       | `null`            | Function to provide custom `aria-valuetext`.                                              |
| `Classes`               | `BitSliderClassStyles?`       | `null`            | Custom CSS classes for different parts.                                                   |
| `DefaultLowerValue`     | `double?`                     | `null`            | Initial lower value for ranged slider (uncontrolled).                                     |
| `DefaultUpperValue`     | `double?`                     | `null`            | Initial upper value for ranged slider (uncontrolled).                                     |
| `DefaultValue`          | `double?`                     | `null`            | Initial value for single slider (uncontrolled).                                           |
| `IsOriginFromZero`      | `bool`                        | `false`           | If true, the track start visually aligns with the zero point when Min < 0 < Max.        |
| `IsRanged`              | `bool`                        | `false`           | Enables range selection mode with two thumbs.                                           |
| `IsReadOnly`            | `bool`                        | `false`           | Makes the slider read-only (visual only, prevents user interaction).                      |
| `IsVertical`            | `bool`                        | `false`           | Renders the slider vertically.                                                            |
| `Label`                 | `string?`                     | `null`            | Descriptive label displayed above the slider.                                             |
| `LowerValue`            | `double`                      | `0`               | Lower value in ranged mode (`@bind-LowerValue`).                                        |
| `Min`                   | `double`                      | `0`               | Minimum allowed value.                                                                  |
| `Max`                   | `double`                      | `10`              | Maximum allowed value.                                                                  |
| `OnChange`              | `EventCallback<ChangeEventArgs>`|                   | Callback invoked on every value change during interaction.                              |
| `RangeValue`            | `BitSliderRangeValue?`        | `null`            | Represents the range value (`Lower`, `Upper`). Use `@bind-RangeValue`.                |
| `ShowValue`             | `bool`                        | `true`            | Shows the current value(s) next to the slider.                                          |
| `SliderBoxHtmlAttributes`| `Dictionary<string, object>?` | `null`            | Additional HTML attributes applied to the slider box `div`.                             |
| `Step`                  | `double`                      | `1`               | The increment/decrement step size.                                                      |
| `Styles`                | `BitSliderClassStyles?`       | `null`            | Custom CSS styles for different parts.                                                  |
| `UpperValue`            | `double`                      | `0`               | Upper value in ranged mode (`@bind-UpperValue`).                                        |
| `Value`                 | `double`                      | `0`               | The current value in single-select mode (`@bind-Value`).                                |
| `ValueFormat`           | `string?`                     | `null`            | Custom format string for displaying the value(s).                                       |
| *(Inherited)*           | *(See BitInputBase)*          |                   |                                                                                         |

**BitInputBase Parameters & Members (Inherited)**

*(Refer to the `BitCheckbox` reference file for details)*

**BitComponentBase Parameters & Members (Inherited)**

*(Refer to the `BitCheckbox` reference file for details)*

**BitSliderClassStyles Properties**

| Name              | Type      | Default | Description                                                         |
| :---------------- | :-------- | :------ | :------------------------------------------------------------------ |
| `Root`            | `string?` | `null`  | CSS class/style for the root `div` element.                       |
| `Label`           | `string?` | `null`  | CSS class/style for the label element.                              |
| `UpperValueLabel` | `string?` | `null`  | CSS class/style for the upper value label (ranged mode).          |
| `Container`       | `string?` | `null`  | CSS class/style for the main container `div`.                     |
| `LowerValueLabel` | `string?` | `null`  | CSS class/style for the lower value label (ranged mode).          |
| `SliderBox`       | `string?` | `null`  | CSS class/style for the `div` containing the input(s).            |
| `LowerValueInput` | `string?` | `null`  | CSS class/style for the lower value `input` element (ranged mode). |
| `UpperValueInput` | `string?` | `null`  | CSS class/style for the upper value `input` element (ranged mode). |
| `ValueInput`      | `string?` | `null`  | CSS class/style for the single `input` element.                   |
| `OriginFromZero`  | `string?` | `null`  | CSS class/style for the zero-origin marker `span`.                |
| `ValueLabel`      | `string?` | `null`  | CSS class/style for the value label (single mode).                |

**BitSliderRangeValue Properties**

| Name    | Type   | Default | Description                          |
| :------ | :----- | :------ | :----------------------------------- |
| `Lower` | `double` | `0`     | The lower value of the range.      |
| `Upper` | `double` | `0`     | The upper value of the range.      |

**Enums**

*   **BitSize**: Defines size options (`Small`, `Medium`, `Large`). *(Note: Although listed in the linked files, the example specifically for Size seems missing in the provided HTML for Slider)*
*   **BitVisibility**: Defines visibility states (`Visible`, `Hidden`, `Collapsed`).
*   **BitDir**: Defines text direction (`Ltr`, `Rtl`, `Auto`).
*   **BitLabelPosition**: Defines label placement (`Top`, `Start`, `End`, `Bottom`). *(Note: Not demonstrated for Slider in provided HTML)*
*   **BitSpinButtonMode**: Defines spin button styles (`Compact`, `Inline`, `Spread`). *(Note: Not applicable/demonstrated for Slider)*

---

## Feedback

*   Provide feedback via the **GitHub repo**: [File an Issue](https://github.com/bitfoundation/bitplatform/issues/new/choose) or [Start a Discussion](https://github.com/bitfoundation/bitplatform/discussions/new/choose).
*   Review/Edit this demo page: [Review](https://github.com/bitfoundation/bitplatform/blob/develop/src/BlazorUI/Demo/Client/Bit.BlazorUI.Demo.Client.Core/Pages/Components/Inputs/Slider/BitSliderDemo.razor) / [Edit](https://github.com/bitfoundation/bitplatform/edit/develop/src/BlazorUI/Demo/Client/Bit.BlazorUI.Demo.Client.Core/Pages/Components/Inputs/Slider/BitSliderDemo.razor)
*   Review/Edit the component source: [Review](https://github.com/bitfoundation/bitplatform/blob/develop/src/BlazorUI/Bit.BlazorUI/Components/Inputs/Slider/BitSlider.razor) / [Edit](https://github.com/bitfoundation/bitplatform/edit/develop/src/BlazorUI/Bit.BlazorUI/Components/Inputs/Slider/BitSlider.razor)

