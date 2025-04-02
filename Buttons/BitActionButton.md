# ActionButton Component Documentation

This document serves as a comprehensive reference for the **ActionButton** component. The ActionButton is a specialized type of button that comes with a distinct set of visual styles and properties. It is designed to enhance user interaction by combining iconography with text, supporting various button states, styles, and behaviors.

---

## Overview

**ActionButton** is a button with built-in icon support and a unique visual style. It offers properties such as:
- **IconName** to specify the icon to display.
- **ReversedIcon** to swap the positions of the icon and the button content.
- **Href** and **Rel** properties to render the button as a hyperlink.
- Customizable **Color**, **Size**, and styling via **Styles** or **Classes**.
- Built-in support for different button types (Submit, Reset, Button) and RTL (Right-to-Left) layout.

---

## Usage

### Basic Usage

Below are examples of basic ActionButton usage:
  
```cshtml
<BitActionButton IconName="@BitIconName.AddFriend">
    Create account
</BitActionButton>

<BitActionButton IconName="@BitIconName.AddFriend" ReversedIcon="true">
    Reversed Icon
</BitActionButton>

<BitActionButton IconName="@BitIconName.AddFriend" IsEnabled="false">
    Disabled
</BitActionButton>

<BitActionButton>
    No Icon
</BitActionButton>
```

In the rendered output, you will see buttons with an icon (using the `AddFriend` icon), a reversed icon layout, a disabled button state, and a button with no icon.

---

### Href Usage

Use the **Href** property to render the ActionButton as a hyperlink. For example:

```cshtml
<BitActionButton IconName="@BitIconName.Globe" 
                 Href="https://bitplatform.dev" 
                 Target="_blank">
    Open bitplatform.dev
</BitActionButton>

<BitActionButton IconName="@BitIconName.Globe" 
                 Href="https://github.com/bitfoundation/bitplatform">
    Go to bitplatform GitHub
</BitActionButton>
```

---

### Rel Attribute

When used as a link, the **Rel** property adds security and SEO attributes to the hyperlink:

```cshtml
<BitActionButton Rel="BitLinkRel.NoFollow" 
                 Href="https://bitplatform.dev" 
                 Target="_blank" 
                 IconName="@BitIconName.Globe">
    Open bitplatform.dev with a rel attribute (nofollow)
</BitActionButton>

<BitActionButton Rel="BitLinkRel.NoFollow | BitLinkRel.NoReferrer" 
                 Href="https://bitplatform.dev" 
                 Target="_blank" 
                 IconName="@BitIconName.Globe">
    Open bitplatform.dev with a rel attribute (nofollow &amp; noreferrer)
</BitActionButton>
```

---

### Color Variants

ActionButton supports different predefined colors. Here are some examples:

