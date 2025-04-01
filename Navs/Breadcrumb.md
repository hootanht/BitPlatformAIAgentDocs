# BitBreadcrumb Component Reference

This document serves as a comprehensive guide to the **BitBreadcrumb** component. It explains how to use and customize the component, details its API, and offers code examples. Use this file as a reference when integrating BitBreadcrumb into your projects.

---

## Overview

**BitBreadcrumb** is a navigational UI component designed to display a breadcrumb trail for users. It helps users understand their current location within a hierarchical structure and provides one-click access to previous levels. The component is highly customizable and supports multiple API patterns.

### Key Features
- **Multiple API Options:**  
  - Use the `BitBreadcrumbItem` class.
  - Use a custom generic class.
  - Use the `BitBreadcrumbOption` component.
- **Display Control:**  
  - Limit the number of displayed items with `MaxDisplayedItems`.
  - Group the remaining items in an overflow menu using `OverflowIndex`.
- **Customizable Icons and Templates:**  
  - Customize divider icons, overflow icons, and item icons.
  - Use custom templates for items, overflow items, and dividers.
- **Right-to-Left (RTL) Support:**  
  - Easily switch layouts for languages written from right to left.

---

## Usage

### Basic Implementation

A simple implementation of BitBreadcrumb might look like this:

```html
<div class="bit-brc">
  <ul class="bit-brc-icn">
    <li>
      <a href="/components/breadcrumb">
        <span>Item 1</span>
      </a>
    </li>
    <li>
      <i class="bit-brc-div bit-icon bit-icon--ChevronRight"></i>
    </li>
    <li>
      <a href="/components/breadcrumb">
        <span>Item 2</span>
      </a>
    </li>
    <li>
      <i class="bit-brc-div bit-icon bit-icon--ChevronRight"></i>
    </li>
    <li>
      <a href="/components/breadcrumb" aria-current="page" class="bit-brc-sel">
        <span>Item 4</span>
      </a>
    </li>
  </ul>
</div>
```

### Disabled and Item-Disabled States

For scenarios where items are not interactive, you can render them as disabled:

```html
<!-- Disabled Breadcrumb Example -->
<div class="bit-brc bit-dis">
  <ul class="bit-brc-icn">
    <li>
      <span class="bit-brc-nii bit-brc-dis">
        <span>Item 1</span>
      </span>
    </li>
    <!-- More disabled items go here -->
  </ul>
</div>
```

### Handling Overflow

To control how many breadcrumb items are displayed, use the `MaxDisplayedItems` and `OverflowIndex` parameters. Items beyond the limit will be grouped into an overflow menu.

```html
<!-- Breadcrumb with Overflow Items -->
<div class="bit-brc">
  <ul class="bit-brc-icn">
    <li>
      <button class="bit-brc-obt">
        <i class="bit-icon bit-icon--More"></i>
      </button>
    </li>
    <li>
      <a href="/components/breadcrumb" aria-current="page" class="bit-brc-sel">
        <span>Item 4</span>
      </a>
    </li>
  </ul>
</div>
```

### Custom Icons

Customize icons (such as overflow, divider, and item icons) by providing different icon names or using custom templates:

```html
<!-- Custom Icon Example -->
<div class="bit-brc">
  <ul class="bit-brc-icn">
    <li>
      <a href="/components/breadcrumb">
        <i class="bit-icon bit-icon--AdminELogoInverse32"></i>
        <span>Item 1</span>
      </a>
    </li>
    <li>
      <i class="bit-brc-div bit-icon bit-icon--CaretRightSolid8"></i>
    </li>
    <li>
      <a href="/components/breadcrumb">
        <i class="bit-icon bit-icon--AppsContent"></i>
        <span>Item 2</span>
      </a>
    </li>
    <li>
      <button class="bit-brc-obt">
        <i class="bit-icon bit-icon--ChevronDown"></i>
      </button>
    </li>
    <li>
      <i class="bit-brc-div bit-icon bit-icon--CaretRightSolid8"></i>
    </li>
    <li>
      <a href="/components/breadcrumb" aria-current="page" class="bit-brc-sel">
        <i class="bit-icon bit-icon--ClassNotebookLogo16"></i>
        <span>Item 4</span>
      </a>
    </li>
  </ul>
</div>
```

