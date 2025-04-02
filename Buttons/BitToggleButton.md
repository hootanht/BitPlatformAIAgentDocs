# BitToggleButton Blazor Component

**Objective:** This document provides context and reference information about the `BitToggleButton` Blazor component, based *solely* on the provided HTML documentation extract. Use this information to understand the component's features, generate relevant code snippets, and explain its usage.

**Key Component:** `BitToggleButton`

---

## Overview

`BitToggleButton` is a type of button that stores and shows a status representing the toggle state (checked/unchecked) of the component.

---

## Usage Examples

**1. Basic**

* **Description**: A standard toggle button showing different text and icons based on its checked state.
* **Code**:

    ```cshtml
    <BitToggleButton OffText="Unmuted" OffIconName="@BitIconName.Microphone"
                     OnText="Muted" OnIconName="@BitIconName.MicOff" />
    ```

**2. Variant**

* **Description**: Shows the three visual variants: `Fill` (default), `Outline`, and `Text`, in both enabled and disabled states.
* **Code**:

    ```cshtml
    <BitToggleButton Variant="BitVariant.Fill">Fill</BitToggleButton>
    <BitToggleButton Variant="BitVariant.Outline">Outline</BitToggleButton>
    <BitToggleButton Variant="BitVariant.Text">Text</BitToggleButton>

    <BitToggleButton Variant="BitVariant.Fill" IsEnabled="false">Fill</BitToggleButton>
    <BitToggleButton Variant="BitVariant.Outline" IsEnabled="false">Outline</BitToggleButton>
    <BitToggleButton Variant="BitVariant.Text" IsEnabled="false">Text</BitToggleButton>
    ```

**3. Size**

* **Description**: Illustrates the available sizes (`Small`, `Medium`, `Large`) for toggle buttons across different variants.
* **Code**:

    ```cshtml
    <BitToggleButton Size="BitSize.Small" Variant="BitVariant.Fill">Small</BitToggleButton>
    <BitToggleButton Size="BitSize.Medium" Variant="BitVariant.Fill">Medium</BitToggleButton>
    <BitToggleButton Size="BitSize.Large" Variant="BitVariant.Fill">Large</BitToggleButton>

    <BitToggleButton Size="BitSize.Small" Variant="BitVariant.Outline">Small</BitToggleButton>
    <BitToggleButton Size="BitSize.Medium" Variant="BitVariant.Outline">Medium</BitToggleButton>
    <BitToggleButton Size="BitSize.Large" Variant="BitVariant.Outline">Large</BitToggleButton>

    <BitToggleButton Size="BitSize.Small" Variant="BitVariant.Text">Small</BitToggleButton>
    <BitToggleButton Size="BitSize.Medium" Variant="BitVariant.Text">Medium</BitToggleButton>
    <BitToggleButton Size="BitSize.Large" Variant="BitVariant.Text">Large</BitToggleButton>
    ```

**4. Color**

* **Description**: Displays toggle buttons using various `BitColor` options (`Primary`, `Secondary`, `Tertiary`, `Info`, `Success`, `Warning`, `SevereWarning`, `Error`, and background/foreground/border variations) across different variants (`Fill`, `Outline`, `Text`).
* **Code**: (Shows pattern for one color - Primary)

    ```cshtml
    <BitToggleButton Variant="BitVariant.Fill" Color="BitColor.Primary">Primary</BitToggleButton>
    <BitToggleButton Variant="BitVariant.Outline" Color="BitColor.Primary">Primary</BitToggleButton>
    <BitToggleButton Variant="BitVariant.Text" Color="BitColor.Primary">Primary</BitToggleButton>

    @* ... other colors follow the same pattern ... *@
    ```

**5. Style & Class**

