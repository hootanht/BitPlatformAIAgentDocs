# BitToggle Component Reference (`.NET Blazor - Bit Blazor UI`)

## Overview

**Component Name:** `BitToggle`
**Alias:** `Switch`

The `BitToggle` component functions as a physical switch, allowing users to choose between two mutually exclusive options (typically On/Off or True/False). It's commonly used for settings or options where the change should take effect immediately.

## Core Concepts & Features

*   **Boolean State:** Represents a boolean (`true`/`false`) value.
*   **Labeling:** Supports a primary `Label` and optional state-specific text (`OnText`, `OffText`, `Text`).
*   **Layout:**
    *   Default: Label appears above the toggle switch.
    *   `Inline`: Label and switch appear on the same line.
    *   `Reversed`: Swaps the position of the label and the switch.
    *   `FullWidth`: (Primarily effective with `Inline`) Makes the component occupy the full width, distributing space between the label and the switch.
*   **Customization:**
    *   `LabelTemplate`: Allows custom rendering of the label content.
    *   `Styles` / `Classes`: Provides fine-grained control over the appearance of internal elements (root, button, thumb, text).
*   **Data Binding:** Supports standard Blazor one-way (`Value`) and two-way (`@bind-Value`) data binding.
*   **Validation:** Integrates with Blazor's `EditForm` and validation system.
*   **Accessibility:** Implements `role="switch"` and associates the label correctly (`aria-labelledby`, `aria-checked`).
*   **States:** Supports `Enabled` and `Disabled` states.
*   **RTL Support:** Supports Right-to-Left text direction via the `Dir` property.

## Usage Examples

Below are examples demonstrating common configurations and features of the `BitToggle`.

---

### Example 1: Basic Usage

Displays a simple `BitToggle` with a label and another one in a disabled state.

```cshtml
<BitToggle Label="Basic" />
<BitToggle Label="Disabled" IsEnabled="false" />
```

---

### Example 2: Custom Texts

Demonstrates customizing the text displayed next to the toggle switch based on its state using `Text`, `OnText`, and `OffText`.

* `Text`: A single text displayed regardless of the state (if `OnText`/`OffText` are not set).
* `OnText` / `OffText`: Specific texts displayed for the checked (true) and unchecked (false) states, respectively.

```cshtml
<BitToggle Label="Text" Text="This is a toggle!" />
<BitToggle Label="OnText & OffText" OnText="Toggle is On" OffText="Toggle is Off" />
```

---

### Example 3: Label Customization

Shows how to render the label inline with the toggle switch (`Inline` property) and how to use `LabelTemplate` for custom label rendering (e.g., adding icons or specific styling).

```cshtml
<BitToggle Label="This is an inline label" Inline />

<BitToggle>
    <LabelTemplate>
        <div style="display:flex; align-items:center; gap:10px">
            <BitLabel Style="color:green">This is custom Label</BitLabel>
            <BitIcon IconName="@BitIconName.Filter" />
        </div>
    </LabelTemplate>
</BitToggle>
```

---

### Example 4: Reversed Layout

Demonstrates the `Reversed` property, which places the toggle switch *before* the label, both in default block layout and inline layout.

```cshtml
<BitToggle Label="This is a reversed label" Reversed />

<BitToggle Label="This is a reversed inline label" Reversed Inline />
```

---

### Example 5: Full Width Layout

Illustrates the `FullWidth` property, typically used with `Inline`, to make the toggle component span the available width, pushing the label and switch to opposite ends.

```cshtml
<BitToggle Label="This is a full-width toggle" FullWidth Inline />

<BitToggle Label="This is a reversed full-width toggle" Reversed FullWidth Inline />

@* Example with custom LabelTemplate using FullWidth *@
<BitToggle FullWidth Inline>
    <LabelTemplate>
        <BitActionButton Class="bit-acb-fwi">go go go</BitActionButton> @* Example: Button fills label space *@
    </LabelTemplate>
</BitToggle>
```

---

### Example 6: Data Binding

Shows how to bind the toggle's boolean state to a C# variable using one-way (`Value`) and two-way (`@bind-Value`) binding. A `BitToggleButton` is included to demonstrate external control over the bound variable.

```cshtml
<BitToggle Label="One-way" Value="oneWayValue" />
<BitToggleButton @bind-IsChecked="oneWayValue" OnText="On" OffText="Off" />

<br/><br/>

<BitToggle Label="Two-way" @bind-Value="twoWayValue" />
<BitToggleButton @bind-IsChecked="twoWayValue" OnText="On" OffText="Off" />
```

