# BitSwiper Component Reference (Blazor UI / TouchSlider)

## 1. Overview

**`BitSwiper`** (also referred to as TouchSlider) is a Blazor component designed to display a collection of items (slides) in a horizontally scrollable row format. It's optimized for touch interactions (swiping) but also provides optional navigation buttons. It's ideal for showcasing items like product cards, images, or teasers where horizontal space is limited.

**Key Purpose:** To present a series of content items in a compact, horizontally swipeable/scrollable container.

## 2. Key Features

*   **Horizontal Scrolling/Swiping:** Allows users to navigate through items using touch gestures (swipe left/right) or mouse dragging.
*   **Item Definition:** Uses nested `BitSwiperItem` components to define the content of each slide/item.
*   **Navigation Buttons:** Provides optional built-in previous/next buttons for navigation (`HideNextPrev` parameter).
*   **Configurable Scrolling:** Allows controlling how many items are scrolled per navigation action (`ScrollItemsCount`).
*   **Customization:** Supports standard Blazor component customization via `Class`, `Style`, `Id`, `HtmlAttributes`, and allows hiding navigation buttons.
*   **Animation Control:** The duration of the scroll animation can be configured (`AnimationDuration`).
*   **RTL Support:** Built-in support for Right-to-Left layouts using the `Dir` parameter.

## 3. Core Usage (Basic Example)

The basic structure involves a `BitSwiper` parent containing multiple `BitSwiperItem` children. Each `BitSwiperItem` typically needs a defined width for proper layout.

**Components:**
*   `BitSwiper`: The main container enabling swipe/scroll behavior.
*   `BitSwiperItem`: Represents a single item within the swiper row.

**Example (`.razor`):**

```cshtml
<style>
    /* Styling for individual items within the swiper */
    .basic-swiper-item {
        width: 250px; /* Crucial: Define the width of each item */
        height: 150px; /* Example height */
        position: relative; /* For absolute positioning inside */
        overflow: hidden; /* Ensure content fits */
        border: 1px solid #ccc; /* Example border */
        box-sizing: border-box; /* Include border in width/height */
        flex-shrink: 0; /* Prevent items from shrinking */
    }

    .basic-swiper-item .number {
        position: absolute;
        top: 0.5rem;
        left: 0.5rem;
        padding: 0.25rem 0.5rem;
        font-size: 0.75rem;
        color: white;
        background-color: rgba(0, 0, 0, 0.6);
        border-radius: 3px;
        white-space: nowrap;
    }

    .basic-swiper-item .image {
        width: 100%;
        height: 100%;
        object-fit: cover; /* Make image cover the item area */
        display: block;
    }
</style>

<BitSwiper AriaLabel="Basic Image Swiper">
    @for (int i = 1; i <= 8; i++) // Example with 8 items
    {
        var index = i;
        var imageIndex = (index - 1) % 4 + 1; // Cycle through 4 images
        <BitSwiperItem Class="basic-swiper-item">
            <div class="number">Item @index</div>
            <img class="image" src="/images/carousel/img@(imageIndex).jpg" alt="Image @index" />
        </BitSwiperItem>
    }
</BitSwiper>
```

**Explanation:**

1. **`<BitSwiper>`:** The main component. It handles the swipe detection and horizontal layout. `AriaLabel` added for accessibility.
2. **`@for` Loop:** A common way to generate multiple `BitSwiperItem` components dynamically.
3. **`<BitSwiperItem>`:** Each child defines one item in the horizontal row.
4. **Styling (`.basic-swiper-item`):**
    * `width`: **Essential.** Each item *must* have a defined width for the swiper layout to work correctly.
    * `height`: Defines the item height.
    * `flex-shrink: 0`: Prevents items from shrinking if the container is too small (though the container should ideally handle overflow).
    * Other styles define the appearance of the content within the item.
5. **Navigation:** By default, `BitSwiper` displays previous/next buttons when applicable (i.e., when there are more items than fit in the view). Touch swiping is always enabled.

---

## 4. Key Features & Configuration

### 4.1 Controlling Scroll Amount

Define how many items move when the user clicks the next/prev buttons. Note that touch swiping is usually continuous.

**Parameter:** `ScrollItemsCount` (int, default: `1`)

```cshtml
<style>
    .scroll-item { width: 180px; height: 100px; border: 1px solid green; line-height: 100px; text-align: center; background-color: lightgreen; flex-shrink: 0; margin: 5px; }
</style>

@* Clicking next/prev moves 2 items at a time *@
<BitSwiper ScrollItemsCount="2">
    @for (int i = 1; i <= 10; i++)
    {
        <BitSwiperItem Class="scroll-item">Item @i</BitSwiperItem>
    }
</BitSwiper>

```

