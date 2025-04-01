# BitTimeline Component Reference

This document serves as a comprehensive reference for the **BitTimeline** component. The BitTimeline organizes and displays events or data chronologically along a linear axis. It supports multiple orientations, visual variants, and customization options, making it ideal for showcasing timelines in various UI scenarios.

---

## Overview

The **BitTimeline** component displays a sequence of events or items along a timeline. Each item can represent an event, with a dot (or icon), title, and optional secondary text or content. The component supports:
- **Vertical and Horizontal orientations**
- **Disabled states** for the entire timeline or individual items
- **Multiple visual variants:** Fill (default), Outline, and Text
- **Icons** within items
- **Reversed direction** for flexible layouts
- **Right-to-Left (RTL) support** for languages such as Arabic

---

## Notes

The BitTimeline is a **Multi-API** component that can accept the list of timeline items in three different ways:
1. **BitTimelineItem** class – Use this class to define individual timeline items.
2. **Custom Generic** class – For scenarios where a custom data model is preferred.
3. **BitTimelineOption** component – A specialized component for defining timeline options.

This flexibility allows you to integrate timeline data from various sources and structure your content as needed.

---

## Usage

Below are several examples demonstrating different use cases and configurations of the BitTimeline component.

### 1. Basic (Vertical) Timeline

A simple vertical timeline with three items:

```razor
<BitTimeline>
    <BitTimelineItem>
        <TimelineTitle>Item 1</TimelineTitle>
    </BitTimelineItem>
    <BitTimelineItem>
        <TimelineTitle>Item 2</TimelineTitle>
        <TimelineSubtitle>Item 2 Secondary</TimelineSubtitle>
    </BitTimelineItem>
    <BitTimelineItem>
        <TimelineTitle>Item 3</TimelineTitle>
    </BitTimelineItem>
</BitTimeline>
```

### 2. Horizontal Timeline

Render timeline items horizontally by setting the `Horizontal` parameter to `true`:

```razor
<BitTimeline Horizontal="true">
    <!-- Timeline items go here -->
</BitTimeline>
```

### 3. Disabled Timeline

Disable the entire timeline or specific items to prevent user interaction:

```razor
<BitTimeline>
    <BitTimelineItem IsEnabled="false">
        <TimelineTitle>Item 1</TimelineTitle>
    </BitTimelineItem>
    <!-- Additional items -->
</BitTimeline>
```

### 4. Visual Variants

Choose a visual variant (Fill, Outline, or Text) to change the component's look:

```razor
<BitTimeline Variant="BitVariant.Outline">
    <!-- Timeline items go here -->
</BitTimeline>
```

### 5. Timeline with Icons

Add icons to timeline items by specifying the `IconName` property:

```razor
<BitTimeline>
    <BitTimelineItem IconName="Add">
        <TimelineTitle>Item 1</TimelineTitle>
    </BitTimelineItem>
</BitTimeline>
```

### 6. Reversed Timeline

Reverse the direction of timeline items:

```razor
<BitTimeline Reversed="true">
    <!-- Timeline items go here -->
</BitTimeline>
```

### 7. RTL (Right-to-Left) Timeline

For languages that read right-to-left, apply the RTL attribute and class:

```html
<div class="bit-tln bit-rtl" dir="rtl">
    <!-- Timeline items with RTL content -->
</div>
```

### 8. Custom Styles & Classes

Customize the appearance of the timeline and its items using the `Style` and `Classes` parameters:

```razor
<BitTimeline Style="max-width:600px; color: dodgerblue;" Classes="custom-timeline-class">
    <!-- Timeline items go here -->
</BitTimeline>
```

Individual timeline items can also be customized similarly.

---

## API Reference

### BitTimeline Component Parameters