* **Description**: Demonstrates applying custom `Style` and `Class` attributes to the root component, and using the `Styles` and `Classes` parameters to target specific internal elements (like Root, Checked state, Icon, Text) for advanced customization.
* **Code**: (Includes CSS for context)

    ```css
    .custom-class {
        border-radius: 1rem;
        border-color: blueviolet;
        transition: background-color 1s;
        background: linear-gradient(90deg, magenta, transparent) blue;
    }
    .custom-class:hover {
        border-color: magenta;
        background-color: magenta;
    }
    .custom-root { /* Styles for Classes parameter example */
        border: none;
        color: blueviolet;
        background: transparent;
    }
    .custom-text { /* Styles for Classes parameter example */
        position: relative;
    }
    .custom-root:hover .custom-text { color: darkviolet; }
    .custom-text::after { /* Underline effect */
        content: ''; left: 0; width: 0; height: 2px; bottom: -6px;
        position: absolute; transition: 0.3s ease;
        background: linear-gradient(90deg, #ff00cc, #3333ff);
    }
    .custom-icon { color: hotpink; }
    .custom-checked { /* Styles for checked state via Classes parameter */
        border: none; background-color: transparent;
    }
    .custom-checked .custom-text::after { width: 100%; }
    .custom-checked .custom-icon { color: hotpink; }
    ```

    ```cshtml
    <BitToggleButton Style="background-color: transparent; border-color: blueviolet; color: blueviolet;"
                     Variant="BitVariant.Outline"
                     OffText="Styled Button: Unmuted" OffIconName="@BitIconName.Microphone"
                     OnText="Styled Button: Muted" OnIconName="@BitIconName.MicOff" />

    <BitToggleButton Class="custom-class"
                     OffText="Classed Button: Unmuted" OffIconName="@BitIconName.Microphone"
                     OnText="Classed Button: Muted" OnIconName="@BitIconName.MicOff" />


    <BitToggleButton OffText="Styled Button: Unmuted" OffIconName="@BitIconName.Microphone"
                     OnText="Styled Button: Muted" OnIconName="@BitIconName.MicOff"
                     Styles="@(new() { Root = "--toggle-background: pink; background: var(--toggle-background); border: none;",
                                       Checked = "--toggle-background: peachpuff;",
                                       Icon = "color: red;",
                                       Text = "color: tomato;" })" />

    <BitToggleButton Variant="BitVariant.Text"
                     OffText="Classed Button: Unmuted" OffIconName="@BitIconName.Microphone"
                     OnText="Classed Button: Muted" OnIconName="@BitIconName.MicOff"
                     Classes="@(new() { Root = "custom-root",
                                        Checked = "custom-checked",
                                        Container = "custom-content", // Note: Container class mentioned in example, maps to internal structure
                                        Icon = "custom-icon",
                                        Text = "custom-text" })" />
    ```

**6. Binding**

* **Description**: Shows different ways to manage the button's checked state: using `DefaultIsChecked` for initial state, two-way binding with `@bind-IsChecked`, and handling the `OnChange` event.
* **Code**:

    ```cshtml
    <BitToggleButton DefaultIsChecked="true"
                     OffText="Unmuted" OnText="Muted"
                     OffIconName="@BitIconName.Microphone" OnIconName="@BitIconName.MicOff" />

    <BitToggleButton @bind-IsChecked="example51Value"
                     Text="@(example51Value ? "Muted" : "Unmuted")"
                     IconName="@(example51Value ? BitIconName.MicOff : BitIconName.Microphone)" />
    <BitCheckbox Label="Checked Toggle Button" @bind-Value="example51Value" />

    <BitToggleButton OnChange="v => example52Value = v"
                     OffText="Unmuted" OnText="Muted"
                     OffIconName="@BitIconName.Microphone" OnIconName="@BitIconName.MicOff" />
    <BitLabel>Check status is: @example52Value</BitLabel>
    ```

    ```csharp
    @code {
        private bool example51Value;
        private bool example52Value;
    }
    ```

**7. Templates**

* **Description**: Shows how to provide custom content (`ChildContent`) inside the toggle button instead of relying solely on text/icon parameters.
* **Code**: (Includes CSS for context)

    ```css
    .custom-content { /* Example class used in template */
        gap: 0.5rem;
        display: flex;
        align-items: center;
    }
    ```

    ```cshtml
    <BitToggleButton Class="custom-content">
        <BitIcon IconName="@BitIconName.Airplane" />
        <span>Custom template</span>
        <BitRollerLoading CustomSize="20" Color="BitColor.Tertiary" />
    </BitToggleButton>
    ```