---

## API Reference

### BitBreadcrumb Parameters

| Name               | Type                                   | Default | Description                                                                              |
| ------------------ | -------------------------------------- | ------- | ---------------------------------------------------------------------------------------- |
| `ChildContent`     | `RenderFragment?`                      | `null`  | The content of the BitBreadcrumb, typically composed of BitBreadcrumbOption components.  |
| `Classes`          | `BitBreadcrumbClassStyles?`            | `null`  | Custom CSS classes for different parts of the breadcrumb.                                |
| `DividerIconName`  | `string?`                              | `null`  | The name of the divider icon.                                                            |
| `ItemTemplate`     | `RenderFragment<TItem>?`               | `null`  | Custom template for rendering each breadcrumb item.                                      |
| `MaxDisplayedItems`| `uint`                                 | `0`     | Maximum number of breadcrumb items to display before collapsing the rest.                |
| `NameSelectors`    | `BitBreadcrumbNameSelectors<TItem>?`   | `null`  | Custom selectors for binding item properties.                                            |
| `OnItemClick`      | `EventCallback<TItem>`                 |         | Event triggered when a breadcrumb item is clicked.                                       |
| `OverflowAriaLabel`| `string?`                              | `null`  | Aria-label for the overflow button.                                                      |
| `OverflowIndex`    | `uint`                                 | `0`     | Index at which overflow items will be collapsed.                                         |
| `OverflowIconName` | `string`                               | `More`  | Icon name for the overflow button.                                                       |
| `OverflowTemplate` | `RenderFragment<TItem>?`               | `null`  | Custom template for each item in the overflow list.                                      |
| `ReversedIcon`     | `bool`                                 | `false` | If set to true, reverses the positions of the icon and text in the breadcrumb item.        |
| `Styles`           | `BitBreadcrumbClassStyles?`            | `null`  | Custom CSS styles for various parts of the breadcrumb.                                   |

*(For a complete API reference, see the BitPlatform documentation or the component source code.)*

### BitComponentBase Parameters

| Name         | Type                   | Default                                | Description                                                                       |
| ------------ | ---------------------- | -------------------------------------- | --------------------------------------------------------------------------------- |
| `AriaLabel`  | `string?`              | `null`                                 | Aria-label of the component, for accessibility.                                  |
| `Class`      | `string?`              | `null`                                 | Custom CSS class for the root element.                                           |
| `Dir`        | `BitDir?`              | `null`                                 | Determines the direction (LTR/RTL) of the component.                             |
| `HtmlAttributes` | `Dictionary<string, object>` | `new Dictionary<string, object>()` | Additional attributes to be applied to the component's root element.              |
| `Id`         | `string?`              | `null`                                 | Custom id for the root element. If not provided, a unique id is generated.         |
| `IsEnabled`  | `bool`                 | `true`                                 | Whether the component is enabled.                                                |
| `Style`      | `string?`              | `null`                                 | Custom inline styles for the root element.                                       |
| `Visibility` | `BitVisibility`        | `BitVisibility.Visible`                | Controls whether the component is visible, hidden, or collapsed.                 |

### BitBreadcrumbItem Properties

