# BitMenuButton Component Reference

This document provides a complete reference for the `BitMenuButton` component. It is intended for developers and AI agents alike, serving as a detailed guide for usage, API parameters, and customization. Use this file as a reference when implementing or modifying the menu button in your applications.

---

## Overview

The `BitMenuButton` is a flexible, customizable menu button component designed to render a list of selectable options. It supports various sizes, visual variants, and rich templating options, making it suitable for diverse UI requirements.

---

## Usage

To use the `BitMenuButton` in your Blazor application, include it in your component and supply one or more menu button options:

```razor
<BitMenuButton Text="Options" DefaultSelectedItem="ItemB" OnChange="@HandleItemChange">
    <BitMenuButtonOption Text="Item A" Key="A" />
    <BitMenuButtonOption Text="Item B" Key="B" />
    <BitMenuButtonOption Text="Item C" Key="C" />
</BitMenuButton>

@code {
    private string currentItem = "ItemB";

    private void HandleItemChange(string selectedItem)
    {
        currentItem = selectedItem;
        // Additional logic here...
    }
}
```

*Note:* Replace `HandleItemChange` with your custom event callback to handle selection changes.

---

## API Reference

### BitMenuButton Parameters

| **Name**              | **Type**                           | **Default Value**           | **Description**                                                                                           |
|-----------------------|------------------------------------|-----------------------------|-----------------------------------------------------------------------------------------------------------|
| `AriaDescription`     | `string?`                          | `null`                      | Detailed description for screen readers.                                                                |
| `AriaHidden`          | `bool`                             | `false`                     | If true, adds an `aria-hidden` attribute, instructing screen readers to ignore the menu button.            |
| `ButtonType`          | `BitButtonType`                    | `null`                      | Sets the `type` attribute of the menu button (e.g., Button, Submit, Reset).                               |
| `ChevronDownIcon`     | `string?`                          | `null`                      | Icon name for the chevron indicating the dropdown state.                                                |
| `ChildContent`        | `RenderFragment?`                  | `null`                      | Content of the menu button, usually a collection of `BitMenuButtonOption` components.                      |
| `Classes`             | `BitMenuButtonClassStyles?`        | `null`                      | Custom CSS classes for styling different parts of the menu button.                                         |
| `Color`               | `BitColor?`                        | `null`                      | Sets the general color theme of the menu button.                                                          |
| `DefaultSelectedItem` | `TItem?`                           | `null`                      | The initial item to display as the header.                                                               |
| `HeaderTemplate`      | `RenderFragment?`                  | `null`                      | Custom template for the header content.                                                                   |
| `IconName`            | `string?`                          | `null`                      | Icon to display within the header of the menu button.                                                     |
| `IsOpen`              | `bool`                             | `false`                     | Controls whether the callout menu is open.                                                                |
| `Items`               | `IEnumerable<TItem>`               | `new List<TItem>()`         | Collection of items to display as menu options.                                                           |
| `ItemTemplate`        | `RenderFragment<TItem>?`           | `null`                      | Custom template for rendering each item.                                                                  |
| `NameSelectors`       | `BitMenuButtonNameSelectors<TItem>?`| `null`                     | Defines selectors to extract item properties (e.g., text, icon, key).                                      |
| `OnClick`             | `EventCallback<MouseEventArgs>`    | –                           | Callback when the menu button header is clicked.                                                         |
| `OnChange`            | `EventCallback<TItem>`             | –                           | Callback when the selected item changes.                                                                  |
| `Options`             | `RenderFragment?`                  | `null`                      | Alias for `ChildContent`; used to render the options.                                                     |
| `SelectedItem`        | `TItem?`                           | `null`                      | The currently selected item that appears as the header.                                                  |
| `Size`                | `BitSize?`                         | `null`                      | Sets the size of the menu button (Small, Medium, Large).                                                  |
| `Split`               | `bool`                             | `false`                     | Renders the button as a split button if true.                                                             |
| `Sticky`              | `bool`                             | `false`                     | If true, the selected item remains as the header after selection.                                         |
| `Styles`              | `BitMenuButtonClassStyles?`        | `null`                      | Custom CSS styles for the component.                                                                      |
| `Text`                | `string?`                          | `null`                      | Text to display in the header.                                                                            |
| `Variant`             | `BitVariant?`                      | `null`                      | Visual variant of the menu button (Fill, Outline, or Text).                                               |

