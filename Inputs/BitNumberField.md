# BitNumberField Blazor Component

**Objective:** This document provides context and reference information about the `BitNumberField` Blazor component, based *solely* on the provided HTML documentation extract. Use this information to understand the component's purpose, features, parameters, and usage.

**Key Component:** `BitNumberField`
**Alias:** `NumberInput`

---

## Overview

`BitNumberField` is a component designed for entering numeric values. It supports various number types (decimal, integer) and formats, including options for suffixes. It also provides optional increment and decrement buttons.

---

## Usage Examples

**1. Basic**

*   **Description**: Demonstrates basic configurations: a standard field, a disabled field with a default value, a field with a placeholder, and a required field.
*   **Code**:
    ```cshtml
    <BitNumberField Label="Basic" TValue="int?" />

    <BitNumberField Label="Disabled & DefaultValue" DefaultValue="1363" IsEnabled="false" />

    <BitNumberField Label="Placeholder" TValue="int?" Placeholder="Enter a number..." />

    <BitNumberField Label="Required" TValue="int?" Required />
    ```

**2. Label**

*   **Description**: Shows different label positions (`Top` (default), `Start`, `End`, `Bottom`) using the `LabelPosition` parameter and demonstrates customizing the label using `LabelTemplate`.
*   **Code**:
    ```cshtml
    <BitNumberField Label="Top (default)" TValue="int" />

    <BitNumberField Label="Start" LabelPosition="BitLabelPosition.Start" TValue="int" />

    <BitNumberField Label="End" LabelPosition="BitLabelPosition.End" TValue="int" />

    <BitNumberField Label="Bottom" LabelPosition="BitLabelPosition.Bottom" TValue="int" />

    <BitNumberField TValue="int">
        <LabelTemplate>
            <div style="display:flex;align-items:center;gap:10px">
                <BitLabel Style="color:green;">This is custom Label</BitLabel>
                <BitIcon IconName="@BitIconName.Filter" Style="font-size:18px;" />
            </div>
        </LabelTemplate>
    </BitNumberField>
    ```

**3. Icons**

*   **Description**: Illustrates adding an icon next to the label (`IconName`) and customizing the increment/decrement button icons (`IncrementIconName`, `DecrementIconName`) for different display modes (`Compact`, `Inline`, `Spread`).
*   **Code**:
    ```cshtml
    <BitNumberField Label="Label & Icon" TValue="int"
                    IconName="@BitIconName.Lightbulb" />

    <BitNumberField Label="Compact mode" TValue="int"
                    Mode="BitSpinButtonMode.Compact"
                    IncrementIconName="@BitIconName.LikeSolid"
                    DecrementIconName="@BitIconName.DislikeSolid" />

    <BitNumberField Label="Inline mode" TValue="int"
                    Mode="BitSpinButtonMode.Inline"
                    IncrementIconName="@BitIconName.Forward"
                    DecrementIconName="@BitIconName.Back" />

    <BitNumberField Label="Spread mode" TValue="int"
                    Mode="BitSpinButtonMode.Spread"
                    IncrementIconName="@BitIconName.CalculatorAddition"
                    DecrementIconName="@BitIconName.CalculatorSubtract" />
    ```

**4. NumberFormat**

*   **Description**: Shows how to format the displayed number using standard or custom numeric format strings via the `NumberFormat` parameter (e.g., "N0", "C0", "000000").
*   **Code**:
    ```cshtml
    <BitNumberField Label="N0" DefaultValue="1234567890d" NumberFormat="N0" />

    <BitNumberField Label="C0" DefaultValue="150" NumberFormat="C0" />

    <BitNumberField Label="000000" DefaultValue="1363" NumberFormat="000000" />
    ```

**5. Prefix & Suffix**

*   **Description**: Demonstrates adding text before (`Prefix`) and after (`Suffix`) the input value. Note that these are purely visual and not part of the bound value.
*   **Code**:
    ```cshtml
    <BitNumberField TValue="int" Label="Prefix" Prefix="Distance:" />

    <BitNumberField TValue="int" Label="Suffix" Suffix="km" />

    <BitNumberField TValue="int" Label="Prefix & Suffix" Prefix="Distance:" Suffix="km" />

    <BitNumberField TValue="int" Label="With buttons" Prefix="Distance:" Suffix="km" ShowButtons="true" />

    <BitNumberField TValue="int" Label="Disabled" Prefix="Distance:" Suffix="km" IsEnabled="false" />
    ```

