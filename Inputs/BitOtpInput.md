# BitOtpInput Blazor Component

**Objective:** This document provides context and reference information about the `BitOtpInput` Blazor component, based *solely* on the provided HTML documentation extract. Use this information to understand the component's purpose, features, parameters, and usage.

**Key Component:** `BitOtpInput`

---

## Overview

`BitOtpInput` is used for Multi-Factor Authentication (MFA) procedures, allowing users to enter a one-time password (OTP). It presents a series of input boxes for entering the code digits.

---

## Usage Examples

**1. Basic**

*   **Description**: Demonstrates basic usage, including a standard 5-digit OTP input, a disabled version, a 4-digit version (`Length="4"`), auto-shifting focus between inputs (`AutoShift`), and auto-focusing the first input on render (`AutoFocus`).
*   **Code**:
    ```cshtml
    <BitOtpInput />
    <BitOtpInput IsEnabled="false" />
    <BitOtpInput Length="4" />
    <BitOtpInput AutoShift />
    <BitOtpInput AutoFocus />
    ```

**2. Label**

*   **Description**: Shows how to add a descriptive label above the OTP input fields using the `Label` parameter or a custom `LabelTemplate`.
*   **Code**:
    ```cshtml
    <BitOtpInput Label="OTP" />

    <BitOtpInput>
        <LabelTemplate>
            <BitStack Horizontal>
                <BitText Gutter><i>Custom label</i></BitText>
                <BitSpacer />
                <BitIcon IconName="@BitIconName.TemporaryAccessPass" />
            </BitStack>
        </LabelTemplate>
    </BitOtpInput>
    ```

**3. Type**

*   **Description**: Demonstrates setting the underlying HTML input `type` using the `Type` parameter, allowing for text (`Text`, default), numeric (`Number`), or password (`Password`) input behaviors.
*   **Code**:
    ```cshtml
    <BitOtpInput Label="Text" Type="BitInputType.Text" />
    <BitOtpInput Label="Number" Type="BitInputType.Number" />
    <BitOtpInput Label="Password" Type="BitInputType.Password" />
    ```

**4. Directions**

*   **Description**: Shows different layout directions for the input boxes: `Default` (horizontal, LTR based on parent/culture), `Reversed` (horizontal, inputs rendered right-to-left relative to each other), `Vertical`, and `Reversed Vertical`.
*   **Code**:
    ```cshtml
    <BitOtpInput Label="Default" />
    <BitOtpInput Label="Reversed" Reversed />
    <BitOtpInput Label="Vertical" Vertical />
    <BitOtpInput Label="Reversed Vertical" Vertical Reversed />
    ```

**5. Binding**

*   **Description**: Illustrates one-way (`Value`) and two-way (`@bind-Value`) data binding to synchronize the entered OTP value with a C# variable.
*   **Code**:
    ```cshtml
    <BitOtpInput Label="One-way" Value="@oneWayValue" />
    <BitTextField Style="margin-top: 5px;" @bind-Value="oneWayValue" />

    <BitOtpInput Label="Two-way" @bind-Value="@twoWayValue" />
    <BitTextField Style="margin-top: 5px;" @bind-Value="twoWayValue" />
    ```
    ```csharp
    @code {
        private string? oneWayValue;
        private string? twoWayValue;
    }
    ```

**6. Events**

*   **Description**: Demonstrates handling various events: `OnChange` (when the value changes), `OnFill` (when all inputs are filled), `OnFocusIn`, `OnFocusOut`, `OnInput`, `OnKeyDown`, and `OnPaste`. Event arguments often include the specific input index.
*   **Code**:
    ```cshtml
    <BitOtpInput Label="OnChange" OnChange="v => onChangeValue = v" />
    <div>OnChange value: @onChangeValue</div>

    <BitOtpInput Label="OnFill" OnFill="v => onFillValue = v" />
    <div>OnFill value: @onFillValue</div>

    <BitOtpInput Label="OnFocusIn" OnFocusIn="args => onFocusInArgs = args" />
    <div>Focus type: @onFocusInArgs?.Event.Type</div>
    <div>Input index: @onFocusInArgs?.Index</div>

    <BitOtpInput Label="OnFocusOut" OnFocusOut="args => onFocusOutArgs = args" />
    <div>Focus type: @onFocusOutArgs?.Event.Type</div>
    <div>Input index: @onFocusOutArgs?.Index</div>

    <BitOtpInput Label="OnInput" OnInput="args => onInputArgs = args" />
    <div>Value: @onInputArgs?.Event.Value</div>
    <div>Input index: @onInputArgs?.Index</div>

    <BitOtpInput Label="OnKeyDown" OnKeyDown="args => onKeyDownArgs = args" />
    <div>Key & Code: [@onKeyDownArgs?.Event.Key] [@onKeyDownArgs?.Event.Code]</div>
    <div>Input index: @onKeyDownArgs?.Index</div>

    <BitOtpInput Label="OnPaste" OnPaste="args => onPasteArgs = args" />
    <div>Focus type: @onPasteArgs?.Event.Type</div>
    <div>Input index: @onPasteArgs?.Index</div>
    ```
    ```csharp
    @code {
        private string? onChangeValue;
        private string? onFillValue;
        private (FocusEventArgs Event, int Index)? onFocusInArgs;
        private (FocusEventArgs Event, int Index)? onFocusOutArgs;
        private (ChangeEventArgs Event, int Index)? onInputArgs;
        private (KeyboardEventArgs Event, int Index)? onKeyDownArgs;
        private (ClipboardEventArgs Event, int Index)? onPasteArgs;
    }
    ```