**8. Events**

* **Description**: Demonstrates handling the `OnClick` event.
* **Code**:

    ```cshtml
    <BitToggleButton OnClick="() => clickCounter++">Click me (@clickCounter)</BitToggleButton>
    ```

    ```csharp
    @code {
        private int clickCounter;
    }
    ```

**9. RTL**

* **Description**: Demonstrates using `Dir="BitDir.Rtl"` to render the component in a right-to-left layout.
* **Code**:

    ```cshtml
    <BitToggleButton Dir="BitDir.Rtl" Variant="BitVariant.Fill"
                     OffText="صدا وصل" OffIconName="@BitIconName.Microphone"
                     OnText="صدا قطع" OnIconName="@BitIconName.MicOff" />

    <BitToggleButton Dir="BitDir.Rtl" Variant="BitVariant.Outline"
                     OffText="صدا وصل" OffIconName="@BitIconName.Microphone"
                     OnText="صدا قطع" OnIconName="@BitIconName.MicOff" />

    <BitToggleButton Dir="BitDir.Rtl" Variant="BitVariant.Text"
                     OffText="صدا وصل" OffIconName="@BitIconName.Microphone"
                     OnText="صدا قطع" OnIconName="@BitIconName.MicOff" />
    ```

---

## API Reference

**BitToggleButton Parameters**

| Name               | Type                          | Default | Description                                                                    |
| :----------------- | :---------------------------- | :------ | :----------------------------------------------------------------------------- |
| `AllowDisabledFocus`| `bool`                        | `false` | Whether the button can have focus in disabled mode.                            |
| `AriaDescription`  | `string?`                     | `null`  | Detailed description for screen readers.                                       |
| `AriaHidden`       | `bool`                        | `false` | If true, hides the element from screen readers.                              |
| `ChildContent`     | `RenderFragment?`             | `null`  | Custom content for the button (overrides Text/Icon parameters).              |
| `Classes`          | `BitToggleButtonClassStyles?` | `null`  | Custom CSS classes for different parts (Root, Checked, Icon, Text).          |
| `Color`            | `BitColor?`                   | `null`  | General color of the button.                                                   |
| `DefaultIsChecked` | `bool?`                       | `null`  | Initial checked state (uncontrolled).                                        |
| `IconName`         | `string?`                     | `null`  | Icon name rendered inside the button (used if On/OffIconName are not set).   |
| `IsChecked`        | `bool`                        | `false` | Checked state (use `@bind-IsChecked` for two-way binding).                   |
| `OnChange`         | `EventCallback<bool>`         |         | Callback when the `IsChecked` value changes.                                 |
| `OnClick`          | `EventCallback<MouseEventArgs>`|         | Callback when the button is clicked.                                         |
| `OffIconName`      | `string?`                     |         | Icon displayed when `IsChecked` is false.                                    |
| `OffText`          | `string?`                     |         | Text displayed when `IsChecked` is false.                                    |
| `OffTitle`         | `string?`                     |         | Title (tooltip) displayed when `IsChecked` is false.                           |
| `OnIconName`       | `string?`                     |         | Icon displayed when `IsChecked` is true.                                     |
| `OnText`           | `string?`                     |         | Text displayed when `IsChecked` is true.                                     |
| `OnTitle`          | `string?`                     |         | Title (tooltip) displayed when `IsChecked` is true.                            |
| `Size`             | `BitSize?`                    | `null`  | Size of the button (`Small`, `Medium`, `Large`).                               |
| `Styles`           | `BitToggleButtonClassStyles?` | `null`  | Custom CSS styles for different parts (Root, Checked, Icon, Text).           |
| `Text`             | `string?`                     | `null`  | Text displayed (used if On/OffText are not set, or `ChildContent` is null).  |
| `Title`            | `string?`                     | `null`  | Title (tooltip) displayed (used if On/OffTitle are not set).                 |
| `Variant`          | `BitVariant?`                 | `null`  | Visual variant (`Fill`, `Outline`, `Text`).                                    |
| *(Inherited)*      | *(See BitComponentBase)*      |         |                                                                                |

