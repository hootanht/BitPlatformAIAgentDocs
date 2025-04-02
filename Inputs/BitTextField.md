# BitTextField Component Reference (`.NET Blazor - Bit Blazor UI`)

## Overview

**Component Name:** `BitTextField`
**Alias:** `TextInput`

The `BitTextField` component provides a standard way for users to enter and edit text within a Blazor application. It is a versatile input element suitable for use in forms, modal dialogs, tables, and any other surface where text input is required. It corresponds to the standard HTML `<input type="text">` or `<textarea>` elements but offers enhanced features and styling consistent with the Bit Blazor UI library.

## Core Concepts & Features

*   **Basic Input:** Standard text entry field with label and placeholder support.
*   **States:** Supports `Enabled`, `Disabled`, `ReadOnly`, and `Required` states.
*   **Styling Variants:** Offers different visual styles:
    *   Default (bordered)
    *   `Underlined`
    *   `NoBorder`
*   **Multiline:** Can function as a `<textarea>` for multi-line input (`Multiline` property), with options for `Resizable` and setting the number of `Rows`.
*   **Icons:** Allows embedding an icon within the field using `IconName`.
*   **Prefix & Suffix:** Supports adding non-editable text (`Prefix`, `Suffix`) or custom content (`PrefixTemplate`, `SuffixTemplate`) before or after the input value.
*   **Password Input:** Can be set to `Type="BitInputType.Password"` for password fields, with an optional `CanRevealPassword` toggle.
*   **Data Binding:**
    *   Supports standard Blazor one-way (`Value`) and two-way (`@bind-Value`) data binding.
    *   Provides `OnChange` event callback.
    *   Offers control over update timing with `Immediate` (oninput), `DebounceTime`, and `ThrottleTime`.
*   **Value Processing:** Includes a `Trim` option to automatically remove leading/trailing whitespace.
*   **Customization:** Highly customizable via:
    *   Standard HTML attributes (`Style`, `Class`).
    *   Specific `Styles` and `Classes` objects for granular control over internal elements (Root, Label, Input, etc.).
    *   Template slots (`LabelTemplate`, `DescriptionTemplate`, etc.).
*   **Validation:** Integrates seamlessly with Blazor's `EditForm` and data annotation validators (`DataAnnotationsValidator`, `ValidationMessage`).
*   **Accessibility:** Designed with accessibility in mind, supporting `AriaLabel`, `Label` association, etc.
*   **RTL Support:** Supports Right-to-Left text direction via the `Dir` property.

## Usage Examples

Below are examples demonstrating common configurations and features of the `BitTextField`.

---

### Example 1: Basics

Displays various basic configurations for the `BitTextField`, including placeholders, disabled state, read-only mode, descriptions, required fields, max length, and auto-focus.

```cshtml
<BitTextField Label="Basic" />
<BitTextField Label="Placeholder" Placeholder="Enter a text..." />
<BitTextField Label="Disabled" IsEnabled="false" />
<BitTextField Label="ReadOnly" ReadOnly DefaultValue="This is ReadOnly" />
<BitTextField Label="Description" Description="This is Description" />
<BitTextField Label="Required" Required />
<BitTextField Label="MaxLength: 5" MaxLength="5" />
<BitTextField Label="Auto focused" AutoFocus />
```

---

### Example 2: Underlined Style

Showcases the `BitTextField` with an underlined style (`Underlined` property), including variations with placeholders, disabled state, and required fields.

```cshtml
<BitTextField Label="Basic" Underlined />
<BitTextField Label="Placeholder" Underlined Placeholder="Enter a text..." />
<BitTextField Label="Disabled" Underlined IsEnabled="false" />
<BitTextField Label="Required" Underlined Required />
```

---

### Example 3: No Border Style

Demonstrates `BitTextField` without borders (`NoBorder` property), including variations for disabled and required fields.

```cshtml
<BitTextField Label="Basic" Placeholder="Enter a text..." NoBorder />
<BitTextField Label="Disabled" Placeholder="Enter a text..." NoBorder IsEnabled="false" />
<BitTextField Label="Required" Placeholder="Enter a text..." NoBorder Required />
```