```cshtml
<BitActionButton Color="BitColor.Primary" IconName="@BitIconName.ColorSolid">
    Primary
</BitActionButton>

<BitActionButton Color="BitColor.Secondary" IconName="@BitIconName.ColorSolid">
    Secondary
</BitActionButton>

<BitActionButton Color="BitColor.Tertiary" IconName="@BitIconName.ColorSolid">
    Tertiary
</BitActionButton>

<BitActionButton Color="BitColor.Info" IconName="@BitIconName.ColorSolid">
    Info
</BitActionButton>

<BitActionButton Color="BitColor.Success" IconName="@BitIconName.ColorSolid">
    Success
</BitActionButton>

<BitActionButton Color="BitColor.Warning" IconName="@BitIconName.ColorSolid">
    Warning
</BitActionButton>

<BitActionButton Color="BitColor.SevereWarning" IconName="@BitIconName.ColorSolid">
    SevereWarning
</BitActionButton>

<BitActionButton Color="BitColor.Error" IconName="@BitIconName.ColorSolid">
    Error
</BitActionButton>

<!-- Background variants (rendered on a contrasting background) -->
<BitActionButton Color="BitColor.PrimaryBackground" IconName="@BitIconName.ColorSolid">
    PrimaryBackground
</BitActionButton>

<BitActionButton Color="BitColor.SecondaryBackground" IconName="@BitIconName.ColorSolid">
    SecondaryBackground
</BitActionButton>

<BitActionButton Color="BitColor.TertiaryBackground" IconName="@BitIconName.ColorSolid">
    TertiaryBackground
</BitActionButton>

<BitActionButton Color="BitColor.PrimaryForeground" IconName="@BitIconName.ColorSolid">
    PrimaryForeground
</BitActionButton>

<BitActionButton Color="BitColor.SecondaryForeground" IconName="@BitIconName.ColorSolid">
    SecondaryForeground
</BitActionButton>

<BitActionButton Color="BitColor.TertiaryForeground" IconName="@BitIconName.ColorSolid">
    TertiaryForeground
</BitActionButton>

<BitActionButton Color="BitColor.PrimaryBorder" IconName="@BitIconName.ColorSolid">
    PrimaryBorder
</BitActionButton>

<BitActionButton Color="BitColor.SecondaryBorder" IconName="@BitIconName.ColorSolid">
    SecondaryBorder
</BitActionButton>

<BitActionButton Color="BitColor.TertiaryBorder" IconName="@BitIconName.ColorSolid">
    TertiaryBorder
</BitActionButton>
```

---

### Size

ActionButton can be rendered in different sizes. For example:

```cshtml
<BitActionButton Size="BitSize.Small" IconName="@BitIconName.FontSize">
    Small
</BitActionButton>

<BitActionButton Size="BitSize.Medium" IconName="@BitIconName.FontSize">
    Medium
</BitActionButton>

<BitActionButton Size="BitSize.Large" IconName="@BitIconName.FontSize">
    Large
</BitActionButton>
```

You can also see the rendered buttons in small, medium, and large sizes.

---

### Style & Class

Customize the appearance of ActionButton using inline styles or external CSS classes. For instance:

```cshtml
<!-- Inline style example -->
<style>
  .custom-class {
      padding: 0.5rem;
      filter: hue-rotate(45deg);
      background-color: blueviolet;
  }
  
  .custom-image {
      width: 16rem;
      filter: opacity(25%);
      border-radius: 1rem 3rem;
  }
</style>

<BitActionButton IconName="@BitIconName.Brush" 
                 Styles="@(new BitActionButtonClassStyles { Root = "font-size: 1.5rem;", Icon = "color: blueviolet;" })" 
                 Src="images/bit-logo-blue.png">
    Action Button Styles
</BitActionButton>

<BitActionButton IconName="@BitIconName.FormatPainter" 
                 Classes="@(new BitActionButtonClassStyles { Root = "custom-root", Icon = "custom-icon", Content = "custom-content" })">
    Action Button Classes (Hover me)
</BitActionButton>
```

---

### Template

ActionButton also supports custom templates. You can embed a custom template to change the content layout when needed.

```cshtml
<BitActionButton IconName="@BitIconName.AddFriend">
    <div style="display:flex; gap:0.5rem;">
        <div>This is a custom template</div>
        <BitSpinnerLoading CustomSize="20" />
    </div>
</BitActionButton>
```

---

### Button Type

ActionButton can be used within forms and support different HTML button types (Submit, Reset, and standard Button). For example:

```cshtml
<EditForm Model="validationButtonModel" OnValidSubmit="HandleValidSubmit">
    <DataAnnotationsValidator />
    <ValidationSummary />
    
    <BitTextField Label="Required" Required @bind-Value="validationButtonModel.RequiredText" />
    <ValidationMessage For="() => validationButtonModel.RequiredText" style="color:red" />
    
    <BitTextField Label="Nonrequired" @bind-Value="validationButtonModel.NonRequiredText" />
    
    <div>
        <BitActionButton IconName="@BitIconName.SendMirrored" ButtonType="BitButtonType.Submit">
            Submit
        </BitActionButton>
        <BitActionButton IconName="@BitIconName.Reset" ButtonType="BitButtonType.Reset">
            Reset
        </BitActionButton>
        <BitActionButton IconName="@BitIconName.ButtonControl" ButtonType="BitButtonType.Button">
            Button
        </BitActionButton>
    </div>
</EditForm>

@code {
    public class ButtonValidationModel
    {
        [Required]
        public string RequiredText { get; set; } = string.Empty;
        public string? NonRequiredText { get; set; }
    }
    
    private ButtonValidationModel validationButtonModel = new();
    
    private async Task HandleValidSubmit()
    {
        await Task.Delay(2000);
        validationButtonModel = new ButtonValidationModel();
        StateHasChanged();
    }
}
```