| Name         | Type                            | Default Value              | Description                                                                |
| ------------ | ------------------------------- | -------------------------- | -------------------------------------------------------------------------- |
| ChildContent | RenderFragment?                 | null                       | The content of the BitTimeline, typically BitTimelineOption components.   |
| Classes      | BitTimelineClassStyles?         | null                       | Custom CSS classes for different parts of the timeline.                  |
| Color        | BitColor?                       | null                       | The general color of the timeline.                                        |
| Horizontal   | bool                            | false                      | Renders timeline items horizontally if set to true.                      |
| Items        | IEnumerable&lt;TItem&gt;        | new List&lt;TItem&gt;()    | List of timeline items representing events or data points.               |
| NameSelectors| BitTimelineNameSelectors&lt;TItem&gt;? | null                | Names and selectors for custom input properties.                         |
| OnItemClick  | EventCallback&lt;TItem&gt;       | –                          | Callback invoked when a timeline item is clicked.                        |
| Options      | RenderFragment?                 | null                       | Alias for ChildContent.                                                   |
| Reversed     | bool                            | false                      | Reverses the direction of all timeline items.                             |
| Size         | BitSize?                        | null                       | The size of the timeline. Possible values: Small, Medium, Large.            |
| Styles       | BitTimelineClassStyles?         | null                       | Custom CSS styles for different parts of the timeline.                    |
| Variant      | BitVariant?                     | null                       | The visual variant of the timeline (Fill, Outline, Text).                 |

### BitComponentBase Parameters

| Name           | Type                             | Default Value                             | Description                                                                  |
| -------------- | -------------------------------- | ----------------------------------------- | ---------------------------------------------------------------------------- |
| AriaLabel      | string?                          | null                                      | Aria-label for screen readers.                                               |
| Class          | string?                          | null                                      | Custom CSS class for the root element.                                     |
| Dir            | BitDir?                          | null                                      | Reading direction (LTR, RTL, or Auto).                                       |
| HtmlAttributes | Dictionary&lt;string, object&gt; | new Dictionary&lt;string, object&gt;()    | Additional HTML attributes.                                                |
| Id             | string?                          | null                                      | Custom id attribute; if null, a unique identifier is generated.            |
| IsEnabled      | bool                             | true                                      | Whether the component is enabled.                                          |
| Style          | string?                          | null                                      | Custom CSS style for the root element.                                     |
| Visibility     | BitVisibility                    | BitVisibility.Visible                     | Controls component visibility.                                             |

### Public Members of BitComponentBase

| Name        | Type             | Default Value    | Description                                          |
| ----------- | ---------------- | ---------------- | ---------------------------------------------------- |
| UniqueId    | Guid             | Guid.NewGuid()   | Unique identifier assigned at component construction. |
| RootElement | ElementReference | –                | Reference to the root HTML element.                |

---

## BitTimelineItem Properties

| Name             | Type                                | Default Value | Description                                            |
| ---------------- | ----------------------------------- | ------------- | ------------------------------------------------------ |
| Class            | string?                             | null          | Custom CSS classes for the item.                       |
| Color            | BitColor?                           | null          | The color of the item.                                 |
| DotTemplate      | RenderFragment&lt;BitTimelineItem&gt;? | null      | Custom template for the item's dot.                    |
| HideDot          | bool                                | false         | Hides the item's dot if set to true.                   |
| IconName         | string?                             | null          | Name of an icon to render in the item.                 |
| IsEnabled        | bool                                | true          | Determines if the item is enabled.                     |
| Key              | string?                             | null          | Unique key for the item.                               |
| OnClick          | EventCallback                       | –             | Click event handler for the item.                      |
| PrimaryContent   | RenderFragment&lt;BitTimelineItem&gt;? | null       | Primary content of the item.                           |
| PrimaryText      | string?                             | null          | Primary text of the item.                              |
| Reversed         | bool                                | false         | Reverses the item's direction if true.               |
| SecondaryContent | RenderFragment&lt;BitTimelineItem&gt;? | null       | Secondary content of the item.                         |
| SecondaryText    | string?                             | null          | Secondary text of the item.                            |
| Size             | BitSize?                            | null          | The size of the item.                                  |
| Style            | string?                             | null          | Custom style for the item.                             |
| Template         | RenderFragment&lt;BitTimelineItem&gt;? | null       | Custom template for the item.                          |

---

## BitTimelineOption Properties

| Name           | Type                                  | Default Value | Description                                            |
| -------------- | ------------------------------------- | ------------- | ------------------------------------------------------ |
| Class          | string?                               | null          | Custom CSS classes for the option.                     |
| Color          | BitColor?                             | null          | The color of the option.                               |
| DotTemplate    | RenderFragment&lt;BitTimelineOption&gt;? | null      | Custom template for the option's dot.                  |
| HideDot        | bool                                  | false         | Hides the option's dot if set to true.                 |
| IconName       | string?                               | null          | Name of an icon to render in the option.              |
| IsEnabled      | bool                                  | true          | Indicates if the option is enabled.                    |
| Key            | string?                               | null          | Unique key for the option.                             |
| OnClick        | EventCallback                         | –             | Click event handler for the option.                    |
| PrimaryContent | RenderFragment&lt;BitTimelineOption&gt;? | null      | Primary content of the option.                         |
| PrimaryText    | string?                               | null          | Primary text of the option.                            |
| Reversed       | bool                                  | false         | Reverses the option's direction if true.               |
| SecondaryContent | RenderFragment&lt;BitTimelineOption&gt;? | null    | Secondary content of the option.                       |
| SecondaryText  | string?                               | null          | Secondary text of the option.                          |
| Size           | BitSize?                              | null          | The size of the option.                                |
| Style          | string?                               | null          | Custom style for the option.                           |
| Template       | RenderFragment&lt;BitTimelineOption&gt;? | null      | Custom template for the option.                        |