---

### Example 4: Multiline Text Field

Displays `BitTextField` in multiline mode (`Multiline` property), functioning as a `<textarea>`. Includes options for `Resizable`, fixed size (`Rows`), and setting the number of rows.

```cshtml
<BitTextField Label="Multiline" Multiline />
<BitTextField Label="Resizable" Multiline Resizable />
<BitTextField Label="Rows = 10" Multiline Rows="10" />
```

---

### Example 5: Icon Integration

Shows how to add icons to the `BitTextField` component using the `IconName` property with `BitIconName` enum values.

```cshtml
<BitTextField Label="Email" IconName="@BitIconName.EditMail" />
<BitTextField Label="Calendar" IconName="@BitIconName.Calendar" />
```

---

### Example 6: Prefix & Suffix

Demonstrates using `Prefix` and `Suffix` properties to add text elements before or after the input field. These are purely visual and not part of the bound value.

```cshtml
<BitTextField Label="Prefix" Prefix="https://" />
<BitTextField Label="Suffix" Suffix=".com" />
<BitTextField Label="Prefix and Suffix" Prefix="https://" Suffix=".com" />
<BitTextField Label="Disabled" Prefix="https://" Suffix=".com" IsEnabled="false" />
```

---

### Example 7: Custom Templates

Illustrates the use of custom `RenderFragment` templates for labels (`LabelTemplate`), descriptions (`DescriptionTemplate`), prefixes (`PrefixTemplate`), and suffixes (`SuffixTemplate`) to achieve highly customized appearances.

```cshtml
<BitTextField>
    <LabelTemplate>
        <BitLabel Style="color:coral">Custom Label</BitLabel>
    </LabelTemplate>
</BitTextField>

<BitTextField Label="Custom Description">
    <DescriptionTemplate>
        <BitLabel Style="color:coral">Description</BitLabel>
    </DescriptionTemplate>
</BitTextField>

<BitTextField Label="Custom Prefix">
    <PrefixTemplate>
        <BitLabel Style="color:coral;margin:0 5px">Prefix</BitLabel>
    </PrefixTemplate>
</BitTextField>

<BitTextField Label="Custom Suffix">
    <SuffixTemplate>
        <BitLabel Style="color:coral;margin:0 5px">Suffix</BitLabel>
    </SuffixTemplate>
</BitTextField>
```

---

### Example 8: Password Field

Shows `BitTextField` configured for password entry using `Type="BitInputType.Password"`. Includes an example with the `CanRevealPassword` property to add a toggle button for showing/hiding the password.

```cshtml
<BitTextField Label="Password" Type="BitInputType.Password" />
<BitTextField Label="Reveal Password" Type="BitInputType.Password" CanRevealPassword />
```

---

### Example 9: Data Binding Options

Demonstrates various data binding scenarios:

* One-way binding (`Value`).
* Two-way binding (`@bind-Value`).
* Using the `OnChange` event callback.
* Immediate updates (`Immediate` property, triggers on `oninput`).
* Debounced updates (`DebounceTime` property with `Immediate`).
* Throttled updates (`ThrottleTime` property with `Immediate`).

```cshtml
<BitTextField Label="One-way" Value="@oneWayValue" />
<div>Value: [@oneWayValue]</div>
<BitOtpInput Length="5" Style="margin-top: 5px;" @bind-Value="oneWayValue" /> @* Example using another input to modify value *@

<BitTextField Label="Two-way" @bind-Value="twoWayValue" />
<div>Value: [@twoWayValue]</div>
<BitOtpInput Length="5" Style="margin-top: 5px;" @bind-Value="twoWayValue" Immediate /> @* Example using another input to modify value *@

<BitTextField Label="OnChange" OnChange="(v) => onChangeValue = v" Immediate />
<BitLabel>Value: [@onChangeValue]</BitLabel>

<BitTextField Label="Immediate" @bind-Value="@immediateValue" Immediate />
<div>Value: [@immediateValue]</div>

<BitTextField Label="Debounce" @bind-Value="@debounceValue" Immediate DebounceTime="300" />
<div>Value: [@debounceValue]</div>

<BitTextField Label="Throttle" @bind-Value="@throttleValue" Immediate ThrottleTime="300" />
<div>Value: [@throttleValue]</div>
```