**6. Binding**

*   **Description**: Shows one-way (`Value` parameter) and two-way (`@bind-Value`) data binding with the `BitNumberField`.
*   **Code**:
    ```cshtml
    <BitNumberField Label="One-way" Value="oneWayValue" />
    <BitRating @bind-Value="oneWayValue" />

    <BitNumberField Label="Two-way" @bind-Value="twoWayValue" />
    <BitRating @bind-Value="twoWayValue" />
    ```
    ```csharp
    @code {
        private double oneWayValue;
        private double twoWayValue;
    }
    ```

**7. Min & Max**

*   **Description**: Demonstrates setting minimum (`Min`) and maximum (`Max`) allowed values for the input.
*   **Code**:
    ```cshtml
    <BitNumberField Label="Min = 0" Min="0" @bind-Value="minValue" />
    <div>value: [@minValue]</div>

    <BitNumberField Label="Max = 100" Max="100" @bind-Value="maxValue" />
    <div>value: [@maxValue]</div>

    <BitNumberField Label="Min & Max (-10, 10)" Min="-10" Max="10" @bind-Value="minMaxValue" />
    <div>value: [@minMaxValue]</div>
    ```
    ```csharp
    @code {
        private int minValue;
        private int maxValue;
        private int minMaxValue;
    }
    ```

**8. Precision**

*   **Description**: Uses the `Precision` parameter to specify the number of decimal places to round the displayed value to.
*   **Code**:
    ```cshtml
    <BitNumberField Precision="2" @bind-Value="precisionInputValue" Label="Rounding to 2 Decimal Places" />
    ```
    ```csharp
    @code {
        private double precisionInputValue = 3.1415;
    }
    ```

**9. HideInput**

*   **Description**: Shows how to hide the actual input field using `HideInput`, often used when the value is primarily controlled by increment/decrement buttons and displayed via the label.
*   **Code**:
    ```cshtml
    <BitNumberField HideInput
                    @bind-Value="hideInputValue"
                    Mode="BitSpinButtonMode.Inline"
                    Label="@hideInputValue.ToString()" />
    ```
    ```csharp
    @code {
        private int hideInputValue;
    }
    ```

**10. Events**

*   **Description**: Demonstrates handling `OnIncrement`, `OnDecrement`, and `OnChange` events.
*   **Code**:
    ```cshtml
    <BitNumberField Label="OnIncrement & OnDecrement" ShowButtons="true"
                    OnIncrement="(double v) => onIncrementCounter++"
                    OnDecrement="(double v) => onDecrementCounter++" />
    <div>OnIncrement Counter: @onIncrementCounter</div>
    <div>OnDecrement Counter: @onDecrementCounter</div>

    <BitNumberField Label="OnChange" OnChange="(double v) => onChangeCounter++" />
    <div>OnChange Counter: @onChangeCounter</div>
    ```
    ```csharp
    @code {
        private int onIncrementCounter;
        private int onDecrementCounter;
        private int onChangeCounter;
    }
    ```

**11. Validation**

*   **Description**: Shows how to integrate `BitNumberField` with Blazor's `EditForm` and `DataAnnotationsValidator` for input validation (e.g., using `[Required]`, `[Range]`).
*   **Code**: (Includes CSS for context)
    ```css
    .validation-message { color: #A4262C; font-size: 0.75rem; }
    ```
    ```cshtml
    @using System.ComponentModel.DataAnnotations;

    <EditForm Model="@validationModel" OnValidSubmit="HandleValidSubmit" OnInvalidSubmit="HandleInvalidSubmit">
        <DataAnnotationsValidator />

        <BitNumberField Label="@($"Age: [{validationModel.Age}]")" @bind-Value="validationModel.Age" />
        <ValidationMessage For="@(() => validationModel.Age)" />
        <br />
        <BitButton ButtonType="BitButtonType.Submit">Submit</BitButton>
    </EditForm>
    ```
    ```csharp
    @code {
        public class BitNumberFieldValidationModel
        {
            [Required(ErrorMessage = "Enter an age")]
            [Range(1, 150, ErrorMessage = "Nobody is that old")]
            public int? Age { get; set; }
        }

        private BitNumberFieldValidationModel validationModel = new();

        private async Task HandleValidSubmit() { /* Logic for valid submission */ }
        private void HandleInvalidSubmit() { /* Logic for invalid submission */ }
    }
    ```