---

### RTL

Use the **Dir** property to render the button in a right-to-left (RTL) context.

```cshtml
<BitActionButton Dir="BitDir.Rtl" IconName="@BitIconName.AddFriend">
    ساخت حساب
</BitActionButton>
```

Alternatively, you can set the `dir` attribute on a container:

```html
<div dir="rtl">
    <button class="bit-acb bit-rtl bit-acb-pri bit-acb-md">
        <i class="bit-acb-ico bit-icon bit-icon--AddFriend"></i>
        <div class="bit-acb-con">ساخت حساب</div>
    </button>
</div>
```

---

## API

### BitActionButton Parameters

| **Name**              | **Type**                              | **Default Value** | **Description**                                                                                          |
| --------------------- | ------------------------------------- | ----------------- | -------------------------------------------------------------------------------------------------------- |
| AllowDisabledFocus    | `bool`                                | `false`           | Whether the button can receive focus when disabled.                                                    |
| AriaDescription       | `string?`                             | `null`            | Provides a detailed description for screen readers.                                                     |
| AriaHidden            | `bool`                                | `false`           | If true, adds `aria-hidden` to instruct screen readers to ignore the button.                              |
| ButtonType            | `BitButtonType`                       | `null`            | Specifies the HTML button type (e.g., Button, Submit, Reset).                                             |
| ChildContent          | `RenderFragment?`                      | `null`            | The content displayed inside the button.                                                                |
| Classes               | `BitActionButtonClassStyles?`         | `null`            | Custom CSS classes for different parts of the button.                                                   |
| Color                 | `BitColor?`                           | `null`            | Specifies the general color of the button.                                                              |
| FullWidth             | `bool`                                | `false`           | If true, renders the button at the full width of its container.                                           |
| Href                  | `string?`                             | `null`            | When provided, the button renders as an anchor element with the specified URL.                            |
| IconName              | `string?`                             | `null`            | The name of the icon to display inside the button.                                                      |
| IconOnly              | `bool`                                | `false`           | If true, only the icon is rendered without any accompanying text.                                         |
| OnClick               | `EventCallback<MouseEventArgs>`        | `null`            | Callback invoked when the button is clicked.                                                            |
| Rel                   | `BitLinkRel?`                         | `null`            | Specifies the relationship between the current document and the linked document when used with Href.      |
| Size                  | `BitSize?`                            | `null`            | Specifies the size of the button (Small, Medium, Large).                                                  |
| Target                | `string?`                             | `null`            | Specifies the target for the link when the button is rendered as an anchor (e.g., `_blank`).                |
| Title                 | `string?`                             | `null`            | The tooltip text displayed on hover.                                                                    |

### BitComponentBase Parameters

| **Name**         | **Type**                              | **Default Value** | **Description**                                                                             |
| ---------------- | ------------------------------------- | ----------------- | ------------------------------------------------------------------------------------------- |
| AriaLabel        | `string?`                             | `null`            | The aria-label for accessibility.                                                         |
| Class            | `string?`                             | `null`            | Custom CSS class for the root element.                                                    |
| Dir              | `BitDir?`                             | `null`            | Sets the text direction (Ltr, Rtl, or Auto).                                                |
| HtmlAttributes   | `Dictionary<string, object>`          | `new Dictionary<string, object>()` | Additional HTML attributes for the root element.                                    |
| Id               | `string?`                             | `null`            | Custom id for the root element. If not provided, a unique id will be generated.             |
| IsEnabled        | `bool`                                | `true`            | Determines whether the component is enabled.                                              |
| Style            | `string?`                             | `null`            | Custom CSS style for the root element.                                                      |
| Visibility       | `BitVisibility`                       | `BitVisibility.Visible` | Controls the visibility of the component.                                             |

