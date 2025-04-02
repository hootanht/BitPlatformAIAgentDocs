# BitButtonGroup Component Documentation

This document describes the **BitButtonGroup** component including its API, parameters, properties, styling options, and related enums. It is intended as a reference for developers and AI agents to quickly understand the component's features and usage.

---

## Overview

The **BitButtonGroup** component is used to render a group of buttons with various customization options. It supports features such as:
- Custom items with icons, text, and toggle mode.
- Adjustable size and layout (horizontal or vertical).
- Custom styling via CSS classes and inline styles.
- Support for accessibility attributes and right-to-left (RTL) layouts.
- Integration with event callbacks for item clicks.

---

## API Reference

### BitButtonGroup Parameters

| Name         | Type                                    | Default Value         | Description                                                                                         |
|--------------|-----------------------------------------|-----------------------|-----------------------------------------------------------------------------------------------------|
| **ChildContent** | `RenderFragment?`                    | `null`                | The content of the BitButtonGroup, usually a set of BitButtonGroupOption components.               |
| **IconOnly**     | `bool`                             | `false`               | Determines that only the icon should be rendered for each button.                                  |
| **Classes**      | `BitButtonGroupClassStyles?`         | `null`                | Custom CSS classes for different parts of the ButtonGroup.                                          |
| **Color**        | `BitColor?`                        | `null`                | The general color of the button group.                                                              |
| **FullWidth**    | `bool`                             | `false`               | Expands the ButtonGroup to 100% of the available width.                                             |
| **Items**        | `IEnumerable<TItem>`               | `new List<TItem>()`   | The list of items, where each item represents a button with its own properties and actions.         |
| **ItemTemplate** | `RenderFragment<TItem>?`           | `null`                | Custom template to render the content of each item.                                                 |
| **NameSelectors**| `BitButtonGroupNameSelectors<TItem>?` | `null`             | Defines names and selectors for the custom input type properties for each item.                     |
| **OnItemClick**  | `EventCallback<TItem>`             | (none)                | Callback that is called when a button is clicked.                                                  |
| **Options**      | `RenderFragment?`                  | `null`                | Alias of *ChildContent* – allows defining the options using a template.                             |
| **Toggle**       | `bool`                             | `false`               | When true, enables toggle mode for each button.                                                    |
| **Size**         | `BitSize`                          | `null`                | The size of the ButtonGroup. Possible values: `Small`, `Medium`, or `Large`.                        |
| **Styles**       | `BitButtonGroupClassStyles?`         | `null`                | Custom CSS styles for different parts of the ButtonGroup.                                           |
| **Variant**      | `BitVariant?`                      | `null`                | The visual variant of the button group. Options: `Fill`, `Outline`, or `Text`.                      |
| **Vertical**     | `bool`                             | `false`               | If true, renders the ButtonGroup items vertically instead of the default horizontal layout.         |

---

## Inherited Parameters from BitComponentBase

The BitButtonGroup component inherits from **BitComponentBase**. In addition to its own parameters, it supports these properties:

| Name            | Type                            | Default Value                         | Description                                                                                      |
|-----------------|---------------------------------|---------------------------------------|--------------------------------------------------------------------------------------------------|
| **AriaLabel**   | `string?`                       | `null`                                | The aria-label for screen readers.                                                             |
| **Class**       | `string?`                       | `null`                                | Custom CSS class for the root element of the component.                                        |
| **Dir**         | `BitDir?`                       | `null`                                | Specifies the text direction (e.g., Ltr, Rtl, Auto).                                             |
| **HtmlAttributes** | `Dictionary<string, object>` | `new Dictionary<string, object>()`    | Additional attributes that are applied to the root element.                                    |
| **Id**          | `string?`                       | `null`                                | The id of the root element. If null, a unique id will be generated.                              |
| **IsEnabled**   | `bool`                          | `true`                                | Determines if the component is enabled.                                                        |
| **Style**       | `string?`                       | `null`                                | Inline CSS styles for the root element.                                                        |
| **Visibility**  | `BitVisibility`                 | `BitVisibility.Visible`               | Determines whether the component is visible, hidden, or collapsed.                             |