**BitComponentBase Parameters (Inherited)**

| Name           | Type                         | Default                   | Description                                                           |
| :------------- | :--------------------------- | :------------------------ | :-------------------------------------------------------------------- |
| `AriaLabel`    | `string?`                    | `null`                    | Aria-label for accessibility.                                         |
| `Class`        | `string?`                    | `null`                    | Custom CSS class for the root element.                                |
| `Dir`          | `BitDir?`                    | `null`                    | Component direction (`Ltr`, `Rtl`, `Auto`).                           |
| `HtmlAttributes`| `Dictionary<string, object>` | `new Dictionary<>()`      | Additional HTML attributes to render.                                 |
| `Id`           | `string?`                    | `null`                    | Custom ID for the root element (defaults to `UniqueId`).              |
| `IsEnabled`    | `bool`                       | `true`                    | Whether the component is enabled.                                     |
| `Style`        | `string?`                    | `null`                    | Custom CSS style for the root element.                                |
| `Visibility`   | `BitVisibility`              | `BitVisibility.Visible`   | Component visibility (`Visible`, `Hidden`, `Collapsed`).              |

**BitComponentBase Public Members (Inherited)**

| Name        | Type               | Default          | Description                                       |
| :---------- | :----------------- | :--------------- | :------------------------------------------------ |
| `UniqueId`  | `Guid`             | `Guid.NewGuid()` | Readonly unique ID assigned at construction.      |
| `RootElement` | `ElementReference` |                  | `ElementReference` for the root DOM element.    |

**BitToggleButtonClassStyles Properties (for `Classes`/`Styles`)**

| Name    | Type      | Default | Description                                                |
| :------ | :-------- | :------ | :--------------------------------------------------------- |
| `Root`    | `string?` | `null`  | Custom CSS class/style for the root `<button>` element.  |
| `Checked` | `string?` | `null`  | Custom CSS class/style applied when the button is checked. |
| `Icon`    | `string?` | `null`  | Custom CSS class/style for the icon element (`<i>`).      |
| `Text`    | `string?` | `null`  | Custom CSS class/style for the text element (`<span>`).   |

**Enums**

* **BitColor**: Defines color options (`Primary`, `Secondary`, `Tertiary`, `Info`, `Success`, `Warning`, `SevereWarning`, `Error`, `PrimaryBackground`, `SecondaryBackground`, `TertiaryBackground`, `PrimaryForeground`, `SecondaryForeground`, `TertiaryForeground`, `PrimaryBorder`, `SecondaryBorder`, `TertiaryBorder`).
* **BitSize**: Defines size options (`Small`, `Medium`, `Large`).
* **BitVariant**: Defines visual styles (`Fill`, `Outline`, `Text`).
* **BitVisibility**: Defines visibility states (`Visible`, `Hidden`, `Collapsed`).
* **BitDir**: Defines text direction (`Ltr`, `Rtl`, `Auto`).

---

## Feedback

* Provide feedback via the **GitHub repo**: [File an Issue](https://github.com/bitfoundation/bitplatform/issues/new/choose) or [Start a Discussion](https://github.com/bitfoundation/bitplatform/discussions/new/choose).
* Review/Edit this demo page: [Review](https://github.com/bitfoundation/bitplatform/blob/develop/src/BlazorUI/Demo/Client/Bit.BlazorUI.Demo.Client.Core/Pages/Components/Buttons/ToggleButton/BitToggleButtonDemo.razor) / [Edit](https://github.com/bitfoundation/bitplatform/edit/develop/src/BlazorUI/Demo/Client/Bit.BlazorUI.Demo.Client.Core/Pages/Components/Buttons/ToggleButton/BitToggleButtonDemo.razor)
* Review/Edit the component source: [Review](https://github.com/bitfoundation/bitplatform/blob/develop/src/BlazorUI/Bit.BlazorUI/Components/Buttons/ToggleButton/BitToggleButton.razor) / [Edit](https://github.com/bitfoundation/bitplatform/edit/develop/src/BlazorUI/Bit.BlazorUI/Components/Buttons/ToggleButton/BitToggleButton.razor)
