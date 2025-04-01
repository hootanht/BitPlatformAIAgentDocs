# BitNav Component Reference

This document serves as a comprehensive guide to the **BitNav** component – a versatile navigation pane used in Blazor applications. BitNav can be used as a standard navigation menu or as a Tree/TreeView to display hierarchical parent-child data. It supports multiple APIs and provides extensive customization options.

---

## Overview

**BitNav** is a navigation component that helps users access the main areas of an application or website. It can be configured in different modes:
- **Tree:** Displays a hierarchical list of navigation items.
- **TreeView:** Similar to Tree but optimized for more complex parent-child relationships.

**Key Features:**
- **Multi-API Support:** Accepts items in three different ways:
  1. As instances of the `BitNavItem` class.
  2. As a custom generic class.
  3. As `BitNavOption` components.
- **Customization:** Customize using templates, CSS classes, and inline styles.
- **Responsive Layouts:** Render as full width, fit width, or custom-sized based on content.
- **Accessibility:** Supports ARIA attributes and right-to-left (RTL) layouts.

---

## Usage

### Basic Example

This basic example shows a navigation menu with a few items. Each item is rendered as a button or link with an optional description.

```html
<nav id="5b3uph" role="navigation" class="bit-nav bit-nav-apbg bit-nav-pri">
  <ul role="list">
    <li role="listitem">
      <button type="button" title="bit platform" tabindex="-1" class="bit-nav-ict" style="padding-inline-start:0px;">
        <div class="bit-nav-mct">
          <div tabindex="0" type="button" class="bit-nav-cbt" aria-expanded="false">
            <i class="bit-icon bit-icon--ChevronRight bit-ico-r90" aria-hidden="true"></i>
          </div>
          <div class="bit-nav-itm">
            <span class="bit-nav-itx">bit platform</span>
          </div>
        </div>
        <div title="the bit platform description" class="bit-nav-des" style="padding-inline-start:27px;">
          the bit platform description
        </div>
      </button>
    </li>
    <li role="listitem">
      <button type="button" title="Community" tabindex="-1" class="bit-nav-ict" style="padding-inline-start:0px;">
        <div class="bit-nav-mct">
          <div tabindex="0" type="button" class="bit-nav-cbt" aria-expanded="false">
            <i class="bit-icon bit-icon--ChevronRight bit-ico-r90" aria-hidden="true"></i>
          </div>
          <div class="bit-nav-itm">
            <span class="bit-nav-itx">Community</span>
          </div>
        </div>
      </button>
    </li>
    <li role="listitem">
      <a href="/iconography" tabindex="-1" title="Iconography" class="bit-nav-ict" style="padding-inline-start:27px;">
        <div class="bit-nav-mct">
          <div class="bit-nav-itm">
            <i class="bit-nav-iic bit-icon bit-icon--AppIconDefault" aria-hidden="true"></i>
            <span class="bit-nav-itx">Iconography</span>
          </div>
        </div>
      </a>
    </li>
  </ul>
</nav>
```

### FitWidth Example

The **FitWidth** mode renders the navigation pane using only as much width as its content requires.

```html
<nav id="kfqllc" role="navigation" class="bit-nav bit-nav-ftw bit-nav-apbg bit-nav-pri">
  <!-- Similar structure as the basic example with FitWidth styling -->
</nav>
```

### Grouped Example

In Grouped mode, nav items are organized into groups with custom headers. This is ideal for displaying items in a categorized tree.

```html
<nav id="2r19en" role="navigation" class="bit-nav bit-nav-apbg bit-nav-pri">
  <ul role="list">
    <li role="listitem">
      <button tabindex="0" type="button" class="bit-nav-gcb" aria-expanded="true" aria-label="Mercedes-Benz Collapsed">
        <div class="bit-nav-itg">
          <div class="bit-nav-iit">
            <i class="bit-icon bit-icon--ChevronRight bit-nav-exp" aria-hidden="true"></i>
            <span class="bit-nav-ghd">Mercedes-Benz</span>
          </div>
          <div title="Cars manufactured under the brand of Mercedes-Benz" class="bit-nav-des" style="padding-inline-start:27px;">
            Cars manufactured under the brand of Mercedes-Benz
          </div>
        </div>
      </button>
      <ul role="list">
        <li role="listitem">
          <button type="button" title="SUVs" tabindex="-1" class="bit-nav-ict" style="padding-inline-start:16px;">
            <div class="bit-nav-mct">
              <div tabindex="0" type="button" class="bit-nav-cbt" aria-expanded="false">
                <i class="bit-icon bit-icon--ChevronRight bit-ico-r90" aria-hidden="true"></i>
              </div>
              <div class="bit-nav-itm">
                <span class="bit-nav-itx">SUVs</span>
              </div>
            </div>
          </button>
        </li>
        <!-- More grouped child items -->
      </ul>
    </li>
    <!-- More groups -->
  </ul>
</nav>
```