**7. Validation**

*   **Description**: Shows integrating `BitOtpInput` with Blazor's `EditForm` and `DataAnnotationsValidator` for validation (e.g., requiring a value and enforcing a minimum length).
*   **Code**: (Includes CSS for context)
    ```css
    .validation-message { color: red; font-size: 0.75rem; }
    ```
    ```cshtml
    <EditForm Model="validationOtpInputModel" OnValidSubmit="HandleValidSubmit" OnInvalidSubmit="HandleInvalidSubmit">
        <DataAnnotationsValidator />

        <BitOtpInput Length="6" @bind-Value="validationOtpInputModel.OtpValue" />
        <ValidationMessage For="() => validationOtpInputModel.OtpValue" />

        <BitButton Style="margin-top: 10px;" ButtonType="BitButtonType.Submit">Submit</BitButton>
    </EditForm>
    ```
    ```csharp
    @using System.ComponentModel.DataAnnotations;

    @code {
        public class ValidationOtpInputModel
        {
            [Required(ErrorMessage = "The OTP value is required.")]
            [MinLength(6, ErrorMessage = "Minimum length is 6.")]
            public string OtpValue { get; set; }
        }

        private ValidationOtpInputModel validationOtpInputModel = new();

        private void HandleValidSubmit() { /* Logic for valid submission */ }
        private void HandleInvalidSubmit() { /* Logic for invalid submission */ }
    }
    ```

**8. Size**

*   **Description**: Demonstrates setting the visual size of the input boxes using the `Size` parameter (`Small`, `Medium`, `Large`).
*   **Code**:
    ```cshtml
    <BitOtpInput Label="Small" Size="BitSize.Small" />
    <BitOtpInput Label="Medium" Size="BitSize.Medium" />
    <BitOtpInput Label="Large" Size="BitSize.Large" />
    ```

**9. Style & Class**

*   **Description**: Shows applying custom styling using inline `Style`, root `Class`, and the `Styles` and `Classes` parameters for targeted styling of internal elements (Root, Input, Focused state).
*   **Code**: (Includes CSS for context)
    ```css
    .custom-class { gap: 1rem; margin-inline: 1rem; }
    .custom-class input { border-radius: 0; border-width: 0 0 1px 0; border-color: lightseagreen; }

    /* Styles for the 'Classes' parameter example */
    .custom-root { margin-inline: 1rem; }
    .custom-input { border-radius: 50%; border: 1px solid tomato; }
    .custom-focused { border-color: red; box-shadow: tomato 0 0 1rem; } /* Applied to focused input */
    ```
    ```cshtml
    <BitOtpInput Style="margin-inline: 1rem; box-shadow: aqua 0 0 0.5rem;" />
    <BitOtpInput Class="custom-class" />

    <BitOtpInput Styles="@(new() { Root = "margin-inline: 1rem;",
                                   Input = "border-color: blueviolet;",
                                   Focused = "box-shadow: blueviolet 0 0 1rem;" })" />

    <BitOtpInput Label="Classes" @bind-Value="classesValue"
                 Classes="@(new() { Root = "custom-root",
                                    Input = "custom-input",
                                    Focused = "custom-focused" })" />
    ```

**10. RTL**

*   **Description**: Demonstrates rendering the component in right-to-left mode using `Dir="BitDir.Rtl"` or a cascading value.
*   **Code**:
    ```cshtml
    <CascadingValue Value="BitDir.Rtl">
        <BitOtpInput Label="برچسب در بالا" ShowButtons /> @* Example assumes ShowButtons was meant for NumberField, but kept for structure consistency *@
        <BitOtpInput Label="برچسب درخط" InlineLabel /> @* Example assumes InlineLabel was meant for NumberField, but kept for structure consistency *@
        <BitOtpInput Required />
        <BitOtpInput Label="الزامی" Required />
    </CascadingValue>
    ```

---

## API Reference

**BitOtpInput Parameters**

