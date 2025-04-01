# BitNavBar Component Documentation

The **BitNavBar** is a versatile navigation component designed to display navigation links for the main areas of an application. It supports multiple APIs and customization options to render items in different ways, making it highly adaptable to various UI needs.

---

## Overview

The BitNavBar is a **Multi-API component** that accepts a list of items in three different ways:
1. Using the `BitNavBarItem` class.
2. Using a custom generic class.
3. Using the `BitNavBarOption` component.

This flexibility enables developers to choose the approach that best fits their application architecture.

---

## Key Features

- **Multi-API Support:** Render navigation items via classes or components.
- **Customizable Rendering:** Define custom templates, styles, and classes for both the entire navbar and individual items.
- **Responsive Modes:** Support for basic, disabled, manual, icon-only, fit-width, and full-width modes.
- **Event Handling:** Provides callbacks for item clicks and selection changes.
- **RTL Support:** Easily switch the navigation layout for right-to-left languages.
- **Advanced Customization:** Overriding default styles and classes for both the navbar container and its items.

---

## Usage Examples

### Basic Example

A standard BitNavBar rendering with several items:

```razor
<nav class="bit-nbr bit-nbr-pri">
  <div class="bit-nbr-cnt">
    <button type="button" class="bit-nbr-itm">
      <i class="bit-nbr-ico bit-icon bit-icon--Home"></i>
      <span class="bit-nbr-txt">Home</span>
    </button>
    <button type="button" class="bit-nbr-itm">
      <i class="bit-nbr-ico bit-icon bit-icon--ProductVariant"></i>
      <span class="bit-nbr-txt">Products</span>
    </button>
    <!-- Additional items... -->
  </div>
</nav>
```

### Disabled State

Showcase the disabled appearance by setting the appropriate classes and disabling certain items.

### Manual Mode

Configure the navbar to use manual selection. In this mode, the parent component handles the selection changes:

```razor
<BitNavBar Mode="BitNavMode.Manual" DefaultSelectedItem="@initialItem" OnSelectItem="@HandleSelect">
  @foreach (var item in items)
  {
      <BitNavBarItem Text="@item.Text" IconName="@item.IconName" Url="@item.Url" />
  }
</BitNavBar>
```

### Icon-Only Mode

Only icons are rendered instead of text, ideal for compact UIs:

```razor
<BitNavBar IconOnly="true">
  <!-- Define icon-only items here -->
</BitNavBar>
```

### FitWidth Mode

Enables the component’s width to automatically fit its content:

```razor
<BitNavBar FitWidth="true">
  <!-- Navbar items -->
</BitNavBar>
```

### Advanced Customization

Customize templates, styles, and classes both for the navbar and individual items:

```razor
<BitNavBar Class="custom-navbar" Styles="@(new BitNavBarClassStyles { Root = "my-navbar-root" })">
  <BitNavBarItem Class="custom-item" Text="Dashboard" IconName="DashboardIcon" />
  <!-- More items -->
</BitNavBar>
```

---

## API Reference

### BitNavBar Parameters

| Name                | Type                        | Default Value            | Description                                                                             |
|---------------------|-----------------------------|--------------------------|-----------------------------------------------------------------------------------------|
| `ChildContent`      | `RenderFragment?`           | `null`                   | Content to render as children.                                                          |
| `Classes`           | `BitNavClassStyles?`        | `null`                   | Custom CSS classes for different parts of the navbar.                                   |
| `Color`             | `BitColor?`                 | `null`                   | The general color theme of the navbar.                                                  |
| `DefaultSelectedItem` | `TItem?`                  | `null`                   | The initially selected item (used in manual mode).                                      |
| `FitWidth`          | `bool`                      | `false`                  | Renders the navbar with a width that only fits its content.                             |
| `FullWidth`         | `bool`                      | `false`                  | Renders the navbar to span the full width of its container.                             |
| `IconOnly`          | `bool`                      | `false`                  | Only renders the icon for each navbar item.                                             |
| `Items`             | `IList<TItem>`              | `new List<TItem>()`      | A collection of items to display in the navbar.                                         |
| `ItemTemplate`      | `RenderFragment<TItem>?`    | `null`                   | Custom template for rendering content inside each item.                                 |
| `Mode`              | `BitNavMode`                | `BitNavMode.Automatic`   | Determines how navigation selection is handled.                                         |
| `NameSelectors`     | `BitNavNameSelectors<TItem>?`| `null`                  | Names and selectors for custom item properties.                                         |
| `OnItemClick`       | `EventCallback<TItem>`      | —                        | Callback invoked when an item is clicked.                                               |
| `OnSelectItem`      | `EventCallback<TItem>`      | —                        | Callback invoked when an item is selected.                                              |
| `Options`           | `RenderFragment?`           | `null`                   | Alias for `ChildContent`.                                                                 |
| `Reselectable`      | `bool`                      | `false`                  | Enables re-triggering the selection event even when the same item is selected again.      |
| `SelectedItem`      | `TItem?`                    | `null`                   | The currently selected item.                                                            |
| `Styles`            | `BitNavClassStyles?`        | `null`                   | Custom CSS styles for different parts of the navbar.                                    |