```csharp
@code {
    private bool oneWayValue;
    private bool twoWayValue;
}
```

---

### Example 7: Style & Class Customization

Demonstrates customizing the appearance using the `Styles` and `Classes` parameters, targeting specific internal elements like the `Thumb`, `Button`, and `Checked` state.

```cshtml
<style>
    /* Example CSS for the 'Classes' demo */
    .custom-thumb {
        background: #fff;
        width: 30px;
        height: 30px;
    }

    .custom-button {
        padding: 0;
        width: 52px;
        height: 22px;
        border: none;
        background: #ccc;
        border-radius: 11px;
    }

    /* Styles applied when the toggle is checked via the 'Checked' class */
    .custom-check .custom-thumb {
        background: #ff6868;
    }
    .custom-check .custom-button {
        background: #ffcece;
    }
    .custom-check .custom-button:hover .custom-thumb {
        background: #ff6868; /* Example hover effect */
    }
</style>

<BitToggle Label="Styles"
           Styles="@(new() { Root = "--toggle-background: lightgray;", /* Using CSS variable */
                             Checked = "--toggle-background: #2ecc71;", /* Override variable when checked */
                             Thumb = "background: whitesmoke; height: 28px; width: 28px;",
                             Button = "background: var(--toggle-background); border: none; border-radius: 60px; padding: 0; height: 30px; width: 50px;" })" />

<BitToggle Label="Classes"
           Classes="@(new() { Thumb = "custom-thumb",
                              Button = "custom-button",
                              Checked = "custom-check" })" />
```

---

### Example 8: Validation

Shows how to use `BitToggle` within a Blazor `EditForm` for validation. In this example, the toggle represents agreement to terms, and a `[Range]` attribute ensures it must be `true` for the form to be valid.

```cshtml
<style>
    .validation-message { color: red; }
</style>

<EditForm Model="validationModel" OnValidSubmit="HandleValidSubmit" OnInvalidSubmit="HandleInvalidSubmit">
    <DataAnnotationsValidator />

    <BitToggle Label="Terms and conditions" Text="I agree." @bind-Value="validationModel.TermsAgreement" />
    <ValidationMessage For="@(() => validationModel.TermsAgreement)" />

    <br/>
    <BitButton ButtonType="BitButtonType.Submit">Submit</BitButton>
</EditForm>
```

```csharp
@code {
    public class BitToggleValidationModel
    {
        // Ensures the bool must be 'true' to be valid.
        [Range(typeof(bool), "true", "true", ErrorMessage = "You must agree to the terms and conditions.")]
        public bool TermsAgreement { get; set; } // Default can be false or true depending on initial state needed
    }

    public BitToggleValidationModel validationModel { get; set; } = new();

    private async Task HandleValidSubmit() {
        Console.WriteLine("Form Valid!");
        // Handle form submission
    }

    private void HandleInvalidSubmit() {
        Console.WriteLine("Form Invalid!");
        // Handle validation errors
    }
}
```

---

### Example 9: RTL (Right-to-Left) Support

Demonstrates using `BitToggle` in a Right-to-Left layout by setting `Dir="BitDir.Rtl"`. The `Reversed` property interacts predictably with RTL mode.

```cshtml
<div dir="rtl"> @* Container div sets overall direction *@

    <BitToggle Label="این یک تاگل است" Dir="BitDir.Rtl" OnText="روشن" OffText="خاموش" />
    <br/><br/>
    <BitToggle Label="این یک تاگل خطی است" Dir="BitDir.Rtl" Inline />
    <br/><br/>
    <BitToggle Label="این یک تاگل خطی برعکس است" Dir="BitDir.Rtl" Reversed Inline />

</div>
```

---

## API Reference

### `BitToggle` Parameters

Parameters specific to or overriding behavior for the `BitToggle` component.