| Name                 | Type                           | Default        | Description                                                                             |
| :------------------- | :----------------------------- | :------------- | :-------------------------------------------------------------------------------------- |
| `AutoFocus`          | `bool`                         | `false`        | Auto-focuses the first input field on render.                                           |
| `AutoShift`          | `bool`                         | `false`        | Enables auto-shifting focus when clearing inputs with Backspace/Delete.               |
| `Classes`            | `BitOtpInputClassStyles?`      | `null`         | Custom CSS classes for different parts (Root, Label, InputsWrapper, Input, Focused).      |
| `Label`              | `string?`                      | `null`         | Label displayed above the inputs.                                                       |
| `LabelTemplate`      | `RenderFragment?`              | `null`         | Custom template for the label.                                                          |
| `Length`             | `int`                          | `5`            | Number of OTP input fields.                                                             |
| `OnFill`             | `EventCallback<string?>`       |                | Callback invoked when all inputs are filled.                                            |
| `OnFocusIn`          | `EventCallback<FocusEventArgs>`|                | Callback for the `onfocusin` event on any input.                                        |
| `OnFocusOut`         | `EventCallback<FocusEventArgs>`|                | Callback for the `onfocusout` event on any input.                                       |
| `OnInput`            | `EventCallback<ChangeEventArgs>`|                | Callback for the `oninput` event on any input.                                          |
| `OnKeyDown`          | `EventCallback<KeyboardEventArgs>`|             | Callback for the `onkeydown` event on any input.                                        |
| `OnPaste`            | `EventCallback<ClipboardEventArgs>`|           | Callback for the `onpaste` event on any input.                                          |
| `Reversed`           | `bool`                         | `false`        | Renders inputs in the opposite direction (e.g., right-to-left within the container).    |
| `Size`               | `BitSize?`                     | `null`         | Visual size of the inputs (`Small`, `Medium`, `Large`).                                 |
| `Styles`             | `BitOtpInputClassStyles?`      | `null`         | Custom CSS styles for different parts.                                                  |
| `Type`               | `BitInputType?`                | `Text`         | Input type (`Text`, `Number`, `Password`, etc.).                                        |
| `Vertical`           | `bool`                         | `false`        | Renders inputs vertically instead of horizontally.                                      |
| *(Inherited)*        | *(See BitInputBase)*           |                |                                                                                         |

**BitOtpInput Public Members**

| Name            | Type                 | Description                                                   |
| :-------------- | :------------------- | :------------------------------------------------------------ |
| `InputElements` | `ElementReference[]` | Array of `ElementReference` for each individual input element. |
| `FocusAsync`    | `(int) => ValueTask` | Method to programmatically focus a specific input by index. |
| *(Inherited)*   | *(See BitInputBase)* |                                                               |

**BitInputBase Parameters & Members (Inherited)**

*(Refer to the `BitCheckbox` reference file for details)*

**BitComponentBase Parameters & Members (Inherited)**

*(Refer to the `BitCheckbox` reference file for details)*

**BitOtpInputClassStyles Properties**

| Name          | Type      | Default | Description                                                       |
| :------------ | :-------- | :------ | :---------------------------------------------------------------- |
| `Root`        | `string?` | `null`  | CSS class/style for the root `div` element.                     |
| `Label`       | `string?` | `null`  | CSS class/style for the label element.                            |
| `InputsWrapper`| `string?` | `null`  | CSS class/style for the `div` wrapping all the input elements.  |
| `Input`       | `string?` | `null`  | CSS class/style applied to each individual `input` element.     |
| `Focused`     | `string?` | `null`  | CSS class/style applied to the specific `input` that has focus. |

**Enums**

*   **BitSize**: Defines size options (`Small`, `Medium`, `Large`).
*   **BitInputType**: Defines input types (`Text`, `Password`, `Number`, `Email`, `Tel`, `Url`).
*   **BitVisibility**: Defines visibility states (`Visible`, `Hidden`, `Collapsed`).
*   **BitDir**: Defines text direction (`Ltr`, `Rtl`, `Auto`).

---

## Feedback

*   Provide feedback via the **GitHub repo**: [File an Issue](https://github.com/bitfoundation/bitplatform/issues/new/choose) or [Start a Discussion](https://github.com/bitfoundation/bitplatform/discussions/new/choose).
*   Review/Edit this demo page: [Review](https://github.com/bitfoundation/bitplatform/blob/develop/src/BlazorUI/Demo/Client/Bit.BlazorUI.Demo.Client.Core/Pages/Components/Inputs/OtpInput/BitOtpInputDemo.razor) / [Edit](https://github.com/bitfoundation/bitplatform/edit/develop/src/BlazorUI/Demo/Client/Bit.BlazorUI.Demo.Client.Core/Pages/Components/Inputs/OtpInput/BitOtpInputDemo.razor)
*   Review/Edit the component source: [Review](https://github.com/bitfoundation/bitplatform/blob/develop/src/BlazorUI/Bit.BlazorUI/Components/Inputs/OtpInput/BitOtpInput.razor) / [Edit](https://github.com/bitfoundation/bitplatform/edit/develop/src/BlazorUI/Bit.BlazorUI/Components/Inputs/OtpInput/BitOtpInput.razor)