### Manual Mode Example

In Manual mode the navigation component does not automatically update the selected item. Instead, selection changes are managed externally.

```html
<!-- Manual mode example: the selected item is bound to a value provided by the parent component -->
```

### IconOnly Example

The **IconOnly** mode renders only the icons (hiding the text) of the navigation items. This mode is useful for minimalist designs.

```html
<!-- Example of IconOnly nav where only icons are displayed -->
```

### RTL (Right-to-Left) Example

For RTL languages (such as Arabic or Hebrew), the component can be rendered with a reversed layout.

```html
<div dir="rtl">
  <nav id="9gwvhc" role="navigation" class="bit-nav bit-rtl bit-nav-apbg bit-nav-pri" dir="rtl">
    <ul role="list">
      <li role="listitem">
        <button type="button" title="پلتفرمِ بیت" tabindex="-1" class="bit-nav-ict" style="padding-inline-start:0px;">
          <div class="bit-nav-mct">
            <div tabindex="0" type="button" class="bit-nav-cbt" aria-expanded="false">
              <i class="bit-icon bit-icon--ChevronRight bit-ico-r90" aria-hidden="true"></i>
            </div>
            <div class="bit-nav-itm">
              <span class="bit-nav-itx">پلتفرمِ بیت</span>
            </div>
          </div>
          <div title="توضیحاتِ پلتفرمِ بیت" class="bit-nav-des" style="padding-inline-start:27px;">
            توضیحاتِ پلتفرمِ بیت
          </div>
        </button>
      </li>
      <!-- Additional RTL nav items -->
    </ul>
  </nav>
</div>
```

---

## API Reference

### BitNav Component Parameters

| Name                       | Type                           | Default                                    | Description                                                                                         |
| -------------------------- | ------------------------------ | ------------------------------------------ | --------------------------------------------------------------------------------------------------- |
| `Accent`                   | `BitColor?`                    | `null`                                     | The accent color of the nav.                                                                        |
| `ChevronDownIcon`          | `string?`                      | `null`                                     | Custom icon name for the chevron-down element.                                                      |
| `ChildContent`             | `RenderFragment?`              | `null`                                     | Content to render as children (nav items).                                                         |
| `Classes`                  | `BitNavClassStyles?`           | `null`                                     | Custom CSS classes for various parts of the BitNav component.                                       |
| `Color`                    | `BitColor?`                    | `null`                                     | General color used for elements like icons.                                                        |
| `DefaultSelectedItem`      | `TItem?`                       | `null`                                     | The initially selected item (used in manual mode).                                                |
| `FitWidth`                 | `bool`                         | `false`                                    | Renders the nav in a width that fits its content.                                                  |
| `FullWidth`                | `bool`                         | `false`                                    | Renders the nav to span the full width of its container.                                           |
| `HeaderTemplate`           | `RenderFragment<TItem>?`       | `null`                                     | Custom template for group headers in grouped mode.                                                |
| `HeaderTemplateRenderMode` | `BitNavItemTemplateRenderMode` | `BitNavItemTemplateRenderMode.Normal`      | Specifies how the header template is rendered.                                                     |
| `IconOnly`                 | `bool`                         | `false`                                    | When true, renders only the icons for nav items.                                                   |
| `IndentValue`              | `int`                          | `16`                                       | Pixel value for the indentation of each child level.                                               |
| `IndentPadding`            | `int`                          | `27`                                       | Padding in pixels for items without children (to compensate for the chevron).                        |
| `IndentReversedPadding`    | `int`                          | `4`                                        | Padding in pixels for items in reversed mode.                                                      |
| `Items`                    | `IList<TItem>`                 | `new List<TItem>()`                        | Collection of items to be rendered in the nav.                                                     |
| `ItemTemplate`             | `RenderFragment<TItem>?`       | `null`                                     | Custom template for rendering individual nav items.                                               |
| `ItemTemplateRenderMode`   | `BitNavItemTemplateRenderMode` | `BitNavItemTemplateRenderMode.Normal`      | Render mode for the custom item template.                                                         |
| `Mode`                     | `BitNavMode`                   | `BitNavMode.Automatic`                     | Determines whether the nav automatically manages the selected item or not.                         |
| `NameSelectors`            | `BitNavNameSelectors<TItem>?`  | `null`                                     | Names and selectors for custom input properties.                                                   |
| `OnItemClick`              | `EventCallback<TItem>`         |                                            | Callback invoked when a nav item is clicked.                                                       |
| `OnItemToggle`             | `EventCallback<TItem>`         |                                            | Callback invoked when a group header is toggled (expanded or collapsed).                           |
| `OnSelectItem`             | `EventCallback<TItem>`         |                                            | Callback invoked when a nav item is selected.                                                      |
| `RenderType`               | `BitNavRenderType`             | `BitNavRenderType.Normal`                  | Determines how nav items are rendered (normal or grouped).                                         |
| `Reselectable`             | `bool`                         | `false`                                    | When true, re-select events are fired even if the same item is selected.                           |
| `ReversedChevron`          | `bool`                         | `false`                                    | When true, reverses the location of the expander chevron.                                          |
| `SelectedItem`             | `TItem?`                       | `null`                                     | The currently selected nav item.                                                                   |
| `SingleExpand`             | `bool`                         | `false`                                    | Enables single-expand mode (only one group expanded at a time).                                     |
| `Styles`                   | `BitNavClassStyles?`           | `null`                                     | Custom inline styles for various parts of the BitNav component.                                    |

