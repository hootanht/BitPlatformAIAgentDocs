# BitCheckbox Blazor Component

**Objective:** This document provides context and reference information about the `BitCheckbox` Blazor component, based *solely* on the provided HTML documentation extract. Use this information to understand the component's features, generate relevant code snippets, and explain its usage.

**Key Component:** `BitCheckbox`

---

## Overview

`BitCheckbox` is a component that permits the user to make a binary choice (checked/unchecked). It is visually represented as ☐ when unchecked and ☑ when checked by default.

---

## Usage Examples

**1. Basic**

*   **Description**: Demonstrates the default checkbox, a disabled checkbox, and a disabled checkbox that is pre-checked.
*   **Code**:
    ```cshtml
    <BitCheckbox Label="Basic checkbox" />
    <BitCheckbox Label="Disable checkbox" IsEnabled="false" />
    <BitCheckbox Label="Disable checked checkbox" IsEnabled="false" Value="true" />
    ```

**2. Check icon**

*   **Description**: Shows how to customize the icon displayed when the checkbox is checked using the `CheckIconName` parameter.
*   **Code**:
    ```cshtml
    <BitCheckbox Label="Custom check icon" CheckIconName="@BitIconName.Heart" />
    <BitCheckbox Label="Disabled custom check icon" CheckIconName="@BitIconName.WavingHand" Value="true" IsEnabled="false" />
    ```

**3. Reversed**

*   **Description**: Demonstrates placing the checkbox visual after the label using the `Reversed` parameter, shown in enabled and disabled states.
*   **Code**:
    ```cshtml
    <BitCheckbox Label="Reversed" Reversed />
    <BitCheckbox Label="Reversed - Disabled" Reversed IsEnabled="false" />
    <BitCheckbox Label="Reversed - Disable Checked" Reversed IsEnabled="false" Value="true" />
    ```

**4. LabelTemplate**

*   **Description**: Shows how to use a custom `RenderFragment` for the checkbox label instead of the simple `Label` string, allowing for richer content like icons or other components within the label.
*   **Code**: (Includes CSS for context)
    ```css
    .custom-label {
        color: red;
        font-size: 18px;
        font-weight: bold;
    }
    ```
    ```cshtml
    <BitCheckbox>
        <LabelTemplate>
            <div class="custom-label">
                Custom label <BitIcon IconName="@BitIconName.Filter" />
            </div>
        </LabelTemplate>
    </BitCheckbox>
    ```

**5. Indeterminate**

*   **Description**: Displays the checkbox in an indeterminate state using the `Indeterminate` parameter. This state is visually distinct (often a dash or filled square) and indicates a mixed selection state, commonly used in parent checkboxes for hierarchical lists. This state takes visual precedence over the `Value` (checked/unchecked) state.
*   **Code**:
    ```cshtml
    <BitCheckbox Label="Indeterminate checkbox" Indeterminate />
    <BitCheckbox Label="Disabled indeterminate checkbox" Indeterminate IsEnabled="false" />
    ```

**6. Binding**