---

### BitComponentBase Parameters

These parameters are inherited by BitNavBar:

| Name           | Type                         | Default Value                      | Description                                                                |
|----------------|------------------------------|------------------------------------|----------------------------------------------------------------------------|
| `AriaLabel`    | `string?`                    | `null`                             | ARIA label for accessibility.                                            |
| `Class`        | `string?`                    | `null`                             | Custom CSS class for the root element.                                   |
| `Dir`          | `BitDir?`                    | `null`                             | Specifies the text direction (LTR, RTL, or Auto).                        |
| `HtmlAttributes` | `Dictionary<string, object>` | `new Dictionary<string, object>()` | Additional attributes to be applied to the root element.                 |
| `Id`           | `string?`                    | `null`                             | Custom id for the root element; if null, a unique id is generated.         |
| `IsEnabled`    | `bool`                     | `true`                             | Indicates whether the component is enabled.                              |
| `Style`        | `string?`                    | `null`                             | Inline CSS styles for the root element.                                  |
| `Visibility`   | `BitVisibility`              | `BitVisibility.Visible`            | Controls whether the component is visible, hidden, or collapsed.         |

---

### Public Members

- **UniqueId**: A readonly unique identifier (a new GUID is generated when the component instance is constructed).
- **RootElement**: An `ElementReference` to the root element of the component.

---

### BitNavBarItem Properties

| Name       | Type          | Default Value    | Description                                                              |
|------------|---------------|------------------|--------------------------------------------------------------------------|
| `Class`    | `string?`     | `null`           | Custom CSS class for the navbar item.                                    |
| `Data`     | `object?`     | `null`           | Custom data for additional state.                                       |
| `IconName` | `string?`     | `null`           | Name of the icon to render next to the item.                             |
| `IsEnabled`| `bool`        | `true`           | Whether the navbar item is enabled.                                      |
| `Key`      | `string?`     | `null`           | Unique key or id for the navbar item.                                    |
| `Style`    | `string?`     | `null`           | Custom inline styles for the navbar item.                                |
| `Target`   | `string?`     | `null`           | Specifies how to open the item’s link (e.g., _blank,_self).               |
| `Template` | `RenderFragment<BitNavBarItem>?` | `null` | Custom template for rendering the navbar item.                          |
| `Text`     | `string`      | `string.Empty`   | Text displayed for the navbar item.                                      |
| `Title`    | `string?`     | `null`           | Tooltip text for the navbar item.                                        |
| `Url`      | `string?`     | `null`           | The link URL for the navbar item.                                        |
| `AdditionalUrls` | `IEnumerable<string>?` | `null` | Alternative URLs for auto‑detection in automatic mode.                 |

---

### BitNavBarOption Properties

This sub‑component offers similar customization as BitNavBarItem:

| Name       | Type          | Default Value    | Description                                                              |
|------------|---------------|------------------|--------------------------------------------------------------------------|
| `Class`    | `string?`     | `null`           | Custom CSS class for the navbar option.                                  |
| `Data`     | `object?`     | `null`           | Additional custom data.                                                  |
| `IconName` | `string?`     | `null`           | Name of the icon for the option.                                         |
| `IsEnabled`| `bool`        | `true`           | Whether the option is enabled.                                           |
| `Key`      | `string?`     | `null`           | Unique key or id for the option.                                         |
| `Style`    | `string?`     | `null`           | Inline CSS styles for the option.                                        |
| `Target`   | `string?`     | `null`           | Link target attribute for the option’s URL.                              |
| `Template` | `RenderFragment<BitNavBarOption>?` | `null` | Custom rendering template.                                          |
| `Text`     | `string`      | `string.Empty`   | Text for the option.                                                     |
| `Title`    | `string?`     | `null`           | Tooltip text for the option.                                             |
| `Url`      | `string?`     | `null`           | Link URL for the option.                                                 |
| `AdditionalUrls` | `IEnumerable<string>?` | `null` | Additional URLs to consider in auto‑mode.                             |