| Name          | Type                     | Default Value | Description                                                                                              |
| :------------ | :----------------------- | :------------ | :------------------------------------------------------------------------------------------------------- |
| `Classes`     | `BitToggleClassStyles?`  | `null`        | Custom CSS classes for different parts of the toggle. See `BitToggleClassStyles` section below.          |
| `DefaultValue`| `bool?`                  | `null`        | The initial value of the toggle if `Value` is not bound. `false` if `null`.                              |
| `FullWidth`   | `bool`                   | `false`       | If `true` (and typically `Inline="true"`), renders the toggle across the full container width, spacing out the label and switch. |
| `Inline`      | `bool`                   | `false`       | If `true`, renders the label and the switch knob on the same line.                                        |
| `Label`       | `string?`                | `null`        | The primary text label associated with the toggle.                                                       |
| `LabelTemplate`| `RenderFragment?`        | `null`        | Custom `RenderFragment` to render the label content. Overrides the `Label` string.                       |
| `OffText`     | `string?`                | `null`        | Text displayed next to the switch knob when the toggle state is `false` (off).                             |
| `OnText`      | `string?`                | `null`        | Text displayed next to the switch knob when the toggle state is `true` (on).                              |
| `Reversed`    | `bool`                   | `false`       | If `true`, the switch knob is rendered before the label.                                                  |
| `Role`        | `string`                 | `"switch"`    | The ARIA `role` attribute for the toggle button. Default is `"switch"`.                                  |
| `Styles`      | `BitToggleClassStyles?`  | `null`        | Custom CSS inline styles for different parts of the toggle. See `BitToggleClassStyles` section below.    |
| `Text`        | `string?`                | `null`        | Default text displayed next to the switch knob. Used if `OnText` and `OffText` are not provided.           |
| **Inherited Parameters** |               |               | *Includes parameters from `BitInputBase<bool>` and `BitComponentBase` (see below).*                      |

---

### `BitInputBase<TValue>` Parameters (Inherited by `BitToggle`, where `TValue` is `bool`)

Base class for input components, handling value binding and validation integration.

| Name                | Type                                  | Default Value | Description                                                                                                         |
| :------------------ | :------------------------------------ | :------------ | :------------------------------------------------------------------------------------------------------------------ |
| `DisplayName`       | `string?`                             | `null`        | A user-friendly name for the field, used in validation error messages. If not set, derived from `ValueExpression`. |
| `InputHtmlAttributes` | `IReadOnlyDictionary<string, object>?`| `null`        | Additional HTML attributes to apply directly to the underlying hidden `<input type="checkbox">` element.        |
| `Name`              | `string?`                             | `null`        | The `name` attribute of the hidden input element, useful for form submission.                                     |
| `NoValidate`        | `bool`                                | `false`       | If `true`, suppresses the generation of validation attributes on the hidden input element.                      |
| `OnChange`          | `EventCallback<TValue?>` (`bool?`)    |               | A callback invoked when the `Value` changes (typically on click).                                                  |
| `ReadOnly`          | `bool`                                | `false`       | If `true`, makes the toggle appear visually interactive but prevents user changes (like disabled but focusable). |
| `Required`          | `bool`                                | `false`       | If `true`, adds styling cues. Validation logic relies on model attributes (e.g., `[Range(typeof(bool), "true", "true")]`). |
| `Value`             | `TValue?` (`bool?`)                   | `null`        | The current boolean value (`true`/`false`) of the toggle. Use with `@bind-Value` for two-way data binding.     |
| `ValueChanged`      | `EventCallback<TValue?>` (`bool?`)    |               | An `EventCallback` used implicitly by `@bind-Value` for two-way binding updates.                                  |
| `ValueExpression`   | `Expression<Func<TValue?>>?`          | `null`        | An expression used implicitly by `@bind-Value` to identify the bound property, enabling validation integration. |

---

### `BitInputBase<TValue>` Public Members (Inherited by `BitToggle`)

| Name                      | Type                 | Description                                                                                                         |
| :------------------------ | :------------------- | :------------------------------------------------------------------------------------------------------------------ |
| `InputElement`            | `ElementReference`   | Provides a reference to the underlying hidden `<input type="checkbox">` element. *Note: Less useful for `BitToggle` styling/interaction compared to the button.* |
| `FocusAsync()`            | `() => ValueTask`    | Programmatically sets focus to the toggle's focusable element (the button).                                       |
| `FocusAsync(bool preventScroll)` | `(bool) => ValueTask`| Programmatically sets focus, optionally preventing the browser from scrolling the element into view.             |

---

### `BitComponentBase` Parameters (Base for all Bit components, Inherited by `BitToggle`)

Common parameters for all Bit Blazor UI components.