---

## BitTimelineNameSelectors Properties

| Name        | Type                                            | Default Value                                 | Description                                              |
| ----------- | ----------------------------------------------- | --------------------------------------------- | -------------------------------------------------------- |
| Class       | BitNameSelectorPair&lt;TItem, string?&gt;         | new(nameof(BitTimelineItem.Class))            | Selector for the item's class property.                |
| DotTemplate | BitNameSelectorPair&lt;TItem, RenderFragment?&gt;  | new(nameof(BitTimelineItem.DotTemplate))        | Selector for the item's dot template.                  |
| HideDot     | BitNameSelectorPair&lt;TItem, bool&gt;            | new(nameof(BitTimelineItem.HideDot))            | Selector for the item's HideDot property.              |
| IconName    | BitNameSelectorPair&lt;TItem, string?&gt;          | new(nameof(BitTimelineItem.IconName))           | Selector for the item's icon name.                     |

---

## BitTimelineClassStyles Properties

| Name             | Type    | Default Value | Description                                                          |
| ---------------- | ------- | ------------- | -------------------------------------------------------------------- |
| Root             | string? | null          | Custom CSS classes/styles for the root element of the timeline.      |
| Item             | string? | null          | Custom CSS classes/styles for each timeline item.                    |
| PrimaryContent   | string? | null          | Custom CSS classes/styles for the primary content of an item.        |
| PrimaryText      | string? | null          | Custom CSS classes/styles for the primary text of an item.           |
| SecondaryContent | string? | null          | Custom CSS classes/styles for the secondary content of an item.       |
| SecondaryText    | string? | null          | Custom CSS classes/styles for the secondary text of an item.          |
| Divider          | string? | null          | Custom CSS classes/styles for the divider between items.             |
| Dot              | string? | null          | Custom CSS classes/styles for the dot of an item.                    |
| Icon             | string? | null          | Custom CSS classes/styles for the icon of an item.                   |

---

## Enumerations

### BitVariant Enum

| Name    | Value | Description                 |
| ------- | ----- | --------------------------- |
| Fill    | 0     | Fill styled variant.        |
| Outline | 1     | Outline styled variant.     |
| Text    | 2     | Text styled variant.        |

### BitColor Enum

| Name          | Value | Description                  |
| ------------- | ----- | ---------------------------- |
| Primary       | 0     | Primary general color.       |
| Secondary     | 1     | Secondary general color.     |
| Tertiary      | 2     | Tertiary general color.      |
| Info          | 3     | Info general color.          |
| Success       | 4     | Success general color.       |
| Warning       | 5     | Warning general color.       |
| SevereWarning | 6     | SevereWarning general color. |
| Error         | 7     | Error general color.         |

### BitSize Enum

| Name   | Value | Description               |
| ------ | ----- | ------------------------- |
| Small  | 0     | The small size timeline.  |
| Medium | 1     | The medium size timeline. |
| Large  | 2     | The large size timeline.  |

### BitVisibility Enum

| Name      | Value | Description                                                      |
| --------- | ----- | ---------------------------------------------------------------- |
| Visible   | 0     | The component is visible.                                        |
| Hidden    | 1     | Hidden but occupies space (visibility: hidden).                  |
| Collapsed | 2     | Hidden and removed from layout (display: none).                  |

### BitDir Enum

| Name | Value | Description                                                                                                             |
| ---- | ----- | ----------------------------------------------------------------------------------------------------------------------- |
| Ltr  | 0     | Left-to-right direction, used for languages written from left to right (e.g., English).                                 |
| Rtl  | 1     | Right-to-left direction, used for languages written from right to left (e.g., Arabic).                                  |
| Auto | 2     | Automatically determines direction based on the content's character directionality.                                   |

---