### Public Members (from BitComponentBase)

| Name          | Type                   | Default Value   | Description                                                            |
|---------------|------------------------|-----------------|------------------------------------------------------------------------|
| **UniqueId**  | `Guid`                 | `Guid.NewGuid()`| A read-only unique identifier assigned at component creation.          |
| **RootElement** | `ElementReference`   | (none)          | A reference to the root DOM element of the component.                  |

---

## BitButtonGroupItem Properties

These properties define each button item within the group.

| Name         | Type      | Default Value | Description                                                                                      |
|--------------|-----------|---------------|--------------------------------------------------------------------------------------------------|
| **Class**        | `string?`   | `null`          | Custom CSS classes for the item.                                                                 |
| **IconName**     | `string?`   | `null`          | The name of the icon displayed alongside the item text.                                        |
| **IsEnabled**    | `bool`      | `true`          | Whether the item is enabled.                                                                     |
| **Key**          | `string?`   | `null`          | A unique key for the item.                                                                       |
| **OffIconName**  | `string?`   | `null`          | Icon when the item is not toggled (off state).                                                   |
| **OffText**      | `string?`   | `null`          | Text when the item is not toggled.                                                               |
| **OffTitle**     | `string?`   | `null`          | Title when the item is not toggled.                                                              |
| **OnIconName**   | `string?`   | `null`          | Icon when the item is toggled (on state).                                                        |
| **OnText**       | `string?`   | `null`          | Text when the item is toggled.                                                                   |
| **OnTitle**      | `string?`   | `null`          | Title when the item is toggled.                                                                  |
| **OnClick**      | `EventCallback` |           | Click event handler for the item.                                                                |
| **ReversedIcon** | `bool`      | `false`         | If true, the icon appears after the text.                                                      |
| **Style**        | `string?`   | `null`          | Inline style for the item.                                                                       |
| **Template**     | `RenderFragment<BitButtonGroupItem>?` | `null` | Custom template for rendering the item.                                                        |
| **Text**         | `string?`   | `null`          | The text displayed on the item.                                                                  |
| **Title**        | `string?`   | `null`          | The title (tooltip) of the item.                                                                 |

---

## BitButtonGroupOption Properties

These properties are used when an option (instead of a standard item) is needed.

| Name         | Type      | Default Value | Description                                                                                      |
|--------------|-----------|---------------|--------------------------------------------------------------------------------------------------|
| **Class**        | `string?`   | `null`          | Custom CSS classes for the option.                                                               |
| **IconName**     | `string?`   | `null`          | The name of the icon to display with the option text.                                            |
| **IsEnabled**    | `bool`      | `true`          | Whether the option is enabled.                                                                   |
| **Key**          | `string?`   | `null`          | A unique key for the option.                                                                     |
| **OffIconName**  | `string?`   | `null`          | Icon when the option is in the off state.                                                        |
| **OffText**      | `string?`   | `null`          | Text when the option is in the off state.                                                        |
| **OffTitle**     | `string?`   | `null`          | Title when the option is in the off state.                                                       |
| **OnIconName**   | `string?`   | `null`          | Icon when the option is in the on state.                                                         |
| **OnText**       | `string?`   | `null`          | Text when the option is in the on state.                                                         |
| **OnTitle**      | `string?`   | `null`          | Title when the option is in the on state.                                                        |
| **OnClick**      | `EventCallback` |           | Click event handler for the option.                                                              |
| **ReversedIcon** | `bool`      | `false`         | If true, the icon is rendered after the text.                                                    |
| **Style**        | `string?`   | `null`          | Inline style for the option.                                                                     |
| **Template**     | `RenderFragment<BitButtonGroupOption>?` | `null` | Custom template for rendering the option.                                                        |
| **Text**         | `string?`   | `null`          | The text displayed on the option.                                                                |
| **Title**        | `string?`   | `null`          | The title (tooltip) for the option.                                                              |