```csharp
@code {
    private string oneWayValue;
    private string twoWayValue;
    private string onChangeValue;
    private string? immediateValue;
    private string? debounceValue;
    private string? throttleValue;
}
```

---

### Example 10: Value Trimming

Shows the effect of the `Trim` property. When `Trim` is true, leading and trailing whitespace entered by the user is automatically removed from the bound value.

```cshtml
<BitTextField Label="Trimmed" Trim @bind-Value="trimmedValue" />
<pre>[@trimmedValue]</pre>

<BitTextField Label="Not Trimmed" @bind-Value="notTrimmedValue" />
<pre>[@notTrimmedValue]</pre>
```

```csharp
@code {
    private string trimmedValue;
    private string notTrimmedValue;
}
```

---

### Example 11: Style & Class Customization

Explores different ways to customize the appearance:

* Applying inline `Style` to the root element.
* Applying a custom CSS `Class` to the root element.
* Using the `Styles` object to apply inline styles to specific internal parts (e.g., `Label`, `Input`, `FieldGroup`).
* Using the `Classes` object to apply CSS classes to specific internal parts, allowing for complex styling defined in CSS.

*(Note: CSS definitions provided in the original HTML are assumed to be available)*

```cshtml
<style>
    /* Example CSS rules (simplified from original HTML) */
    .custom-class {
        overflow: hidden;
        margin-inline: 1rem;
        border-radius: 1rem;
        border: 2px solid brown;
        position: relative; /* Needed for pseudo-elements */
    }
    .custom-class *, .custom-class *::after { border: none; }
    .custom-class::after { /* Focus underline effect */ }
    .custom-class:focus::after { /* Focus underline effect */ }

    .custom-root { /* Custom root positioning/layout */ }
    .custom-label { /* Custom label positioning/styling */ }
    .custom-label-top { /* State for floating label */ }
    .custom-input { /* Custom input styling */ }
    .custom-field { /* Custom field group styling */ }
    .custom-field::after { /* Custom focus underline */ }
    .custom-focus .custom-field::after { /* Custom focus underline active state */ }
    .custom-focus .custom-label { /* Custom label active/focused state */ }
</style>

@* Component's Style & Class: *@
<BitTextField Style="box-shadow: aqua 0 0 1rem; margin-inline: 1rem;" />
<BitTextField Class="custom-class" />

@* Styles & Classes objects for granular control: *@
<BitTextField Label="Styles"
              Styles="@(new() { Root = "margin-inline: 1rem;",
                                Focused = "--focused-background: #b2b2b25a;", /* CSS Variable example */
                                FieldGroup = "background: var(--focused-background);",
                                Label = "text-shadow: aqua 0 0 1rem; font-weight: 900; font-size: 1.25rem;",
                                Input = "padding: 0.5rem;" })" />

<BitTextField @bind-Value="classesValue"
              Label="Classes"
              Classes="@(new() { Root = "custom-root",
                                 FieldGroup = "custom-field",
                                 Focused = "custom-focus",
                                 Input = "custom-input",
                                 Label = $"custom-label{(string.IsNullOrEmpty(classesValue) ? string.Empty : " custom-label-top")}" })" />
```

```csharp
@code {
    private string? classesValue;
}
```

---

### Example 12: Validation

Demonstrates how to integrate `BitTextField` with Blazor's built-in validation using `EditForm` and `DataAnnotationsValidator`. Validation rules are defined on a model class using attributes like `[Required]`, `[RegularExpression]`, `[EmailAddress]`, `[StringLength]`. `ValidationMessage` displays errors.