### BitComponentBase Public Members

| **Name**    | **Type**             | **Default Value**      | **Description**                                                                              |
| ----------- | -------------------- | ---------------------- | -------------------------------------------------------------------------------------------- |
| UniqueId    | `Guid`               | `Guid.NewGuid()`       | A read-only unique identifier for the component instance.                                    |
| RootElement | `ElementReference`   | *(none)*               | A reference to the root HTML element of the component.                                      |

### BitActionButtonClassStyles Properties

| **Name** | **Type**  | **Default Value** | **Description**                                                       |
| -------- | --------- | ----------------- | --------------------------------------------------------------------- |
| Root     | `string?` | `null`            | Custom CSS classes/styles for the root element of the ActionButton.   |
| Icon     | `string?` | `null`            | Custom CSS classes/styles for the icon within the ActionButton.       |
| Content  | `string?` | `null`            | Custom CSS classes/styles for the button’s text content.              |

---

## Enumerations

### BitButtonType Enum

| **Name**   | **Value** | **Description**                                                  |
| ---------- | --------- | ---------------------------------------------------------------- |
| Button     | `0`       | The button acts as a standard clickable button.                  |
| Submit     | `1`       | The button submits the form data.                                |
| Reset      | `2`       | The button resets the form data to its initial values.           |

### BitColor Enum

| **Name**             | **Value** | **Description**                                      |
| -------------------- | --------- | ---------------------------------------------------- |
| Primary              | `0`       | Primary color for key actions.                       |
| Secondary            | `1`       | Secondary color for less emphasized actions.         |
| Tertiary             | `2`       | Tertiary color for alternate emphasis.               |
| Info                 | `3`       | Informational color.                                 |
| Success              | `4`       | Indicates successful operations.                   |
| Warning              | `5`       | Indicates caution or warning.                        |
| SevereWarning        | `6`       | Indicates severe warnings.                           |
| Error                | `7`       | Indicates error states.                              |
| PrimaryBackground    | `8`       | Background color for primary elements.             |
| SecondaryBackground  | `9`       | Background color for secondary elements.           |
| TertiaryBackground   | `10`      | Background color for tertiary elements.            |
| PrimaryForeground    | `11`      | Foreground color for primary elements.             |
| SecondaryForeground  | `12`      | Foreground color for secondary elements.           |
| TertiaryForeground   | `13`      | Foreground color for tertiary elements.            |
| PrimaryBorder        | `14`      | Border color for primary elements.                 |
| SecondaryBorder      | `15`      | Border color for secondary elements.               |
| TertiaryBorder       | `16`      | Border color for tertiary elements.                |

### BitSize Enum

| **Name**  | **Value** | **Description**                  |
| --------- | --------- | -------------------------------- |
| Small     | `0`       | Renders a small-sized button.    |
| Medium    | `1`       | Renders a medium-sized button.   |
| Large     | `2`       | Renders a large-sized button.    |

### BitLinkRel Enum

| **Name**    | **Value** | **Description**                                                                           |
| ----------- | --------- | ----------------------------------------------------------------------------------------- |
| Alternate   | `1`       | Provides a link to an alternate representation (e.g., print version, translation).         |
| Author      | `2`       | Provides a link to the author of the document.                                             |
| Bookmark    | `4`       | Provides a permanent URL for bookmarking.                                                 |
| External    | `8`       | Indicates the linked document is external to the current site.                             |
| Help        | `16`      | Provides a link to a help document.                                                         |
| License     | `32`      | Provides a link to licensing information.                                                  |
| Next        | `64`      | Provides a link to the next document in a sequence.                                         |
| NoFollow    | `128`     | Tells search engines not to follow the link.                                               |
| NoOpener    | `256`     | Ensures the new browsing context has no access to the originating window.                  |
| NoReferrer  | `512`     | Ensures no referrer information is sent when the link is followed.                           |
| Prev        | `1024`    | Provides a link to the previous document in a sequence.                                    |
| Search      | `2048`    | Provides a link to a search tool for the document.                                         |
| Tag         | `4096`    | Specifies a tag (keyword) for the current document.                                        |