---

## Custom Styles and Classes

### BitButtonGroupClassStyles

These properties allow you to override the default styling of various parts of the ButtonGroup.

| Name           | Type     | Default Value | Description                                                             |
|----------------|----------|---------------|-------------------------------------------------------------------------|
| **Root**       | `string?`| `null`        | Custom CSS classes/styles for the root element of the BitButtonGroup.   |
| **Button**     | `string?`| `null`        | Custom CSS classes/styles for the internal button element.              |
| **Icon**       | `string?`| `null`        | Custom CSS classes/styles for the icon in the ButtonGroup.              |
| **Text**       | `string?`| `null`        | Custom CSS classes/styles for the button text.                          |
| **ToggledButton** | `string?` | `null`    | Custom CSS classes/styles for a button when toggled in toggle mode.       |

### BitButtonGroupNameSelectors

These selectors let you map custom property names for items. They are defined as pairs of a field name and a selector function.

| Name       | Type                                                     | Default Value                                           | Description                                                              |
|------------|----------------------------------------------------------|---------------------------------------------------------|--------------------------------------------------------------------------|
| **Class**     | `BitNameSelectorPair<TItem, string?>`                 | `new(nameof(BitButtonGroupItem.Class))`                 | Field name and selector for the item’s CSS class.                        |
| **IconName**  | `BitNameSelectorPair<TItem, string?>`                 | `new(nameof(BitButtonGroupItem.IconName))`              | Field name and selector for the item’s icon name.                        |
| **IsEnabled** | `BitNameSelectorPair<TItem, bool>`                    | `new(nameof(BitButtonGroupItem.IsEnabled))`             | Field name and selector for whether the item is enabled.                 |
| **Key**       | `BitNameSelectorPair<TItem, string?>`                 | `new(nameof(BitButtonGroupItem.Key))`                   | Field name and selector for the item’s key.                              |
| **OffIconName** | `BitNameSelectorPair<TItem, string?>`               | `new(nameof(BitButtonGroupItem.OffIconName))`           | Field name and selector for the off state icon name.                     |
| **OffText**   | `BitNameSelectorPair<TItem, string?>`                 | `new(nameof(BitButtonGroupItem.OffText))`               | Field name and selector for the off state text.                          |
| **OffTitle**  | `BitNameSelectorPair<TItem, string?>`                 | `new(nameof(BitButtonGroupItem.OffTitle))`              | Field name and selector for the off state title.                         |
| **OnIconName** | `BitNameSelectorPair<TItem, string?>`                | `new(nameof(BitButtonGroupItem.OnIconName))`            | Field name and selector for the on state icon name.                      |
| **OnText**    | `BitNameSelectorPair<TItem, string?>`                 | `new(nameof(BitButtonGroupItem.OnText))`                | Field name and selector for the on state text.                           |
| **OnTitle**   | `BitNameSelectorPair<TItem, string?>`                 | `new(nameof(BitButtonGroupItem.OnTitle))`               | Field name and selector for the on state title.                          |

#### BitNameSelectorPair\<TItem, TProp\>

This type defines a pair containing:
- **Name**: The custom property name.
- **Selector**: A function that takes an item of type TItem and returns the property value of type TProp.

---

## Enums

### BitVariant

| Name    | Value | Description                   |
|---------|-------|-------------------------------|
| **Fill**    | 0     | Fill styled variant.          |
| **Outline** | 1     | Outline styled variant.       |
| **Text**    | 2     | Text styled variant.          |

### BitColor