```cshtml
<style>
    .validation-message { color: red; } /* Default Blazor validation message style */
</style>

<EditForm Model="validationTextFieldModel" OnValidSubmit="HandleValidSubmit" OnInvalidSubmit="HandleInvalidSubmit" novalidate>
    <DataAnnotationsValidator />

    <BitTextField Label="Required" Required @bind-Value="validationTextFieldModel.Text" />
    <ValidationMessage For="() => validationTextFieldModel.Text" />

    <BitTextField Label="Numeric" @bind-Value="validationTextFieldModel.NumericText" />
    <ValidationMessage For="() => validationTextFieldModel.NumericText" />

    <BitTextField Label="Only chars" @bind-Value="validationTextFieldModel.CharacterText" />
    <ValidationMessage For="() => validationTextFieldModel.CharacterText" />

    <BitTextField Label="Email" @bind-Value="validationTextFieldModel.EmailText" />
    <ValidationMessage For="() => validationTextFieldModel.EmailText" />

    <BitTextField Label="3 < Length < 5" @bind-Value="validationTextFieldModel.RangeText" />
    <ValidationMessage For="() => validationTextFieldModel.RangeText" />

    <BitButton ButtonType="BitButtonType.Submit">Submit</BitButton>
</EditForm>
```

```csharp
@code {
    public class ValidationTextFieldModel
    {
        [Required(ErrorMessage = "This field is required.")]
        public string Text { get; set; }

        [RegularExpression(@"0*[1-9][0-9]*", ErrorMessage = "Only numeric values are allowed.")]
        public string NumericText { get; set; }

        [RegularExpression(@"^[a-zA-Z0-9.]*$", ErrorMessage = "Only letters(a-z), numbers(0-9), and period(.) are allowed.")]
        public string CharacterText { get; set; }

        [EmailAddress(ErrorMessage = "Invalid e-mail address.")]
        public string EmailText { get; set; }

        [StringLength(5, MinimumLength = 3, ErrorMessage = "The text length must be between 3 and 5 chars.")]
        public string RangeText { get; set; }
    }

    private ValidationTextFieldModel validationTextFieldModel = new();

    private void HandleValidSubmit() { Console.WriteLine("Form submitted successfully!"); }
    private void HandleInvalidSubmit() { Console.WriteLine("Form submission failed due to validation errors."); }
}
```

---

### Example 13: RTL (Right-to-Left) Support

Shows how to use `BitTextField` in a Right-to-Left layout by setting the `Dir="BitDir.Rtl"` property. The container `div` also has `dir="rtl"` for correct layout context.

```cshtml
<div dir="rtl"> @* Container div sets overall direction *@
    <BitTextField Dir="BitDir.Rtl"
                  Placeholder="پست الکترونیکی"
                  IconName="@BitIconName.EditMail" />

    <br/><br/>

    <BitTextField Underlined
                  Label="تقویم"
                  Dir="BitDir.Rtl"
                  IconName="@BitIconName.Calendar" />
</div>
```

---

## API Reference

### `BitTextField` Parameters

These are parameters specific to the `BitTextField` component or override base class parameters with specific behavior.