---

### BitNavBarNameSelectors<TItem> Properties

This helper class allows you to specify property names and selectors for custom items:

| Name      | Type                                           | Default Value                              | Description                                                                                           |
|-----------|------------------------------------------------|--------------------------------------------|-------------------------------------------------------------------------------------------------------|
| `Class`   | `BitNameSelectorPair<TItem, string?>`          | `new(nameof(BitNavBarItem.Class))`         | Field name and selector for the custom CSS class property.                                          |
| `Data`    | `BitNameSelectorPair<TItem, object?>`          | `new(nameof(BitNavBarItem.Data))`          | Field name and selector for the custom data property.                                               |
| `IconName`| `BitNameSelectorPair<TItem, string?>`          | `new(nameof(BitNavBarItem.IconName))`      | Field name and selector for the icon name.                                                          |
| `IsEnabled`| `BitNameSelectorPair<TItem, bool?>`           | `new(nameof(BitNavBarItem.IsEnabled))`     | Field name and selector for the enabled state.                                                     |
| `Key`     | `BitNameSelectorPair<TItem, string?>`          | `new(nameof(BitNavBarItem.Key))`           | Field name and selector for the unique key.                                                         |
| `Style`   | `BitNameSelectorPair<TItem, string?>`          | `new(nameof(BitNavBarItem.Style))`         | Field name and selector for inline styles.                                                          |
| `Target`  | `BitNameSelectorPair<TItem, string?>`          | `new(nameof(BitNavBarItem.Target))`        | Field name and selector for the link target.                                                        |
| `Template`| `BitNameSelectorPair<TItem, RenderFragment<TItem>?>` | `new(nameof(BitNavBarItem.Template))` | Field name and selector for the custom template.                                                    |
| `Text`    | `BitNameSelectorPair<TItem, string?>`          | `new(nameof(BitNavBarItem.Text))`          | Field name and selector for the text content.                                                       |
| `Title`   | `BitNameSelectorPair<TItem, string?>`          | `new(nameof(BitNavBarItem.Title))`         | Field name and selector for the tooltip text.                                                       |
| `Url`     | `BitNameSelectorPair<TItem, string?>`          | `new(nameof(BitNavBarItem.Url))`           | Field name and selector for the link URL.                                                           |
| `AdditionalUrls` | `BitNameSelectorPair<TItem, IEnumerable<string>?>` | `new(nameof(BitNavBarItem.AdditionalUrls))` | Field name and selector for additional URLs used in auto‑detection.                                  |

---

### BitNavBarClassStyles Properties

Customize the CSS classes for various parts of the navbar:

| Name          | Type      | Default Value | Description                                                         |
|---------------|-----------|---------------|---------------------------------------------------------------------|
| `Root`        | `string?` | `null`        | Custom CSS class for the root element of the BitNavBar.             |
| `Container`   | `string?` | `null`        | Custom CSS class for the container holding the navbar items.        |
| `Item`        | `string?` | `null`        | Custom CSS class for each navbar item.                              |
| `ItemIcon`    | `string?` | `null`        | Custom CSS class for the icon of a navbar item.                     |
| `ItemText`    | `string?` | `null`        | Custom CSS class for the text of a navbar item.                     |
| `SelectedItem`| `string?` | `null`        | Custom CSS class for the selected navbar item.                      |

---

### Enumerations

#### BitNavMode Enum

| Name       | Value | Description                                                                                           |
|------------|-------|-------------------------------------------------------------------------------------------------------|
| **Automatic** | 0   | Selected key is automatically changed using the NavigationManager based on the current URL.            |
| **Manual**    | 1   | Parent component handles the change; the navbar does not automatically update the selected key.      |

#### BitVisibility Enum

| Name      | Value | Description                                                            |
|-----------|-------|------------------------------------------------------------------------|
| **Visible**   | 0   | The component content is visible.                                   |
| **Hidden**    | 1   | The component content is hidden but still occupies space (CSS `visibility: hidden`). |
| **Collapsed** | 2   | The component is not rendered at all (CSS `display: none`).            |

#### BitDir Enum

| Name | Value | Description                                                                                                                     |
|------|-------|---------------------------------------------------------------------------------------------------------------------------------|
| **Ltr**  | 0     | Left-to-right text direction (suitable for languages like English).                                                           |
| **Rtl**  | 1     | Right-to-left text direction (suitable for languages like Arabic).                                                            |
| **Auto** | 2     | Automatically determine directionality based on the content’s strong character direction.                                     |

---