| Name             | Type                            | Default Value                       | Description                                                                                                 |
| :--------------- | :------------------------------ | :---------------------------------- | :---------------------------------------------------------------------------------------------------------- |
| `AriaLabel`      | `string?`                       | `null`                              | Defines a string value that labels the toggle button element for accessibility, overriding the visual Label association if needed. |
| `Class`          | `string?`                       | `null`                              | Custom CSS class(es) to apply to the root element (`div`) of the component.                                 |
| `Dir`            | `BitDir?`                       | `null`                              | Sets the text direction (`ltr`, `rtl`, `auto`) for the component. See `BitDir` enum below.                    |
| `HtmlAttributes` | `Dictionary<string, object>`    | `new Dictionary<string, object>()`  | Allows capturing and rendering arbitrary HTML attributes (splatting) on the root element (`div`) of the component. |
| `Id`             | `string?`                       | `null`                              | Custom `id` attribute for the root element (`div`). If not provided, the component's `UniqueId` is used.      |
| `IsEnabled`      | `bool`                          | `true`                              | Whether the component is enabled. If `false`, it appears grayed out and cannot be interacted with.          |
| `Style`          | `string?`                       | `null`                              | Custom inline CSS style(s) to apply to the root element (`div`) of the component.                           |
| `Visibility`     | `BitVisibility`                 | `BitVisibility.Visible`             | Controls whether the component is visible, hidden (occupies space), or collapsed (no space). See `BitVisibility` enum below. |

---

### `BitComponentBase` Public Members (Base for all Bit components, Inherited by `BitToggle`)

| Name          | Type               | Default Value    | Description                                                                                                      |
| :------------ | :----------------- | :--------------- | :--------------------------------------------------------------------------------------------------------------- |
| `UniqueId`    | `Guid`             | `Guid.NewGuid()` | A read-only, unique identifier (GUID) generated automatically for each component instance. Useful for `id` refs. |
| `RootElement` | `ElementReference` |                  | Provides a reference to the root HTML element (`div`) of the component.                                          |

---

### `BitToggleClassStyles` Properties (Used by `Classes` and `Styles` parameters)

Defines CSS classes or styles for specific parts of the `BitToggle`.

| Property    | Type      | Description                                                                          | Maps to Element(s)       |
| :---------- | :-------- | :----------------------------------------------------------------------------------- | :----------------------- |
| `Root`      | `string?` | The main container `div` element.                                                    | Root `div`               |
| `Label`     | `string?` | The `<label>` element wrapping the `Label`/`LabelTemplate` content.                  | `<label>`                |
| `Container` | `string?` | The `div` containing the toggle button and the state text (`OnText`/`OffText`/`Text`). | `div.bit-tgl-cnt`        |
| `Button`    | `string?` | The `<button role="switch">` element representing the clickable switch area.          | `<button.bit-tgl-btn>`   |
| `Checked`   | `string?` | Class/style applied to the `Root` element when the toggle is checked (`true`).       | Root `div` (when checked)|
| `Thumb`     | `string?` | The `<span>` element representing the movable knob/thumb of the switch.             | `span.bit-tgl-sta`       |
| `Text`      | `string?` | The `<label>` element displaying the `OnText`, `OffText`, or `Text`.                 | `<label.bit-tgl-stx>`    |

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

* **Purpose:** Use `BitToggle` for settings or options that have two distinct states and where the result of changing the state is immediate. Avoid using it for actions that require a separate submission step (like in a form, unless validated as shown).
* **Clarity:** Ensure the `Label`, `OnText`, and `OffText` clearly communicate the purpose and state of the toggle. If `OnText`/`OffText` are used, they should explicitly state the *current* status (e.g., "Notifications On", "Notifications Off").
* **Accessibility:** The component handles ARIA roles and states (`role="switch"`, `aria-checked`). Always provide a meaningful `Label` or `LabelTemplate` that is correctly associated for screen readers. If the visual label is complex (like in `LabelTemplate`), ensure the primary textual meaning is still conveyed programmatically.
* **Validation:** When used in forms requiring the toggle to be 'on' (true), use validation attributes like `[Range(typeof(bool), "true", "true")]` on the bound model property. The `Required` parameter is less meaningful for a boolean toggle itself.
* **Layout:** Choose `Inline`, `Reversed`, and `FullWidth` options carefully based on the surrounding layout and desired visual flow. `FullWidth` generally requires `Inline` to be effective.