| Name                      | Type                                  | Default Value       | Description                                                                                                                                |
| :------------------------ | :------------------------------------ | :------------------ | :----------------------------------------------------------------------------------------------------------------------------------------- |
| `AutoComplete`            | `string?`                             | `null`              | Maps to the `autocomplete` attribute of the HTML input element.                                                                            |
| `CanRevealPassword`       | `bool`                                | `false`             | Whether to show the reveal password button for input `Type='Password'`.                                                                    |
| `Classes`                 | `BitTextFieldClassStyles?`            | `null`              | Custom CSS classes for different parts of the `BitTextField`. See `BitTextFieldClassStyles` section below.                                     |
| `DefaultValue`            | `string?`                             | `null`              | Initial value for uncontrolled components (when not using `@bind-Value`).                                                                  |
| `Description`             | `string?`                             | `null`              | Description displayed below the text field to provide additional details.                                                                  |
| `DescriptionTemplate`     | `RenderFragment?`                     | `null`              | Custom `RenderFragment` for the description area. Overrides the `Description` string.                                                       |
| `IconName`                | `string?`                             | `null`              | Name of the icon (from `BitIconName` enum or custom icon font) to show at the far right end.                                                |
| `InputMode`               | `BitInputMode?`                       | `null`              | Sets the `inputmode` HTML attribute, hinting at the type of virtual keyboard to display. See `BitInputMode` enum below.                    |
| `Label`                   | `string?`                             | `null`              | Label displayed above the text field. Associated with the input for screen readers.                                                        |
| `LabelTemplate`           | `RenderFragment?`                     | `null`              | Custom `RenderFragment` for the label. Overrides the `Label` string.                                                                       |
| `MaxLength`               | `int`                                 | `-1`                | Specifies the maximum number of characters allowed (`maxlength` attribute). `-1` indicates no limit.                                         |
| `Multiline`               | `bool`                                | `false`             | If `true`, renders a `<textarea>` instead of an `<input>`, allowing multi-line input.                                                      |
| `NoBorder`                | `bool`                                | `false`             | If `true`, the text field will not display its default border.                                                                             |
| `OnClick`                 | `EventCallback<MouseEventArgs>`       |                     | Callback for when the *input element itself* is clicked.                                                                                   |
| `OnFocus`                 | `EventCallback<FocusEventArgs>`       |                     | Callback for when focus enters the input element (allows event bubbling).                                                                  |
| `OnFocusIn`               | `EventCallback<FocusEventArgs>`       |                     | Callback for when focus enters the input element (does not bubble). Useful for focus tracking without parent interference.                   |
| `OnFocusOut`              | `EventCallback<FocusEventArgs>`       |                     | Callback for when focus leaves the input element.                                                                                          |
| `OnKeyDown`               | `EventCallback<KeyboardEventArgs>`    |                     | Callback for when a keyboard key is pressed down while the input is focused.                                                               |
| `OnKeyUp`                 | `EventCallback<KeyboardEventArgs>`    |                     | Callback for when a keyboard key is released while the input is focused.                                                                   |
| `Placeholder`             | `string?`                             | `null`              | Placeholder text displayed inside the input when it is empty.                                                                              |
| `Prefix`                  | `string?`                             | `null`              | Text displayed *before* the input field content, within the component border. This text is **not** included in the component's `Value`. |
| `PrefixTemplate`          | `RenderFragment?`                     | `null`              | Custom `RenderFragment` for the prefix area. Overrides the `Prefix` string.                                                                  |
| `Resizable`               | `bool`                                | `false`             | For `Multiline` text fields, whether the textarea is resizable by the user (adds a resize handle).                                         |
| `RevealPasswordAriaLabel` | `string?`                             | `null`              | Aria-label for the reveal password button (used when `CanRevealPassword` is true). Defaults to localized text if not provided.              |
| `Rows`                    | `int?`                                | `null`              | For `Multiline` text fields, specifies the initial number of visible text lines (maps to `rows` attribute). Defaults to 3 if `Multiline` is true and `Rows` is null. |
| `Styles`                  | `BitTextFieldClassStyles?`            | `null`              | Custom CSS inline styles for different parts of the `BitTextField`. See `BitTextFieldClassStyles` section below.                             |
| `Suffix`                  | `string?`                             | `null`              | Text displayed *after* the input field content, within the component border. This text is **not** included in the component's `Value`.    |
| `SuffixTemplate`          | `RenderFragment?`                     | `null`              | Custom `RenderFragment` for the suffix area. Overrides the `Suffix` string.                                                                  |
| `Trim`                    | `bool`                                | `false`             | If `true`, automatically removes leading and trailing whitespace from the `Value` when the input loses focus or the value changes.         |
| `Type`                    | `BitInputType`                        | `BitInputType.Text` | The type of the input field (e.g., `Text`, `Password`, `Number`). See `BitInputType` enum below.                                           |
| `Underlined`              | `bool`                                | `false`             | If `true`, the text field uses an underlined style instead of the default border/background style.                                         |
| **Inherited Parameters**  |                                       |                     | *Includes parameters from `BitTextInputBase`, `BitInputBase<string>`, and `BitComponentBase` (see following sections).*                   |