| Name          | Type         | Default | Description                                                     |
| ------------- | ------------ | ------- | --------------------------------------------------------------- |
| `Key`         | `string?`    |         | Unique key for the breadcrumb item.                             |
| `Text`        | `string?`    |         | The text to display in the breadcrumb item.                     |
| `Href`        | `string?`    |         | URL to navigate to when the item is clicked.                    |
| `Class`       | `string?`    |         | Custom CSS class for the breadcrumb item.                       |
| `Style`       | `string?`    |         | Inline styles for the breadcrumb item.                          |
| `IconName`    | `string?`    |         | Icon name to render next to the item text.                      |
| `ReversedIcon`| `bool?`      |         | Reverses the icon and text positions if true.                   |
| `IsSelected`  | `bool`       |         | Indicates whether the item is the currently selected item.      |
| `IsEnabled`   | `bool`       | `true`  | Indicates whether the item is enabled.                          |
| `OnClick`     | `Action<BitBreadcrumbItem>?` |   | Click event handler for the item.                               |
| `OverflowTemplate` | `RenderFragment<BitBreadcrumbItem>?` | | Custom template for the item when rendered in the overflow menu. |
| `Template`    | `RenderFragment<BitBreadcrumbItem>?` | | Custom template for the item.                                    |

### BitBreadcrumbOption Properties

| Name       | Type         | Default | Description                                                     |
| ---------- | ------------ | ------- | --------------------------------------------------------------- |
| `Key`      | `string?`    |         | Unique key for the breadcrumb option.                           |
| `Text`     | `string?`    |         | Text to display in the breadcrumb option.                       |
| `Href`     | `string?`    |         | URL to navigate to when the option is clicked.                  |
| `Class`    | `string?`    |         | Custom CSS class for the breadcrumb option.                     |
| `Style`    | `string?`    |         | Inline styles for the breadcrumb option.                        |
| `IconName` | `string?`    |         | Icon name to render next to the option text.                    |
| `ReversedIcon` | `bool?` |         | Reverses the icon and text positions if true.                   |
| `IsSelected` | `bool`    |         | Indicates whether the option is currently selected.             |
| `IsEnabled`  | `bool`    | `true`  | Indicates whether the option is enabled.                        |
| `OnClick`   | `EventCallback<BitBreadcrumbOption>` | | Click event handler for the option.                             |
| `OverflowTemplate` | `RenderFragment<BitBreadcrumbItem>?` | | Custom template for the option in the overflow list. |
| `Template`  | `RenderFragment<BitBreadcrumbItem>?` | | Custom template for the option.                                 |

---

## Customizations

BitBreadcrumb allows extensive customization:

- **Icons:**  
  Customize the divider, overflow, and item icons by setting properties such as `DividerIconName` and `OverflowIconName`, or by providing custom templates.

- **Templates:**  
  Use custom templates for:
  - **DividerIconTemplate:** Customize the appearance of the divider between items.
  - **ItemTemplate:** Override the default rendering of each breadcrumb item.
  - **OverflowTemplate:** Define how overflow items appear in the dropdown menu.

- **CSS Classes and Styles:**  
  Override the default styling by providing custom CSS classes and inline styles using the `Classes` and `Styles` parameters. Detailed class selectors (for the root, overlay, item container, overflow button, etc.) are available in the API reference.

- **Dynamic Content:**  
  The component supports dynamic addition and removal of items, allowing you to update the breadcrumb trail as the user navigates.

---

## Events

- **OnItemClick:**  
  An event callback that is invoked when a breadcrumb item is clicked. Use this event to update the active state or perform navigation logic.

---

## Right-to-Left (RTL) Support

For applications that use right-to-left languages (e.g., Arabic), BitBreadcrumb supports RTL layouts. Simply add the `dir="rtl"` attribute and the `bit-rtl` class to the root element:

```html
<div class="bit-brc bit-rtl" dir="rtl">
  <ul class="bit-brc-icn">
    <li>
      <span class="bit-brc-nii"><span>پوشه اول</span></span>
    </li>
    <li>
      <i class="bit-brc-div bit-icon bit-icon--ChevronRight"></i>
    </li>
    <li>
      <span class="bit-brc-nii bit-brc-sel"><span>پوشه دوم</span></span>
    </li>
    <!-- Additional RTL items... -->
  </ul>
</div>
```

---