### BitVisibility Enum

| **Name**    | **Value** | **Description**                                                      |
| ----------- | --------- | -------------------------------------------------------------------- |
| Visible     | `0`       | The component is visible.                                            |
| Hidden      | `1`       | The component is hidden but occupies space (using `visibility:hidden`).|
| Collapsed   | `2`       | The component is hidden and does not occupy any space (`display:none`).|

### BitDir Enum

| **Name** | **Value** | **Description**                                                                                   |
| -------- | --------- | ------------------------------------------------------------------------------------------------- |
| Ltr      | `0`       | Left-to-right layout (e.g., for English).                                                          |
| Rtl      | `1`       | Right-to-left layout (e.g., for Arabic).                                                           |
| Auto     | `2`       | Automatically determines text direction based on content.                                        |

---

## Feedback

Your feedback is important to help us improve the ActionButton component. You can share your thoughts or report issues through the following channels:

- **GitHub Repository:**  
  [View Repository](https://github.com/bitfoundation/bitplatform)

- **File a New Issue:**  
  [Open Issue](https://github.com/bitfoundation/bitplatform/issues/new/choose)

- **Start a Discussion:**  
  [New Discussion](https://github.com/bitfoundation/bitplatform/discussions/new/choose)

- **Review/Edit ActionButton Demo:**  
  [Review Demo](https://github.com/bitfoundation/bitplatform/blob/develop/src/BlazorUI/Demo/Client/Bit.BlazorUI.Demo.Client.Core/Pages/Components/Buttons/ActionButton/BitActionButtonDemo.razor)  
  [Edit Demo](https://github.com/bitfoundation/bitplatform/edit/develop/src/BlazorUI/Demo/Client/Bit.BlazorUI.Demo.Client.Core/Pages/Components/Buttons/ActionButton/BitActionButtonDemo.razor)

- **Review/Edit ActionButton Component:**  
  [Review Component](https://github.com/bitfoundation/bitplatform/blob/develop/src/BlazorUI/Bit.BlazorUI/Components/Buttons/ActionButton/BitActionButton.razor)  
  [Edit Component](https://github.com/bitfoundation/bitplatform/edit/develop/src/BlazorUI/Bit.BlazorUI/Components/Buttons/ActionButton/BitActionButton.razor)

---

## Explanation for AI Agent Usage

This Markdown reference is designed for an AI agent (or similar documentation tools) to:

- **Understand the Component:**  
  Identify that **ActionButton** is a specialized button with customizable icon, style, color, size, and behavior settings.

- **Generate Code Examples:**  
  Use the provided code snippets to generate similar examples, including variations in icon usage, hyperlink rendering (via Href and Rel), size adjustments, custom styling, and RTL layouts.

- **Extract API Information:**  
  Parse the API tables to retrieve property names, types, default values, and descriptions for both the ActionButton-specific parameters and the base component parameters.

- **Interpret Enumerations:**  
  Utilize the enum definitions (such as BitButtonType, BitColor, BitSize, BitLinkRel, BitVisibility, and BitDir) to control the visual and behavioral aspects of the button.

- **Apply Custom Styles:**  
  Leverage the examples and custom class/style tables to modify the look and feel of the button using either inline CSS or external class bindings.

- **Access Feedback Channels:**  
  Direct users to the appropriate GitHub links to review, report, or contribute to the component.

This complete reference ensures that both developers and automated systems have all the necessary information to effectively implement, customize, and troubleshoot the ActionButton component within the Bit BlazorUI framework.

---

*End of ActionButton Component Documentation.*