---

### `BitTextField` Public Members

Methods and properties accessible via `@ref`.

| Name           | Type               | Description                                                                    |
| :------------- | :----------------- | :----------------------------------------------------------------------------- |
| `InputElement` | `ElementReference` | Provides a reference to the underlying HTML `<input>` or `<textarea>` element. |
| `FocusAsync()` | `ValueTask`        | Programmatically sets focus to the input element of the `BitTextField`.        |

---

### `BitTextInputBase` Parameters (Inherited by `BitTextField`)

Base class specific to text-based inputs.

| Name           | Type      | Default Value | Description                                                                                                      |
| :------------- | :-------- | :------------ | :--------------------------------------------------------------------------------------------------------------- |
| `AutoComplete` | `string?` | `null`        | Specifies the value of the `autocomplete` attribute (Note: `BitTextField` also defines this).                    |
| `AutoFocus`    | `bool`    | `false`       | If `true`, the text input attempts to automatically focus when the component first renders.                      |
| `DebounceTime` | `int`     | `0`           | Delays the `OnChange`/`ValueChanged` notification until `DebounceTime` milliseconds have passed without input. Requires `Immediate="true"`. `0` disables debouncing. |
| `Immediate`    | `bool`    | `false`       | If `true`, `OnChange`/`ValueChanged` triggers on every keystroke (`oninput` event). If `false` (default), triggers on blur (`onchange` event). |
| `ThrottleTime` | `int`     | `0`           | Limits the rate at which `OnChange`/`ValueChanged` triggers to at most once per `ThrottleTime` milliseconds. Requires `Immediate="true"`. `0` disables throttling. |

---

### `BitInputBase<TValue>` Parameters (Inherited by `BitTextField`, where `TValue` is `string?`)

Base class for input components, handling value binding and validation integration.

| Name                | Type                                  | Default Value | Description                                                                                                         |
| :------------------ | :------------------------------------ | :------------ | :------------------------------------------------------------------------------------------------------------------ |
| `DisplayName`       | `string?`                             | `null`        | A user-friendly name for the field, used in validation error messages. If not set, derived from `ValueExpression`. |
| `InputHtmlAttributes` | `IReadOnlyDictionary<string, object>?`| `null`        | Additional HTML attributes to apply directly to the underlying `<input>` or `<textarea>` element.                   |
| `Name`              | `string?`                             | `null`        | The `name` attribute of the input element, useful for form submission or JavaScript interaction.                 |
| `NoValidate`        | `bool`                                | `false`       | If `true`, suppresses the generation of validation attributes (like `required`, `pattern`) on the input element. |
| `OnChange`          | `EventCallback<TValue?>`              |               | A callback invoked when the `Value` changes. Respects `Immediate`, `DebounceTime`, and `ThrottleTime`.             |
| `ReadOnly`          | `bool`                                | `false`       | If `true`, makes the input read-only (`readonly` attribute). The value cannot be changed by the user.           |
| `Required`          | `bool`                                | `false`       | If `true`, adds the `required` attribute and styling. Note: Actual validation logic relies on model attributes (e.g., `[Required]`). |
| `Value`             | `TValue?` (`string?`)                 | `null`        | The current value of the input component. Use with `@bind-Value` for two-way data binding.                        |
| `ValueChanged`      | `EventCallback<TValue?>`              |               | An `EventCallback` used implicitly by `@bind-Value` for two-way binding updates.                                  |
| `ValueExpression`   | `Expression<Func<TValue?>>?`          | `null`        | An expression used implicitly by `@bind-Value` to identify the bound property, enabling validation integration. |

---

### `BitInputBase<TValue>` Public Members (Inherited by `BitTextField`)