### 4.2 Hiding Navigation Buttons

Remove the default previous and next buttons, relying solely on touch/mouse swiping.

**Parameter:** `HideNextPrev` (boolean, default: `false`)

```cshtml
<style>
    .no-buttons-item { width: 200px; height: 120px; border: 1px solid purple; line-height: 120px; text-align: center; background-color: lavender; flex-shrink: 0; margin: 5px; }
</style>

<BitSwiper HideNextPrev>
     @for (int i = 1; i <= 10; i++)
    {
        <BitSwiperItem Class="no-buttons-item">Item @i</BitSwiperItem>
    }
</BitSwiper>
```

### 4.3 Right-to-Left (RTL) Support

Adapts the layout and navigation direction for RTL languages.

**Parameter:** `Dir="BitDir.Rtl"`

```cshtml
<style>
    .rtl-item { width: 220px; height: 140px; border: 1px solid orange; line-height: 140px; text-align: center; background-color: peachpuff; flex-shrink: 0; margin: 5px; }
</style>

<BitSwiper Dir="BitDir.Rtl">
    @for (int i = 1; i <= 10; i++)
    {
        <BitSwiperItem Class="rtl-item">مورد @i</BitSwiperItem> @* RTL Content *@
    }
</BitSwiper>
```

**Explanation:** Sets the direction to RTL. Navigation buttons (if shown) and swipe directionality will be reversed compared to LTR.

### 4.4 Animation Duration

Control the speed of the scrolling animation when using the navigation buttons.

**Parameter:** `AnimationDuration` (double, default: `0.5`) - Value is in seconds.

```cshtml
<style>
    .anim-item { width: 150px; height: 150px; border: 1px solid teal; line-height: 150px; text-align: center; background-color: lightcyan; flex-shrink: 0; margin: 5px; }
</style>

@* Slower animation (1.5 seconds) *@
<BitSwiper AnimationDuration="1.5">
     @for (int i = 1; i <= 10; i++)
    {
        <BitSwiperItem Class="anim-item">Item @i</BitSwiperItem>
    }
</BitSwiper>
```

---

## 5. Styling

* **Item Width:** This is the most critical style. Each `BitSwiperItem` needs a defined `width` (using CSS `class` or `style`) for the swiper to calculate layout and scrolling correctly.
* **Container Styling:** Apply `Class` or `Style` to the `BitSwiper` component to control its overall appearance (e.g., height, background, padding).
* **Item Styling:** Apply `Class` or `Style` to `BitSwiperItem` or elements within it to style individual items. Remember `flex-shrink: 0` is often useful on items.

```cshtml
<style>
    .custom-swiper {
        height: 180px;
        border: 3px dotted red;
        padding: 10px;
        background-color: #f0f0f0;
    }
    .custom-swiper-item {
        width: 300px; /* Explicit width */
        height: 100%;
        background: linear-gradient(45deg, #ff9a9e, #fad0c4);
        color: white;
        display: flex;
        align-items: center;
        justify-content: center;
        font-size: 1.5rem;
        border-radius: 8px;
        margin: 0 5px; /* Add some spacing between items */
        flex-shrink: 0;
        box-shadow: 2px 2px 5px rgba(0,0,0,0.2);
    }
</style>

<BitSwiper Class="custom-swiper">
     @for (int i = 1; i <= 8; i++)
    {
        <BitSwiperItem Class="custom-swiper-item">Slide @i</BitSwiperItem>
    }
</BitSwiper>
```

---

## 6. API Reference

### `BitSwiper` Parameters

| Name                | Type                | Default Value | Description                                                                                                 |
| :------------------ | :------------------ | :------------ | :---------------------------------------------------------------------------------------------------------- |
| `ChildContent`      | `RenderFragment?`   | `null`        | The content of the swiper, typically consisting of `BitSwiperItem` components.                              |
| `ScrollItemsCount`  | `int`               | `1`           | Number of items scrolled when using the next/prev navigation buttons. Touch swiping is typically continuous. |
| `HideNextPrev`      | `bool`              | `false`       | Hides the default next and previous navigation buttons. Swiping remains enabled.                            |
| `AnimationDuration` | `double`            | `0.5`         | Duration (in seconds) of the scroll animation when using navigation buttons.                                |
| **Inherited**       |                     |               | *Includes `AriaLabel`, `Class`, `Dir`, `HtmlAttributes`, `Id`, `IsEnabled`, `Style`, `Visibility` from `BitComponentBase`.* |