| Name                | Value | Description                          |
|---------------------|-------|--------------------------------------|
| **Primary**         | 0     | Primary general color.               |
| **Secondary**       | 1     | Secondary general color.             |
| **Tertiary**        | 2     | Tertiary general color.              |
| **Info**            | 3     | Info general color.                  |
| **Success**         | 4     | Success general color.               |
| **Warning**         | 5     | Warning general color.               |
| **SevereWarning**   | 6     | Severe Warning general color.        |
| **Error**           | 7     | Error general color.                 |
| **PrimaryBackground**   | 8  | Primary background color.            |
| **SecondaryBackground** | 9  | Secondary background color.          |
| **TertiaryBackground**  | 10 | Tertiary background color.           |
| **PrimaryForeground**   | 11 | Primary foreground color.            |
| **SecondaryForeground** | 12 | Secondary foreground color.          |
| **TertiaryForeground**  | 13 | Tertiary foreground color.           |
| **PrimaryBorder**       | 14 | Primary border color.                |
| **SecondaryBorder**     | 15 | Secondary border color.              |
| **TertiaryBorder**      | 16 | Tertiary border color.               |

### BitSize

| Name   | Value | Description                  |
|--------|-------|------------------------------|
| **Small**  | 0     | The small size button.       |
| **Medium** | 1     | The medium size button.      |
| **Large**  | 2     | The large size button.       |

### BitButtonType

| Name    | Value | Description                                               |
|---------|-------|-----------------------------------------------------------|
| **Button** | 0   | The button is a clickable button.                         |
| **Submit** | 1   | The button is a submit button (submits form-data).         |
| **Reset**  | 2   | The button is a reset button (resets form-data).           |

### BitVisibility

| Name      | Value | Description                                                                  |
|-----------|-------|------------------------------------------------------------------------------|
| **Visible**   | 0     | The component is visible.                                                   |
| **Hidden**    | 1     | The component is hidden (using `visibility: hidden` so it still occupies space).|
| **Collapsed** | 2     | The component is collapsed (using `display: none`).                         |

### BitDir

| Name  | Value | Description                                                                                                      |
|-------|-------|------------------------------------------------------------------------------------------------------------------|
| **Ltr**   | 0     | Left-to-right layout, used for languages such as English.                                                     |
| **Rtl**   | 1     | Right-to-left layout, used for languages such as Arabic.                                                      |
| **Auto**  | 2     | The user agent automatically determines the direction based on the content.                                   |

---

## RTL Support

To render the **BitButtonGroup** in a right-to-left (RTL) layout, set the `Dir` parameter to `BitDir.Rtl`. For example:

```razor
<BitButtonGroup Dir="BitDir.Rtl" Variant="BitVariant.Fill" Items="rtlItems" />
```

This will render the button group with RTL support.

---

## Feedback

We welcome your feedback! You can share your thoughts and suggestions through our [GitHub repository](https://github.com/bitfoundation/bitplatform):

- **File a new Issue:** [New Issue](https://github.com/bitfoundation/bitplatform/issues/new/choose)
- **Start a new Discussion:** [New Discussion](https://github.com/bitfoundation/bitplatform/discussions/new/choose)

You can also [review](https://github.com/bitfoundation/bitplatform/blob/develop/src/BlazorUI/Demo/Client/Bit.BlazorUI.Demo.Client.Core/Pages/Components/Buttons/ButtonGroup/BitButtonGroupDemo.razor) or [edit](https://github.com/bitfoundation/bitplatform/edit/develop/src/BlazorUI/Demo/Client/Bit.BlazorUI.Demo.Client.Core/Pages/Components/Buttons/ButtonGroup/BitButtonGroupDemo.razor) this page, or [review](https://github.com/bitfoundation/bitplatform/blob/develop/src/BlazorUI/Bit.BlazorUI/Components/Buttons/ButtonGroup/BitButtonGroup.razor) / [edit](https://github.com/bitfoundation/bitplatform/edit/develop/src/BlazorUI/Bit.BlazorUI/Components/Buttons/ButtonGroup/BitButtonGroup.razor) the component itself on GitHub.

---

This documentation file should serve as a comprehensive reference for the **BitButtonGroup** component. It includes all necessary details that an AI agent or developer might need to understand how to use and customize the component.