**12. Style & Class**

*   **Description**: Demonstrates applying custom styles and classes using inline `Style`, root `Class`, and the `Styles` and `Classes` parameters for targeted styling of internal elements.
*   **Code**: (Includes CSS for context)
    ```css
    .custom-class { overflow: hidden; margin-inline: 1rem; border-radius: 1rem; border: 2px solid brown; }
    .custom-class *, .custom-class *::after { border: none; }

    /* Styles for the 'Classes' parameter example */
    .custom-root { height: 3rem; display: flex; align-items: end; position: relative; margin-inline: 1rem; }
    .custom-label { top: 0; left: 0; z-index: 1; padding: 0; font-size: 1rem; color: darkgray; position: absolute; transform-origin: top left; transform: translate(0, 22px) scale(1); transition: color 200ms cubic-bezier(0, 0, 0.2, 1) 0ms, transform 200ms cubic-bezier(0, 0, 0.2, 1) 0ms; }
    .custom-label-top { transform: translate(0, 1.5px) scale(0.75); }
    .custom-input { padding: 0; font-size: 1rem; font-weight: 900; }
    .custom-input-wrapper { border-radius: 0; position: relative; border-width: 0 0 1px 0; }
    .custom-input-wrapper::after { content: ''; width: 0; height: 2px; border: none; position: absolute; inset: 100% 0 0 50%; background-color: blueviolet; transition: width 0.3s ease, left 0.3s ease; }
    .custom-focus .custom-input-wrapper::after { left: 0; width: 100%; }
    .custom-focus .custom-label { color: blueviolet; transform: translate(0, 1.5px) scale(0.75); }
    ```
    ```cshtml
    <BitNumberField DefaultValue="10" Style="box-shadow: aqua 0 0 1rem; margin-inline: 1rem;" />
    <BitNumberField DefaultValue="20" Class="custom-class" />

    <BitNumberField DefaultValue="1" Label="Styles"
                    Styles="@(new() { Root = "margin-inline: 1rem;",
                                      Focused = "--focused-background: #b2b2b25a;",
                                      InputWrapper = "background: var(--focused-background);",
                                      Label = "text-shadow: aqua 0 0 1rem; font-weight: 900; font-size: 1.25rem;",
                                      Input = "padding: 0.5rem;" })" />

    <BitNumberField TValue="int?" Label="Classes" @bind-Value="classesValue"
                    Classes="@(new() { Root = "custom-root",
                                       InputWrapper = "custom-input-wrapper",
                                       Focused = "custom-focus",
                                       Input = "custom-input",
                                       Label = $"custom-label{(classesValue is null ? string.Empty : " custom-label-top")}" })" />
    ```

**13. RTL**

*   **Description**: Shows how to render the `BitNumberField` in a right-to-left layout, either by setting `Dir="BitDir.Rtl"` directly or using a cascading value.
*   **Code**:
    ```cshtml
    <CascadingValue Value="BitDir.Rtl">
        <BitNumberField Label="برچسب در بالا" TValue="int" ShowButtons />
        <BitNumberField Label="برچسب درخط" TValue="int" InlineLabel />
        <BitNumberField TValue="int" Required />
        <BitNumberField Label="الزامی" TValue="int" Required />
    </CascadingValue>
    ```

---

## API Reference

**BitNumberField Parameters**