**Note:** Unlike `BitCarousel`, the provided API documentation *does not list public methods* like `GoNext`, `GoPrev`, or `GoTo` for programmatic control of `BitSwiper`. Navigation is primarily handled via touch/mouse drag and the optional built-in buttons.

### `BitSwiperItem` Parameters

`BitSwiperItem` acts as a container for each item/slide in the swiper.

| Name            | Type              | Default Value | Description                                                             |
| :-------------- | :---------------- | :------------ | :---------------------------------------------------------------------- |
| `ChildContent`  | `RenderFragment?` | `null`        | The HTML or Blazor components that constitute the content of the item. |
| **Inherited**   |                   |               | *Includes `Class`, `Style`, `Id`, `Visibility`, etc. from `BitComponentBase`.* |

### Inherited `BitComponentBase` Parameters

*(Same as provided in previous component references)*

| Name             | Type                         | Default Value           | Description                                                               |
| :--------------- | :--------------------------- | :---------------------- | :------------------------------------------------------------------------ |
| `AriaLabel`      | `string?`                    | `null`                  | Aria-label for accessibility.                                             |
| `Class`          | `string?`                    | `null`                  | Custom CSS class for the root element.                                    |
| `Dir`            | `BitDir?`                    | `null`                  | Component direction (Ltr, Rtl, Auto).                                     |
| `HtmlAttributes` | `Dictionary<string, object>` | `new Dictionary<...>()` | Additional HTML attributes to render.                                     |
| `Id`             | `string?`                    | `null`                  | Custom id for the root element.                                           |
| `IsEnabled`      | `bool`                       | `true`                  | Whether the component is enabled.                                         |
| `Style`          | `string?`                    | `null`                  | Custom inline CSS style for the root element.                             |
| `Visibility`     | `BitVisibility`              | `BitVisibility.Visible` | Component visibility (Visible, Hidden, Collapsed).                        |

### Inherited `BitComponentBase` Public Members

*(Same as provided in previous component references)*

| Name          | Type                | Default Value    | Description                                      |
| :------------ | :------------------ | :--------------- | :----------------------------------------------- |
| `UniqueId`    | `Guid`              | `Guid.NewGuid()` | **Readonly**. Unique identifier for the instance. |
| `RootElement` | `ElementReference`  | *(N/A)*          | Reference to the component's root HTML element.  |

### Enums

**`BitVisibility`** *(Same as previous references)*
**`BitDir`** *(Same as previous references)*

---

## 7. Best Practices & Considerations

* **Item Width is Key:** Always define a consistent CSS `width` for your `BitSwiperItem` components. This is essential for the horizontal layout and scrolling calculations. Use `box-sizing: border-box;` to avoid sizing issues with borders/padding.
* **Touch-First:** While buttons are available, the primary interaction model is touch swiping or mouse dragging. Ensure your item content doesn't interfere with these drag gestures.
* **Performance:** For a very large number of complex items, consider if a different pattern (like virtualization with `BitBasicList` if vertical scrolling is acceptable) might be more performant. However, `BitSwiper` is generally efficient for typical use cases.
* **Container Height:** Define a `height` on the `BitSwiper` or its items to ensure consistent visual presentation.
* **Accessibility:** Provide a descriptive `AriaLabel` on the `BitSwiper`. Ensure content within items is accessible (e.g., `alt` text for images). Button navigation (if not hidden) aids keyboard users.
* **Styling:** Use `margin` on `BitSwiperItem`s to create visual spacing between elements if desired. Remember `flex-shrink: 0;` on items prevents them from resizing undesirably.

---

## 8. Further Information (Source Links)

* **Component Source Code:** [BitSwiper.razor on GitHub](https://github.com/bitfoundation/bitplatform/blob/develop/src/BlazorUI/Bit.BlazorUI/Components/Lists/Swiper/BitSwiper.razor)
* **Demo Page Source Code:** [BitSwiperDemo.razor on GitHub](https://github.com/bitfoundation/bitplatform/blob/develop/src/BlazorUI/Demo/Client/Bit.BlazorUI.Demo.Client.Core/Pages/Components/Lists/Swiper/BitSwiperDemo.razor)
* **Project Issues:** [File an Issue on GitHub](https://github.com/bitfoundation/bitplatform/issues/new/choose)
* **Project Discussions:** [Start a Discussion on GitHub](https://github.com/bitfoundation/bitplatform/discussions/new/choose)