| Name                      | Type                 | Description                                                                                                |
| :------------------------ | :------------------- | :--------------------------------------------------------------------------------------------------------- |
| `InputElement`            | `ElementReference`   | Provides a reference to the underlying HTML `<input>` or `<textarea>` element (Note: Also in `BitTextField`). |
| `FocusAsync()`            | `() => ValueTask`    | Programmatically sets focus to the input element.                                                          |
| `FocusAsync(bool preventScroll)` | `(bool) => ValueTask`| Programmatically sets focus, optionally preventing the browser from scrolling the element into view.      |

---

### `BitComponentBase` Parameters (Base for all Bit components, Inherited by `BitTextField`)

Common parameters for all Bit Blazor UI components.

| Name             | Type                            | Default Value                       | Description                                                                                                 |
| :--------------- | :------------------------------ | :---------------------------------- | :---------------------------------------------------------------------------------------------------------- |
| `AriaLabel`      | `string?`                       | `null`                              | Defines a string value that labels the current element for accessibility purposes (`aria-label` attribute). |
| `Class`          | `string?`                       | `null`                              | Custom CSS class(es) to apply to the root element of the component.                                         |
| `Dir`            | `BitDir?`                       | `null`                              | Sets the text direction (`ltr`, `rtl`, `auto`) for the component. See `BitDir` enum below.                    |
| `HtmlAttributes` | `Dictionary<string, object>`    | `new Dictionary<string, object>()`  | Allows capturing and rendering arbitrary HTML attributes (splatting) on the root element of the component. |
| `Id`             | `string?`                       | `null`                              | Custom `id` attribute for the root element. If not provided, the component's `UniqueId` will be used.       |
| `IsEnabled`      | `bool`                          | `true`                              | Whether the component is enabled. If `false`, it typically appears grayed out and interaction is disabled. |
| `Style`          | `string?`                       | `null`                              | Custom inline CSS style(s) to apply to the root element of the component.                                   |
| `Visibility`     | `BitVisibility`                 | `BitVisibility.Visible`             | Controls whether the component is visible, hidden (occupies space), or collapsed (no space). See `BitVisibility` enum below. |

---

### `BitComponentBase` Public Members (Base for all Bit components, Inherited by `BitTextField`)

| Name          | Type               | Default Value    | Description                                                                                                      |
| :------------ | :----------------- | :--------------- | :--------------------------------------------------------------------------------------------------------------- |
| `UniqueId`    | `Guid`             | `Guid.NewGuid()` | A read-only, unique identifier (GUID) generated automatically for each component instance. Useful for `id` refs. |
| `RootElement` | `ElementReference` |                  | Provides a reference to the root HTML element of the component.                                                  |

---

### `BitTextFieldClassStyles` Properties (Used by `Classes` and `Styles` parameters)

This class allows specifying CSS classes (for the `Classes` parameter) or inline styles (for the `Styles` parameter) for various internal parts of the `BitTextField` component, enabling fine-grained visual customization.

| Property                    | Type      | Description                                                                   |
| :-------------------------- | :-------- | :---------------------------------------------------------------------------- |
| `Root`                      | `string?` | The main container `div` element of the component.                            |
| `Focused`                   | `string?` | Class/style applied to the `Root` element when the input has focus.           |
| `InputWrapper`              | `string?` | The `div` wrapping the `Label` (if present) and the `FieldGroup`.             |
| `Label`                     | `string?` | The `<label>` element.                                                        |
| `FieldGroup`                | `string?` | The `div` that visually groups the prefix, input, suffix, icon, etc.          |
| `PrefixContainer`           | `string?` | The `div` containing the prefix element/template.                             |
| `Prefix`                    | `string?` | The `span` or custom element rendering the prefix content.                    |
| `Input`                     | `string?` | The actual `<input>` or `<textarea>` element.                                 |
| `RevealPassword`            | `string?` | The `<button>` element used for revealing the password.                       |
| `RevealPasswordIconContainer`| `string?` | The `span` container inside the reveal password button holding the icon.      |
| `RevealPasswordIcon`        | `string?` | The `<i>` element representing the reveal password icon.                     |
| `Icon`                      | `string?` | The `<i>` element representing the icon specified by `IconName`.             |
| `SuffixContainer`           | `string?` | The `div` containing the suffix element/template.                             |
| `Suffix`                    | `string?` | The `span` or custom element rendering the suffix content.                    |
| `DescriptionContainer`      | `string?` | The `span` or `div` containing the description element/template.              |
| `Description`               | `string?` | The `span` or custom element rendering the description content.               |