*   **Description**: Demonstrates various binding scenarios:
    *   One-way binding to `Value` (checkbox state reflects variable, but changes don't update it).
    *   Two-way binding using `@bind-Value` (checkbox state reflects variable, and changes update it).
    *   One-way binding to `Indeterminate`.
    *   Two-way binding using `@bind-Indeterminate`.
*   **Code**:
    ```cshtml
    <BitCheckbox Label="One-way checked (Fixed)" Value="true" />

    <BitCheckbox Label="One-way" Value="oneWayValue" />
    <BitToggleButton @bind-IsChecked="oneWayValue" Text="Toggle" />

    <BitCheckbox Label="Two-way controlled checkbox" @bind-Value="twoWayValue" />
    <BitToggleButton @bind-IsChecked="twoWayValue" Text="Toggle" />

    <BitCheckbox Label="One-way indeterminate (Fixed)" Indeterminate />

    <BitCheckbox Label="One-way indeterminate" Indeterminate="oneWayIndeterminate" />
    <BitToggleButton @bind-IsChecked="oneWayIndeterminate" Text="Toggle" />

    <BitCheckbox Label="Two-way indeterminate" @bind-Indeterminate="twoWayIndeterminate" />
    <BitToggleButton @bind-IsChecked="twoWayIndeterminate" Text="Toggle" />
    ```
    ```csharp
    @code {
        private bool oneWayValue;
        private bool twoWayValue;
        private bool oneWayIndeterminate = true;
        private bool twoWayIndeterminate = true;
    }
    ```

**7. Validation**

*   **Description**: Shows using `BitCheckbox` within an `EditForm` and validating its state (e.g., requiring it to be checked) using data annotations like `[Range(typeof(bool), "true", "true", ...)]`.
*   **Code**: (Includes CSS for context)
    ```css
    .validation-message { color: red; font-size: 0.75rem; }
    ```
    ```cshtml
    <EditForm Model="validationModel" OnValidSubmit="HandleValidSubmit" OnInvalidSubmit="HandleInvalidSubmit">
        <DataAnnotationsValidator />
        <BitCheckbox Label="I agree with the terms and conditions."
                     @bind-Value="validationModel.TermsAgreement" />
        <ValidationMessage For="@(() => validationModel.TermsAgreement)" />

        <BitButton ButtonType="BitButtonType.Submit">Submit</BitButton>
    </EditForm>
    ```
    ```csharp
    @code {
        private BitCheckboxValidationModel validationModel = new();

        public class BitCheckboxValidationModel
        {
            [Range(typeof(bool), "true", "true", ErrorMessage = "You must agree to the terms and conditions.")]
            public bool TermsAgreement { get; set; }
        }

        private async Task HandleValidSubmit() { /* Logic for valid submission */ }
        private void HandleInvalidSubmit() { /* Logic for invalid submission */ }
    }
    ```

**8. Custom content**

*   **Description**: Demonstrates replacing the default checkbox visual entirely by providing custom `ChildContent`. This allows using icons or other elements to represent the checked, unchecked, and indeterminate states.
*   **Code**:
    ```cshtml
    <BitCheckbox @bind-Value="customCheckboxValue">
        <BitIcon Style="border:1px solid gray;width:22px;height:22px"
                 IconName="@(customCheckboxValue ? BitIconName.Accept : null)" />
        <span>Custom basic checkbox</span>
    </BitCheckbox>

    <BitCheckbox @bind-Value="customContentValue" @bind-Indeterminate="customContentIndeterminate">
        <BitIcon Style="border:1px solid gray;width:22px;height:22px"
                 IconName="@(customContentIndeterminate ? BitIconName.Fingerprint : (customContentValue ? BitIconName.Accept : null))" />
        <span>Custom indeterminate checkbox</span>
    </BitCheckbox>
    <BitButton OnClick="@(() => customContentIndeterminate = true)">Make Indeterminate</BitButton>
    ```
    ```csharp
    @code {
        private bool customCheckboxValue;
        private bool customContentValue;
        private bool customContentIndeterminate = true;
    }
    ```

**9. Size**

*   **Description**: Shows the different visual sizes available for the checkbox: `Small`, `Medium` (default), and `Large`, applied using the `Size` parameter. Examples show each size in unchecked, indeterminate, and checked states.
*   **Code**:
    ```cshtml
    <BitCheckbox Size="BitSize.Small" Label="Checkbox" />
    <BitCheckbox Size="BitSize.Small" Label="Checkbox" Indeterminate />
    <BitCheckbox Size="BitSize.Small" Label="Checkbox" Value />

    <BitCheckbox Size="BitSize.Medium" Label="Checkbox" />
    <BitCheckbox Size="BitSize.Medium" Label="Checkbox" Indeterminate />
    <BitCheckbox Size="BitSize.Medium" Label="Checkbox" Value />

    <BitCheckbox Size="BitSize.Large" Label="Checkbox" />
    <BitCheckbox Size="BitSize.Large" Label="Checkbox" Indeterminate />
    <BitCheckbox Size="BitSize.Large" Label="Checkbox" Value />
    ```

**10. Color**

*   **Description**: Displays checkboxes using various `BitColor` options (`Primary`, `Secondary`, `Tertiary`, `Info`, `Success`, `Warning`, `SevereWarning`, `Error`, and background/foreground/border variations) in unchecked, indeterminate, and checked states.
*   **Code**: (Shows pattern for one color - Primary)
    ```cshtml
    <BitCheckbox Color="BitColor.Primary" Label="Primary" />
    <BitCheckbox Color="BitColor.Primary" Label="Primary" Indeterminate />
    <BitCheckbox Color="BitColor.Primary" Label="Primary" Value />

    @* ... other colors follow the same pattern ... *@
    ```

**11. Style & Class**

*   **Description**: Demonstrates applying custom styling using inline `Style`, root `Class`, and the `Styles` and `Classes` parameters for targeted customization of internal elements (Root, Checked, Box, Icon, Label).
*   **Code**: (Includes CSS for context)
    ```css
    .custom-class { padding: 0.5rem; border-radius: 0.125rem; background-color: #d3d3d347; border: 1px solid dodgerblue; }

    /* Styles for the 'Classes' parameter example */
    .custom-label { font-weight: bold; color: lightseagreen; }
    .custom-icon { color: lightseagreen; }
    .custom-box { border-radius: 0.2rem; border-color: lightseagreen; }
    .custom-checked .custom-icon { color: white; }
    .custom-checked:hover .custom-icon { color: whitesmoke; }
    .custom-checked .custom-box { background-color: lightseagreen; }
    .custom-checked:hover .custom-box { border-color: mediumseagreen; }
    ```
    ```cshtml
    <BitCheckbox Label="Styled checkbox" Style="color: dodgerblue; text-shadow: lightskyblue 0 0 1rem;" />
    <BitCheckbox Label="Classed checkbox" Class="custom-class" />

    <BitCheckbox Label="Styles"
                 Styles="@(new() { Checked = "--check-color: deeppink; --icon-color: white;",
                                   Label = "color: var(--check-color);",
                                   Box = "border-radius: 50%; border-color: var(--check-color); background-color: var(--check-color);",
                                   Icon = "color: var(--icon-color);" })" />

    <BitCheckbox Label="Classes"
                 Classes="@(new() { Checked = "custom-checked",
                                    Icon = "custom-icon",
                                    Label= "custom-label",
                                    Box = "custom-box" })" />
    ```

**12. RTL**

*   **Description**: Shows how to render the checkbox and its label in a right-to-left layout using `Dir="BitDir.Rtl"`.
*   **Code**:
    ```cshtml
    <BitCheckbox Dir="BitDir.Rtl" Label="چکباکس راست به چپ" />
    <BitCheckbox Dir="BitDir.Rtl" Label="چکباکس غیرفعال" IsEnabled="false" />
    <BitCheckbox Dir="BitDir.Rtl" Label="چکباکس غیرفعال چک شده" IsEnabled="false" Value="true" />
    ```

---

## API Reference

**BitCheckbox Parameters**

| Name                 | Type                            | Default        | Description                                                                               |
| :------------------- | :------------------------------ | :------------- | :---------------------------------------------------------------------------------------- |
| `AriaDescription`    | `string?`                       | `null`         | Detailed description for screen readers.                                                |
| `AriaLabelledby`     | `string?`                       | `null`         | ID of an element labeling the checkbox.                                                 |
| `AriaPositionInSet`  | `int?`                          | `null`         | `aria-posinset` value if the checkbox is part of a set.                                   |
| `AriaSetSize`        | `int?`                          | `null`         | `aria-setsize` value if the checkbox is part of a set.                                    |
| `CheckIconName`      | `string`                        | `Accept`       | Custom icon name for the checked state (default is a checkmark).                          |
| `CheckIconAriaLabel` | `string?`                       | `null`         | Aria label for the check icon.                                                            |
| `ChildContent`       | `RenderFragment?`               | `null`         | Custom content to replace the default checkbox visual and label.                          |
| `Classes`            | `BitCheckboxClassStyles?`       | `null`         | Custom CSS classes for different parts (Root, Container, Box, Icon, Label, Checked).      |
| `Color`              | `BitColor?`                     | `null`         | The general color theme of the checkbox.                                                  |
| `DefaultIndeterminate`| `bool?`                        | `null`         | Initial indeterminate state (uncontrolled).                                               |
| `DefaultValue`       | `bool?`                         | `null`         | Initial checked state (uncontrolled).                                                   |
| `Indeterminate`      | `bool`                          | `false`        | Sets the indeterminate state (takes visual precedence over `Value`). Use `@bind-Indeterminate`. |
| `Label`              | `string?`                       | `null`         | The text label displayed next to the checkbox.                                            |
| `LabelTemplate`      | `RenderFragment?`               | `null`         | Custom template for the checkbox label content.                                           |
| `Name`               | `string?`                       | `null`         | `name` attribute for the hidden input element, used in forms.                             |
| `OnClick`            | `EventCallback<MouseEventArgs>` |                | Callback executed when the checkbox container (usually the label) is clicked.             |
| `Reversed`           | `bool`                          | `false`        | If true, renders the label before the checkbox visual.                                    |
| `Size`               | `BitSize?`                      | `null`         | The visual size of the checkbox (`Small`, `Medium`, `Large`).                             |
| `Styles`             | `BitCheckboxClassStyles?`       | `null`         | Custom CSS styles for different parts.                                                    |
| `Title`              | `string?`                       | `null`         | Tooltip text applied to the root element.                                                 |
| *(Inherited)*        | *(See BitInputBase)*            |                |                                                                                           |

**BitInputBase Parameters (Inherited)**

| Name                | Type                              | Default              | Description                                                                    |
| :------------------ | :-------------------------------- | :------------------- | :----------------------------------------------------------------------------- |
| `DisplayName`       | `string?`                         | `null`               | Display name for validation messages.                                          |
| `InputHtmlAttributes`| `IReadOnlyDictionary<string, object>?`| `null`               | Additional attributes applied to the hidden input element.                     |
| `Name`              | `string?`                         | `null`               | Overridden by `BitCheckbox.Name`.                                              |
| `NoValidate`        | `bool`                            | `false`              | Disables validation.                                                           |
| `OnChange`          | `EventCallback<bool?>`            |                      | Callback when the bound `Value` changes.                                       |
| `ReadOnly`          | `bool`                            | `false`              | Makes the input read-only (prevents user interaction changing the state).      |
| `Required`          | `bool`                            | `false`              | Marks the input as required (visual cue, use validation attributes for logic). |
| `Value`             | `bool?`                           | `null`               | The checked state (use `@bind-Value`).                                         |
| *(Inherited)*       | *(See BitComponentBase)*          |                      |                                                                                |

**BitComponentBase Parameters (Inherited)**

| Name           | Type                         | Default                   | Description                                                           |
| :------------- | :--------------------------- | :------------------------ | :-------------------------------------------------------------------- |
| `AriaLabel`    | `string?`                    | `null`                    | Aria-label for the root element.                                      |
| `Class`        | `string?`                    | `null`                    | Custom CSS class for the root element.                                |
| `Dir`          | `BitDir?`                    | `null`                    | Component direction (`Ltr`, `Rtl`, `Auto`).                           |
| `HtmlAttributes`| `Dictionary<string, object>` | `new Dictionary<>()`      | Additional HTML attributes for the root element.                        |
| `Id`           | `string?`                    | `null`                    | Custom ID for the root element (defaults to `UniqueId`).              |
| `IsEnabled`    | `bool`                       | `true`                    | Whether the component is enabled.                                     |
| `Style`        | `string?`                    | `null`                    | Custom CSS style for the root element.                                |
| `Visibility`   | `BitVisibility`              | `BitVisibility.Visible`   | Component visibility (`Visible`, `Hidden`, `Collapsed`).              |

**BitComponentBase Public Members (Inherited)**

| Name        | Type               | Default          | Description                                       |
| :---------- | :----------------- | :--------------- | :------------------------------------------------ |
| `UniqueId`  | `Guid`             | `Guid.NewGuid()` | Readonly unique ID assigned at construction.      |
| `RootElement` | `ElementReference` |                  | `ElementReference` for the root DOM element.    |

**BitCheckboxClassStyles Properties (for `Classes`/`Styles`)**

| Name      | Type      | Default | Description                                                            |
| :-------- | :-------- | :------ | :--------------------------------------------------------------------- |
| `Root`      | `string?` | `null`  | CSS class/style for the root `div` element.                          |
| `Container` | `string?` | `null`  | CSS class/style for the container `label` element.                     |
| `Checked`   | `string?` | `null`  | CSS class/style applied to the root element when checked/indeterminate. |
| `Box`       | `string?` | `null`  | CSS class/style for the checkbox visual box element (`div`).           |
| `Icon`      | `string?` | `null`  | CSS class/style for the checkmark/indeterminate icon (`i`).          |
| `Label`     | `string?` | `null`  | CSS class/style for the label text element (`span`).                   |

**Enums**

*   **BitColor**: Defines color options (`Primary`, `Secondary`, `Tertiary`, `Info`, `Success`, `Warning`, `SevereWarning`, `Error`, `PrimaryBackground`, `SecondaryBackground`, `TertiaryBackground`, `PrimaryForeground`, `SecondaryForeground`, `TertiaryForeground`, `PrimaryBorder`, `SecondaryBorder`, `TertiaryBorder`).
*   **BitSize**: Defines size options (`Small`, `Medium`, `Large`).
*   **BitVisibility**: Defines visibility states (`Visible`, `Hidden`, `Collapsed`).
*   **BitDir**: Defines text direction (`Ltr`, `Rtl`, `Auto`).

---

## Feedback

*   Provide feedback via the **GitHub repo**: [File an Issue](https://github.com/bitfoundation/bitplatform/issues/new/choose) or [Start a Discussion](https://github.com/bitfoundation/bitplatform/discussions/new/choose).
*   Review/Edit this demo page: [Review](https://github.com/bitfoundation/bitplatform/blob/develop/src/BlazorUI/Demo/Client/Bit.BlazorUI.Demo.Client.Core/Pages/Components/Inputs/Checkbox/BitCheckboxDemo.razor) / [Edit](https://github.com/bitfoundation/bitplatform/edit/develop/src/BlazorUI/Demo/Client/Bit.BlazorUI.Demo.Client.Core/Pages/Components/Inputs/Checkbox/BitCheckboxDemo.razor)
*   Review/Edit the component source: [Review](https://github.com/bitfoundation/bitplatform/blob/develop/src/BlazorUI/Bit.BlazorUI/Components/Inputs/Checkbox/BitCheckbox.razor) / [Edit](https://github.com/bitfoundation/bitplatform/edit/develop/src/BlazorUI/Bit.BlazorUI/Components/Inputs/Checkbox/BitCheckbox.razor)