### BitComponentBase Parameters

| Name             | Type                            | Default                                 | Description                                                                               |
| ---------------- | ------------------------------- | --------------------------------------- | ----------------------------------------------------------------------------------------- |
| `AriaLabel`      | `string?`                       | `null`                                  | ARIA label for the root element for improved accessibility.                             |
| `Class`          | `string?`                       | `null`                                  | Custom CSS class for the root element.                                                    |
| `Dir`            | `BitDir?`                       | `null`                                  | Sets the text direction (LTR or RTL) for the component.                                   |
| `HtmlAttributes` | `Dictionary<string, object>`    | `new Dictionary<string, object>()`      | Additional HTML attributes to be applied to the component.                                |
| `Id`             | `string?`                       | `null`                                  | Custom id for the component’s root element (a unique id is generated if not provided).      |
| `IsEnabled`      | `bool`                          | `true`                                  | Determines whether the component is enabled.                                              |
| `Style`          | `string?`                       | `null`                                  | Inline styles for the root element.                                                       |
| `Visibility`     | `BitVisibility`                 | `BitVisibility.Visible`                 | Controls whether the component is visible, hidden, or collapsed.                           |

---

## Custom Templates

BitNav supports custom templates for both group headers and individual nav items. Use the `HeaderTemplate` to override the default header rendering in grouped mode, and the `ItemTemplate` to customize individual item appearance.

**Example of a custom header template (Grouped mode):**

```html
<nav id="db97jg" role="navigation" class="bit-nav bit-nav-apbg bit-nav-pri">
  <ul role="list">
    <li role="listitem">
      <button tabindex="0" type="button" class="bit-nav-gcb" aria-expanded="true" aria-label="Mercedes-Benz Collapsed">
        <div class="nav-custom-header">
          <i class="bit-ico bit-ico-pri bit-icon bit-icon--FavoriteStarFill bit-ico-md bit-ico-txt"></i>
          <span>Mercedes-Benz</span>
        </div>
      </button>
      <ul role="list">
        <!-- Child items go here -->
      </ul>
    </li>
  </ul>
</nav>
```

---

## Events

The **BitNav** component provides several events that allow you to handle user interactions:

- **OnItemClick:** Invoked when a nav item is clicked.
- **OnItemToggle:** Invoked when a group header is toggled (expanded or collapsed).
- **OnSelectItem:** Invoked when a nav item is selected.

These callbacks enable you to update state, perform navigation, or trigger other actions in your application.

---

## Additional Customizations

### Custom Styles

Customize the appearance of BitNav by providing your own CSS classes or inline styles using the `Classes` and `Styles` parameters. For example:

```html
<nav class="bit-nav custom-nav-class" style="border: 1px solid green;">
  <!-- Nav content goes here -->
</nav>
```

### Icon and Color Customizations

- **Accent & Color:** Set the `Accent` and `Color` properties to control the overall look of the nav.
- **ChevronDownIcon:** Customize the icon used for dropdown indicators.
- **BitColor Enum:** Use standard BitColor values for consistency across your application.

### RTL Support

To support right-to-left (RTL) languages, add the `bit-rtl` class and set the `dir="rtl"` attribute on the nav container:

```html
<div dir="rtl">
  <nav id="9gwvhc" role="navigation" class="bit-nav bit-rtl bit-nav-apbg bit-nav-pri" dir="rtl">
    <ul role="list">
      <li role="listitem">
        <button type="button" title="پلتفرمِ بیت" tabindex="-1" class="bit-nav-ict" style="padding-inline-start:0px;">
          <div class="bit-nav-mct">
            <div tabindex="0" type="button" class="bit-nav-cbt" aria-expanded="false">
              <i class="bit-icon bit-icon--ChevronRight bit-ico-r90" aria-hidden="true"></i>
            </div>
            <div class="bit-nav-itm">
              <span class="bit-nav-itx">پلتفرمِ بیت</span>
            </div>
          </div>
          <div title="توضیحاتِ پلتفرمِ بیت" class="bit-nav-des" style="padding-inline-start:27px;">
            توضیحاتِ پلتفرمِ بیت
          </div>
        </button>
      </li>
      <!-- Additional RTL nav items -->
    </ul>
  </nav>
</div>
```

---