---

### Related Enums

#### `BitInputType` Enum (for `Type` parameter)

Defines the behavior and semantics of the input field.

| Name       | Value | Description                              | Corresponds to HTML `type` |
| :--------- | :---- | :--------------------------------------- | :------------------------- |
| `Text`     | 0     | Standard text input.                     | `text`                     |
| `Password` | 1     | Password input (obscures characters).    | `password`                 |
| `Number`   | 2     | Input for numerical values.              | `number`                   |
| `Email`    | 3     | Input for email addresses.               | `email`                    |
| `Tel`      | 4     | Input for telephone numbers.             | `tel`                      |
| `Url`      | 5     | Input for URLs.                          | `url`                      |

#### `BitInputMode` Enum (for `InputMode` parameter)

Provides a hint to the browser about the type of virtual keyboard to display on touch devices.

| Name      | Value | Description                                                                    | Corresponds to HTML `inputmode` |
| :-------- | :---- | :----------------------------------------------------------------------------- | :------------------------------ |
| `None`    | 0     | No specific input mode hint provided.                                          | (attribute not set)             |
| `Text`    | 1     | Standard input keyboard for the user's current locale.                         | `text`                          |
| `Decimal` | 2     | Fractional numeric input keyboard (digits and locale-specific decimal separator). | `decimal`                       |
| `Numeric` | 3     | Numeric input keyboard (digits 0–9 only).                                      | `numeric`                       |
| `Tel`     | 4     | Telephone keypad input (digits 0–9, *, #).                                     | `tel`                           |
| `Search`  | 5     | Virtual keyboard optimized for search input (may have a "Search" button).      | `search`                        |
| `Email`   | 6     | Virtual keyboard optimized for entering email addresses (includes @, .).       | `email`                         |
| `Url`     | 7     | Virtual keyboard optimized for entering URLs (includes /, .).                  | `url`                           |

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

* **Accessibility:** Always provide a `Label` (preferred) or an `AriaLabel` for screen reader users. If using `Prefix` or `Suffix`, ensure the `Label` adequately describes the expected input, as the prefix/suffix are not part of the accessible name by default.
* **Validation:** Integrate with Blazor's `EditForm` for robust validation. Use data annotation attributes (`[Required]`, `[StringLength]`, etc.) on your model properties. The `Required` parameter on `BitTextField` primarily adds visual cues (like `*`) and the HTML `required` attribute; actual validation depends on the model and `DataAnnotationsValidator`.
* **Binding:** Use `@bind-Value` for two-way data binding in most form scenarios. Use the `Value` parameter for one-way binding (less common for inputs). Use `DefaultValue` only for uncontrolled components where Blazor doesn't manage the state.
* **Performance:** Be cautious with `Immediate="true"`. If the bound property update or `OnChange` handler is complex, frequent updates can impact performance. Use `DebounceTime` or `ThrottleTime` to mitigate this if immediate feedback is needed but updates can be slightly delayed or rate-limited.
* **Styling:** Use `Style` and `Class` for simple root-level customization. Use `Styles` and `Classes` objects for more complex scenarios requiring access to internal component elements. Prefer `Classes` and external CSS for maintainability over extensive inline `Styles`.
* **Multiline:** When `Multiline="true"`, the component renders a `<textarea>`. Parameters like `Rows` and `Resizable` only apply in this mode.
* **Password Reveal:** The `CanRevealPassword` feature enhances usability but ensure your application's security policies allow for password visibility toggles.