### BitComponentBase Parameters

The `BitMenuButton` inherits from `BitComponentBase`, which includes:

| **Name**           | **Type**                           | **Default Value**                         | **Description**                                                                           |
|--------------------|------------------------------------|-------------------------------------------|-------------------------------------------------------------------------------------------|
| `AriaLabel`        | `string?`                          | `null`                                    | Aria-label for the component.                                                             |
| `Class`            | `string?`                          | `null`                                    | Custom CSS class for the root element.                                                    |
| `Dir`              | `BitDir?`                          | `null`                                    | Direction (LTR, RTL, or Auto) of the component.                                           |
| `HtmlAttributes`   | `Dictionary<string, object>`       | `new Dictionary<string, object>()`        | Additional HTML attributes for the root element.                                          |
| `Id`               | `string?`                          | `null`                                    | Custom id for the component. If null, a unique id is generated.                           |
| `IsEnabled`        | `bool`                             | `true`                                    | Specifies whether the component is enabled.                                               |
| `Style`            | `string?`                          | `null`                                    | Custom inline CSS for the root element.                                                   |
| `Visibility`       | `BitVisibility`                    | `BitVisibility.Visible`                   | Visibility state of the component.                                                        |

### Public Members (BitComponentBase)

| **Name**     | **Type**             | **Default Value**         | **Description**                                                  |
|--------------|----------------------|---------------------------|------------------------------------------------------------------|
| `UniqueId`   | `Guid`               | `Guid.NewGuid()`          | A readonly unique identifier for the component.                  |
| `RootElement`| `ElementReference`   | –                         | Reference to the root element of the component.                   |

---

## Detailed Subcomponents

### BitMenuButtonItem Properties

These properties are for individual menu button items:

| **Name**     | **Type**      | **Default Value** | **Description**                                          |
|--------------|---------------|-------------------|----------------------------------------------------------|
| `Class`      | `string?`     | `null`            | Custom CSS classes for the item.                         |
| `IconName`   | `string?`     | `null`            | Icon to display alongside the text.                      |
| `IsEnabled`  | `bool`        | `true`            | Whether the item is enabled.                             |
| `IsSelected` | `bool`        | `false`           | Whether the item is currently selected.                  |
| `Key`        | `string?`     | `null`            | A unique key identifier for the item.                    |
| `OnClick`    | `EventCallback`| –                 | Click event handler for the item.                        |
| `Style`      | `string?`     | `null`            | Inline styles for the item.                              |
| `Template`   | `RenderFragment<BitMenuButtonItem>?` | `null` | Custom template for rendering the item.         |
| `Text`       | `string?`     | `null`            | The text content of the item.                            |

### BitMenuButtonOption Properties

These properties are similar to BitMenuButtonItem and are used for options:

| **Name**     | **Type**      | **Default Value** | **Description**                                          |
|--------------|---------------|-------------------|----------------------------------------------------------|
| `Class`      | `string?`     | `null`            | Custom CSS classes for the option.                       |
| `IconName`   | `string?`     | `null`            | Icon to display with the option text.                    |
| `IsEnabled`  | `bool`        | `true`            | Whether the option is enabled.                           |
| `IsSelected` | `bool`        | `false`           | Whether the option is selected.                          |
| `Key`        | `string?`     | `null`            | A unique key for the option.                             |
| `OnClick`    | `EventCallback`| –                 | Click event handler for the option.                      |
| `Style`      | `string?`     | `null`            | Inline styles for the option.                            |
| `Template`   | `RenderFragment<BitMenuButtonOption>?` | `null` | Custom template for the option.           |
| `Text`       | `string?`     | `null`            | The text to display for the option.                      |

### BitMenuButtonClassStyles Properties

Customize the CSS classes and styles for various parts of the menu button:

| **Name**                | **Type**  | **Default Value** | **Description**                                                            |
|-------------------------|-----------|-------------------|----------------------------------------------------------------------------|
| `Root`                  | `string?` | `null`            | Custom CSS for the root element.                                           |
| `Opened`                | `string?` | `null`            | CSS for the callout when it is open.                                       |
| `OperatorButton`        | `string?` | `null`            | CSS for the operator (side) button.                                        |
| `OperatorButtonIcon`    | `string?` | `null`            | CSS for the operator button icon.                                          |
| `OperatorButtonText`    | `string?` | `null`            | CSS for the operator button text.                                          |
| `Callout`               | `string?` | `null`            | CSS for the callout panel.                                                 |
| `CalloutContainer`      | `string?` | `null`            | CSS for the container wrapping the callout.                              |
| `ChevronDownButton`     | `string?` | `null`            | CSS for the chevron button element.                                        |
| `ChevronDown`           | `string?` | `null`            | CSS for the chevron icon.                                                  |
| `Separator`             | `string?` | `null`            | CSS for the separator element (if used).                                   |
| `Icon`                  | `string?` | `null`            | CSS for the icon element in the header.                                    |
| `ItemWrapper`           | `string?` | `null`            | CSS for wrapping each item.                                                |
| `ItemButton`            | `string?` | `null`            | CSS for each item’s clickable button.                                      |
| `ItemIcon`              | `string?` | `null`            | CSS for each item’s icon.                                                  |
| `ItemText`              | `string?` | `null`            | CSS for the text inside each item.                                         |
| `Overlay`               | `string?` | `null`            | CSS for the overlay displayed during interactions.                       |
| `Text`                  | `string?` | `null`            | CSS for the header text.                                                   |

### BitMenuButtonNameSelectors Properties

These selectors help extract item property values from your data:

| **Name**   | **Type**                                               | **Default Value**                                     | **Description**                                                 |
|------------|--------------------------------------------------------|-------------------------------------------------------|-----------------------------------------------------------------|
| `Class`    | `BitNameSelectorPair<TItem, string?>`                  | `new(nameof(BitMenuButtonItem.Class))`               | Selector for the CSS class of an item.                          |
| `IconName` | `BitNameSelectorPair<TItem, string?>`                  | `new(nameof(BitMenuButtonItem.IconName))`            | Selector for the icon name of an item.                           |
| `IsEnabled`| `BitNameSelectorPair<TItem, bool>`                     | `new(nameof(BitMenuButtonItem.IsEnabled))`           | Selector for the enabled state.                                 |
| `IsSelected`| `BitNameSelectorPair<TItem, bool>`                    | `new(nameof(BitMenuButtonItem.IsSelected))`          | Selector for the selected state.                                |
| `Key`      | `BitNameSelectorPair<TItem, string?>`                  | `new(nameof(BitMenuButtonItem.Key))`                 | Selector for the unique key of an item.                          |
| `OnClick`  | `BitNameSelectorPair<TItem, Action<TItem>?>`           | `new(nameof(BitMenuButtonItem.OnClick))`             | Selector for the item’s click event handler.                    |
| `Style`    | `BitNameSelectorPair<TItem, string?>`                  | `new(nameof(BitMenuButtonItem.Style))`               | Selector for the item’s inline styles.                          |
| `Text`     | `BitNameSelectorPair<TItem, string?>`                  | `new(nameof(BitMenuButtonItem.Text))`                | Selector for the item text.                                     |

---

## Enums

### BitButtonType Enum

| **Name**  | **Value** | **Description**                                  |
|-----------|-----------|--------------------------------------------------|
| `Button`  | `0`       | A standard clickable button.                     |
| `Submit`  | `1`       | A submit button (for form submissions).          |
| `Reset`   | `2`       | A reset button (resets form data).               |

### BitColor Enum