| Name                       | Type                          | Default                   | Description                                                                          |
| :------------------------- | :---------------------------- | :------------------------ | :----------------------------------------------------------------------------------- |
| `AriaDescription`          | `string?`                     | `null`                    | Detailed description for screen readers.                                             |
| `AriaPositionInSet`        | `int?`                        | `null`                    | `aria-posinset` value if part of a set.                                              |
| `AriaSetSize`              | `int?`                        | `null`                    | `aria-setsize` value if part of a set.                                               |
| `AriaValueNow`             | `TValue?`                     | `null`                    | Sets `aria-valuenow`.                                                                |
| `AriaValueText`            | `string?`                     | `null`                    | Sets `aria-valuetext`.                                                               |
| `Classes`                  | `BitNumberFieldClassStyles?`  | `null`                    | Custom CSS classes for different parts.                                              |
| `DecrementAriaLabel`       | `string?`                     | `null`                    | Aria-label for the decrement button.                                                 |
| `DecrementIconName`        | `string?`                     | `null`                    | Custom icon for the decrement button.                                                |
| `DecrementTitle`           | `string?`                     | `null`                    | Tooltip for the decrement button.                                                    |
| `DefaultValue`             | `TValue?`                     | `default`                 | Initial value (uncontrolled).                                                        |
| `HideInput`                | `bool`                        | `false`                   | Hides the input field visually.                                                      |
| `IconAriaLabel`            | `string?`                     | `null`                    | Aria-label for the `IconName` icon.                                                |
| `IconName`                 | `string?`                     | `null`                    | Icon displayed next to the label.                                                    |
| `IncrementAriaLabel`       | `string?`                     | `null`                    | Aria-label for the increment button.                                                 |
| `IncrementIconName`        | `string?`                     | `null`                    | Custom icon for the increment button.                                                |
| `IncrementTitle`           | `string?`                     | `null`                    | Tooltip for the increment button.                                                    |
| `IsInputReadOnly`          | `bool`                        | `false`                   | Makes the input visually read-only (doesn't prevent button interaction).         |
| `LabelPosition`            | `BitLabelPosition`            | `Top`                     | Position of the label (`Top`, `Start`, `End`, `Bottom`).                           |
| `Label`                    | `string`                      | `string.Empty`            | Text for the label.                                                                  |
| `LabelTemplate`            | `RenderFragment?`             | `null`                    | Custom template for the label.                                                       |
| `Min`                      | `string?`                     | `null`                    | Minimum allowed value (applied as HTML attribute).                                 |
| `Max`                      | `string?`                     | `null`                    | Maximum allowed value (applied as HTML attribute).                                 |
| `Mode`                     | `BitSpinButtonMode?`          | `null`                    | Render mode for spin buttons (`Compact`, `Inline`, `Spread`).                      |
| `NumberFormat`             | `string?`                     | `null`                    | Format string for displaying the number.                                           |
| `OnBlur`                   | `EventCallback<FocusEventArgs>`|                           | Callback when the control loses focus.                                             |
| `OnDecrement`              | `EventCallback<TValue>`       |                           | Callback when decrement button/key is pressed. Provides the *new* value.           |
| `OnFocus`                  | `EventCallback<FocusEventArgs>`|                           | Callback when the control gains focus.                                             |
| `OnFocusIn`                | `EventCallback<FocusEventArgs>`|                           | Callback when focus moves into the input.                                          |
| `OnFocusOut`               | `EventCallback<FocusEventArgs>`|                           | Callback when focus moves out of the input.                                          |
| `OnIncrement`              | `EventCallback<TValue>`       |                           | Callback when increment button/key is pressed. Provides the *new* value.           |
| `ParsingErrorMessage`      | `string`                      | `"{0} field not valid"`     | Error message format string for parsing errors.                                      |
| `Placeholder`              | `string?`                     | `null`                    | Placeholder text for the input field.                                                |
| `Precision`                | `int?`                        | `null`                    | Number of decimal places to round the value to.                                    |
| `Prefix`                   | `string?`                     | `null`                    | Text displayed before the input value.                                               |
| `PrefixTemplate`           | `RenderFragment?`             | `null`                    | Custom template for the prefix.                                                      |
| `Step`                     | `string?`                     | `null`                    | Increment/decrement step value (applied as HTML attribute).                        |
| `Styles`                   | `BitNumberFieldClassStyles?`  | `null`                    | Custom CSS styles for different parts.                                               |
| `Suffix`                   | `string?`                     | `null`                    | Text displayed after the input value.                                                |
| `SuffixTemplate`           | `RenderFragment?`             | `null`                    | Custom template for the suffix.                                                      |
| `Title`                    | `string?`                     | `null`                    | Tooltip text for the root element.                                                 |
| *(Inherited)*              | *(See BitTextInputBase)*    |                           |                                                                                      |

**BitNumberField Public Members**

| Name             | Type               | Description                                               |
| :--------------- | :----------------- | :-------------------------------------------------------- |
| `InputElement`   | `ElementReference` | `ElementReference` for the main input element.            |
| `FocusAsync`     | `() => ValueTask`  | Method to programmatically focus the input element.       |
| *(Inherited)*    | *(See BitInputBase)*|                                                           |

**BitTextInputBase Parameters (Inherited)**

| Name           | Type      | Default | Description                                                          |
| :------------- | :-------- | :------ | :------------------------------------------------------------------- |
| `AutoComplete` | `string?` | `null`  | `autocomplete` attribute for the input.                            |
| `AutoFocus`    | `bool`    | `false` | Auto-focuses the input on first render.                              |
| `DebounceTime` | `int`     | `0`     | Debounce time (ms) for value changes before triggering `OnChange`.   |
| `Immediate`    | `bool`    | `false` | Triggers `OnChange` on the `oninput` event instead of `onchange`.    |
| `ThrottleTime` | `int`     | `0`     | Throttle time (ms) for value changes before triggering `OnChange`. |

**BitInputBase Parameters & Members (Inherited)**

*(Refer to the `BitCheckbox` reference file for details)*

**BitComponentBase Parameters & Members (Inherited)**

*(Refer to the `BitCheckbox` reference file for details)*

**BitNumberFieldClassStyles Properties**

| Name                       | Type      | Default | Description                                                          |
| :------------------------- | :-------- | :------ | :------------------------------------------------------------------- |
| `Root`                     | `string?` | `null`  | CSS class/style for the root element.                                |
| `LabelContainer`           | `string?` | `null`  | CSS class/style for the label container.                             |
| `Label`                    | `string?` | `null`  | CSS class/style for the label element.                               |
| `InputContainer`           | `string?` | `null`  | CSS class/style for the container of label and input.                |
| `Input`                    | `string?` | `null`  | CSS class/style for the input element.                               |
| `Icon`                     | `string?` | `null`  | CSS class/style for the icon next to the label.                      |
| `Focused`                  | `string?` | `null`  | CSS class/style applied when the component has focus.                |
| `ButtonsContainer`         | `string?` | `null`  | CSS class/style for the container of increment/decrement buttons.    |
| `IncrementButton`          | `string?` | `null`  | CSS class/style for the increment button.                            |
| `IncrementIconContainer`   | `string?` | `null`  | CSS class/style for the container of the increment icon.             |
| `IncrementIcon`            | `string?` | `null`  | CSS class/style for the increment icon.                              |
| `DecrementButton`          | `string?` | `null`  | CSS class/style for the decrement button.                            |
| `DecrementIconContainer`   | `string?` | `null`  | CSS class/style for the container of the decrement icon.             |
| `DecrementIcon`            | `string?` | `null`  | CSS class/style for the decrement icon.                              |

**Enums**

*   **BitLabelPosition**: Defines label placement (`Top`, `Start`, `End`, `Bottom`).
*   **BitSpinButtonMode**: Defines how increment/decrement buttons are displayed (`Compact`, `Inline`, `Spread`).
*   **BitVisibility**: Defines visibility states (`Visible`, `Hidden`, `Collapsed`).
*   **BitDir**: Defines text direction (`Ltr`, `Rtl`, `Auto`).

---

## Feedback

*   Provide feedback via the **GitHub repo**: [File an Issue](https://github.com/bitfoundation/bitplatform/issues/new/choose) or [Start a Discussion](https://github.com/bitfoundation/bitplatform/discussions/new/choose).
*   Review/Edit this demo page: [Review](https://github.com/bitfoundation/bitplatform/blob/develop/src/BlazorUI/Demo/Client/Bit.BlazorUI.Demo.Client.Core/Pages/Components/Inputs/NumberField/BitNumberFieldDemo.razor) / [Edit](https://github.com/bitfoundation/bitplatform/edit/develop/src/BlazorUI/Demo/Client/Bit.BlazorUI.Demo.Client.Core/Pages/Components/Inputs/NumberField/BitNumberFieldDemo.razor)
*   Review/Edit the component source: [Review](https://github.com/bitfoundation/bitplatform/blob/develop/src/BlazorUI/Bit.BlazorUI/Components/Inputs/NumberField/BitNumberField.razor) / [Edit](https://github.com/bitfoundation/bitplatform/edit/develop/src/BlazorUI/Bit.BlazorUI/Components/Inputs/NumberField/BitNumberField.razor)