| **Name**              | **Value** | **Description**                                 |
|-----------------------|-----------|-------------------------------------------------|
| `Primary`             | `0`       | Primary (default) color.                        |
| `Secondary`           | `1`       | Secondary color.                                |
| `Tertiary`            | `2`       | Tertiary color.                                 |
| `Info`                | `3`       | Info color.                                     |
| `Success`             | `4`       | Success color.                                  |
| `Warning`             | `5`       | Warning color.                                  |
| `SevereWarning`       | `6`       | Severe warning color.                           |
| `Error`               | `7`       | Error color.                                    |
| `PrimaryBackground`   | `8`       | Primary background color.                       |
| `SecondaryBackground` | `9`       | Secondary background color.                     |
| `TertiaryBackground`  | `10`      | Tertiary background color.                      |
| `PrimaryForeground`   | `11`      | Primary foreground color.                       |
| `SecondaryForeground` | `12`      | Secondary foreground color.                     |
| `TertiaryForeground`  | `13`      | Tertiary foreground color.                      |
| `PrimaryBorder`       | `14`      | Primary border color.                           |
| `SecondaryBorder`     | `15`      | Secondary border color.                         |
| `TertiaryBorder`      | `16`      | Tertiary border color.                          |

### BitSize Enum

| **Name**  | **Value** | **Description**           |
|-----------|-----------|---------------------------|
| `Small`   | `0`       | Small size.               |
| `Medium`  | `1`       | Medium size (default).    |
| `Large`   | `2`       | Large size.               |

### BitVariant Enum

| **Name**  | **Value** | **Description**             |
|-----------|-----------|-----------------------------|
| `Fill`    | `0`       | Fill style variant.         |
| `Outline` | `1`       | Outline style variant.      |
| `Text`    | `2`       | Text style variant.         |

### BitVisibility Enum

| **Name**    | **Value** | **Description**                                                 |
|-------------|-----------|-----------------------------------------------------------------|
| `Visible`   | `0`       | The component is visible.                                       |
| `Hidden`    | `1`       | The component is hidden (visibility: hidden; space remains).     |
| `Collapsed` | `2`       | The component is collapsed (display: none).                     |

### BitDir Enum

| **Name** | **Value** | **Description**                                                                        |
|----------|-----------|----------------------------------------------------------------------------------------|
| `Ltr`    | `0`       | Left-to-right direction (for languages like English).                                  |
| `Rtl`    | `1`       | Right-to-left direction (for languages like Arabic).                                   |
| `Auto`   | `2`       | Auto-detects direction based on content.                                               |

---

## Events

The `BitMenuButton` component exposes several event callbacks:

- **OnClick**: Invoked when the menu button header is clicked.
- **OnChange**: Invoked when the selected item changes.
- **Item OnClick**: Each item or option can define its own click event.

These callbacks allow you to implement both one-way and two-way data binding for interactive menu behavior.

---

## Binding Examples

### Default Selected Item

Set the `DefaultSelectedItem` to pre-select an item:

```razor
<BitMenuButton DefaultSelectedItem="ItemB">
    <!-- Define options -->
</BitMenuButton>
```

### Two-way Binding

Bind the `SelectedItem` property for dynamic updates:

```razor
<BitMenuButton @bind-SelectedItem="currentItem">
    <!-- Define options -->
</BitMenuButton>

@code {
    private string currentItem = "ItemB";
}
```

### Managing the Open State

Control the callout's open state with the `IsOpen` property:

```razor
<BitMenuButton @bind-IsOpen="isMenuOpen">
    <!-- Define options -->
</BitMenuButton>

@code {
    private bool isMenuOpen = false;
}
```

---

## Templates

Customize the component with your own templates:

- **HeaderTemplate**: Override the default header.
- **ItemTemplate**: Customize how each item or option is rendered.

Example:

```razor
<BitMenuButton HeaderTemplate="@HeaderContent">
    <BitMenuButtonOption Text="Option 1" />
    <BitMenuButtonOption Text="Option 2" />
</BitMenuButton>

@code {
    RenderFragment HeaderContent = @<div style="font-weight: bold;">Custom Header</div>;
}
```

---

## RTL (Right-to-Left) Support

For languages written from right to left, set the `dir` attribute or the `Dir` parameter to `BitDir.Rtl`:

```razor
<BitMenuButton dir="rtl" Text="گزینه ها">
    <BitMenuButtonOption Text="گزینه الف" />
    <BitMenuButtonOption Text="گزینه ب" />
    <BitMenuButtonOption Text="گزینه ج" />
</BitMenuButton>
```

---