# BitImage Component Reference for AI Agent

**Purpose:** This document provides a detailed reference for the `BitImage` Blazor UI component. It is intended to be used by an AI agent (like GitHub Copilot, Cursor, etc.) to understand the component's functionality, usage patterns, and API, enabling the agent to provide accurate code suggestions and assistance related to `BitImage`.

**Source:** This information is derived from the Bit Blazor UI documentation for the `BitImage` component.

---

## Overview

*   **Component:** `BitImage`
*   **Purpose:** Displays an image (photo, illustration) with various options for fitting, loading, styling, and handling different states (loading, error). It enhances the standard `<img>` tag with Blazor component features.
*   **Library:** Bit Blazor UI (`Bit.BlazorUI`)

---

## Usage Examples

### 1. Basic Usage

The fundamental use requires setting the `Src` (source URL) and `Alt` (alternative text) parameters. `IsEnabled="false"` renders the image in a disabled visual state.

```cshtml
@* Basic enabled image *@
<BitImage Alt="Basic BitImage" Src="images/bit-logo-blue.png" />

<br /><br />
<div>Disabled</div>
@* Disabled image *@
<BitImage Alt="Disabled BitImage" IsEnabled="false" Src="images/bit-logo-blue.png" />
```

### 2. Width & Height

Control the dimensions of the image container using the `Width` and `Height` parameters. These accept standard CSS size units (e.g., `rem`, `px`, `%`).

```cshtml
@* Set only width *@
<BitImage Width="9rem"
          Alt="BitImage with width"
          Style="background-color: #00ffff17" @* Background added for visualization *@
          Src="images/bit-logo-blue.png" />

@* Set only height *@
<BitImage Height="5rem"
          Alt="BitImage with height"
          Style="background-color: #00ffff17"
          Src="images/bit-logo-blue.png" />

@* Set both width and height *@
<BitImage Width="256px"
          Height="128px"
          Alt="BitImage with width and height"
          Style="background-color: #00ffff17"
          Src="images/bit-logo-blue.png" />
```

### 3. ImageFit

The `ImageFit` parameter determines how the image scales and aligns within its container if the image's aspect ratio doesn't match the container's dimensions (when `Width` and/or `Height` are set). It uses the `BitImageFit` enum.

```cshtml
@* ImageFit: None *@
<BitImage Height="96px" Width="200px" @* Added Width for clarity *@
          Alt="ImageFit: None BitImage"
          ImageFit="BitImageFit.None"
          Style="background-color: #00ffff17"
          Src="images/bit-logo-blue.png" />
<br /><br />

@* ImageFit: Center *@
<BitImage Height="96px" Width="200px"
          Alt="ImageFit: Center BitImage"
          ImageFit="BitImageFit.Center"
          Style="background-color: #00ffff17"
          Src="images/bit-logo-blue.png" />
<br /><br />

@* ImageFit: Contain *@
<BitImage Height="96px" Width="200px"
          Alt="ImageFit: Contain BitImage"
          ImageFit="BitImageFit.Contain"
          Style="background-color: #00ffff17"
          Src="images/bit-logo-blue.png" />
<br /><br />

@* ImageFit: Cover *@
<BitImage Height="96px" Width="200px"
          Alt="ImageFit: Cover BitImage"
          ImageFit="BitImageFit.Cover"
          Style="background-color: #00ffff17"
          Src="images/bit-logo-blue.png" />
<br /><br />

@* ImageFit: CenterContain *@
<BitImage Height="96px" Width="200px"
          Alt="ImageFit: CenterContain BitImage"
          ImageFit="BitImageFit.CenterContain"
          Style="background-color: #00ffff17"
          Src="images/bit-logo-blue.png" />
<br /><br />

@* ImageFit: CenterCover *@
<BitImage Height="96px" Width="200px"
          Alt="ImageFit: CenterCover BitImage"
          ImageFit="BitImageFit.CenterCover"
          Style="background-color: #00ffff17"
          Src="images/bit-logo-blue.png" />
```

* **Note:** See the `BitImageFit` enum definition in the API section for details on each value.

### 4. Cover Parameter (`Cover`)

The `Cover` parameter (using `BitImageCover` enum) specifies the *intended* orientation (Landscape or Portrait) of the image frame. This influences how `ImageFit` modes like `CenterCover` or `CenterContain` behave, ensuring the image covers or contains appropriately based on the dominant dimension.

```cshtml
@* CenterCover with Landscape frame hint *@
<BitImage Height="96px" Width="200px" @* Landscape frame *@
          Alt="Landscape BitImage with ImageFit: CenterCover"
          Style="background-color: #00ffff17"
          ImageFit="BitImageFit.CenterCover"
          Cover="BitImageCover.Landscape"
          Src="images/bit-logo-blue.png" />
<br /><br />

@* CenterCover with Portrait frame hint *@
<BitImage Height="144px" Width="96px" @* Portrait frame *@
          Alt="Portrait BitImage with ImageFit: CenterCover"
          Style="background-color: #00ffff17"
          ImageFit="BitImageFit.CenterCover"
          Cover="BitImageCover.Portrait"
          Src="images/bit-logo-blue.png" />
<br /><br />

@* CenterContain with Landscape frame hint *@
<BitImage Height="96px" Width="200px"
          Alt="Landscape BitImage with ImageFit: CenterContain"
          Style="background-color: #00ffff17"
          ImageFit="BitImageFit.CenterContain"
          Cover="BitImageCover.Landscape"
          Src="images/bit-logo-blue.png" />
<br /><br />

@* CenterContain with Portrait frame hint *@
<BitImage Height="144px" Width="96px"
          Alt="Portrait BitImage with ImageFit: CenterContain"
          Style="background-color: #00ffff17"
          ImageFit="BitImageFit.CenterContain"
          Cover="BitImageCover.Portrait"
          Src="images/bit-logo-blue.png" />
```

### 5. Maximize Frame (`MaximizeFrame`)

When `MaximizeFrame="true"`, the image *container* (`div`) expands to fill the available space of its parent container. The image itself still adheres to `ImageFit` rules within that maximized frame.

```cshtml
<div style="width: 300px; height: 150px; border: 1px solid red;"> @* Parent container *@
    <BitImage Alt="Maximized BitImage"
              MaximizeFrame="true"
              ImageFit="BitImageFit.CenterContain" @* Example fit within maximized frame *@
              Style="background-color: #00ffff17"
              Src="images/bit-logo-blue.png" />
</div>
```

### 6. Image State Templates (`LoadingTemplate`, `ErrorTemplate`)

Provide custom content to display while the image is loading or if an error occurs during loading.

```cshtml
@* Loading State Example *@
<BitButton OnClick="() => loadLoading = true">Load loading image</BitButton>
@if (loadLoading)
{
    <BitImage Alt="Loading ImageState" Src="/api/Image/GetImage" Width="200px">
        <LoadingTemplate>
            <div style="width: 200px; height: 100px; display: flex; align-items: center; justify-content: center; border: 1px dashed grey;">
                <b>loading...</b>
                @* Consider adding a BitSpinner here *@
            </div>
        </LoadingTemplate>
    </BitImage>
}

<br /><br />

@* Error State Example *@
<BitButton OnClick="() => loadError = true">Load error image</BitButton>
@if (loadError)
{
    <BitImage Alt="Error ImageState" Src="/api/Image/GetImageError" Width="200px">
        @* Optional Loading Template *@
        <LoadingTemplate>
             <div style="width: 200px; height: 100px; display: flex; align-items: center; justify-content: center; border: 1px dashed grey;">
                 <b>...</b>
             </div>
        </LoadingTemplate>
        <ErrorTemplate>
            <div style="width: 200px; height: 100px; display: flex; align-items: center; justify-content: center; border: 1px dashed red; color: red;">
                <b>error loading image!</b>
            </div>
        </ErrorTemplate>
    </BitImage>
}
```

```csharp
@code {
    private bool loadLoading;
    private bool loadError;

    // NOTE: The API endpoints /api/Image/GetImage and /api/Image/GetImageError
    // are specific to the demo environment used to generate the source HTML.
    // Replace with actual image URLs for real use. Use a deliberately slow
    // endpoint or a non-existent one to test these states.
}
```

* **Related:** The `OnLoadingStateChange` event callback provides the current `BitImageState` (Loading, Loaded, Error).

### 7. Style & Class Customization

Apply custom styles or classes to the image component.

* `Style`/`Class`: Applied to the root container `div`.
* `Styles`/`Classes`: Use `BitImageClassStyles` object to target specific parts: `Root` (container) or `Image` (the `<img>` tag itself).

```cshtml
<style>
    .custom-root-class {
        padding: 0.5rem;
        filter: hue-rotate(45deg);
        background-color: blueviolet;
        display: inline-block; /* Ensure background color applies correctly */
    }

    .custom-image-class {
        width: 16rem; /* Style the image tag directly */
        filter: opacity(25%);
        border-radius: 1rem 3rem;
    }
</style>

@* Using Style on the root container *@
<BitImage Alt="Styled BitImage Root"
          Style="border: 2px solid goldenrod; border-radius: 5px; width: 258px; display: inline-block;"
          Src="images/bit-logo-blue.png" />
<br /><br />

@* Using Class on the root container *@
<BitImage Alt="Classed BitImage Root"
          Class="custom-root-class"
          Src="images/bit-logo-blue.png" />
<br /><br />

@* Using Styles to target the inner image tag *@
<BitImage Alt="Styles BitImage Image Tag"
          Styles="@(new() { Image = "filter: blur(2px); border: 3px solid green;" })"
          Src="images/bit-logo-blue.png" />
<br /><br />

@* Using Classes to target the inner image tag *@
<BitImage Alt="Classes BitImage Image Tag"
          Classes="@(new() { Image = "custom-image-class" })"
          Src="images/bit-logo-blue.png" />
```

---

## API Reference

### `BitImage` Parameters

| Name                 | Type                              | Default Value              | Description                                                                                  |
| :------------------- | :-------------------------------- | :------------------------- | :------------------------------------------------------------------------------------------- |
| `Alt`                | `string?`                         | `null`                     | Specifies an alternate text for the image (accessibility).                                   |
| `Classes`            | `BitImageClassStyles?`            | `null`                     | Custom CSS classes for `Root` container and inner `Image` tag. See class definition below. |
| `Cover`              | `BitImageCover?`                  | `null`                     | Specifies the intended orientation (Landscape/Portrait) to influence fitting. See enum def. |
| `ErrorTemplate`      | `RenderFragment?`                 | `null`                     | Custom content to display if the image fails to load.                                      |
| `FadeIn`             | `bool`                            | `true`                     | If true, the image fades in smoothly when loaded.                                            |
| `Height`             | `string?`                         | `null`                     | Sets the height of the image container (e.g., "100px", "5rem").                              |
| `ImageAttributes`    | `Dictionary<string, object>`      | `new Dictionary<>()`       | Additional HTML attributes to apply directly to the rendered `<img>` tag.                    |
| `ImageFit`           | `BitImageFit?`                    | `null` (defaults to browser behavior)| Determines how the image scales/crops within its frame. See enum definition below.      |
| `Loading`            | `BitImageLoading?`                | `null` (defaults to browser default) | Sets the browser's native image loading behavior (`Lazy` or `Eager`). See enum def. |
| `LoadingTemplate`    | `RenderFragment?`                 | `null`                     | Custom content to display while the image is loading.                                        |
| `MaximizeFrame`      | `bool`                            | `false`                    | If true, the image container expands to fill its parent.                                   |
| `OnClick`            | `EventCallback<MouseEventArgs>`   |                            | Callback function invoked when the image (container) is clicked.                             |
| `OnLoadingStateChange`| `EventCallback<BitImageState>`    |                            | Callback invoked when the image loading state changes (Loading, Loaded, Error). See enum def.|
| `StartVisible`       | `bool`                            | `true`                     | If true, image is visible initially and hides on error. If false, hidden until loaded.       |
| `Src`                | `string?`                         | `null`                     | The URL source of the image. *Required for image to display.*                             |
| `Styles`             | `BitImageClassStyles?`            | `null`                     | Custom inline CSS styles for `Root` container and inner `Image` tag. See class def below. |
| `Title`              | `string?`                         | `null`                     | Text to display as a tooltip when hovering over the image.                                 |
| `Width`              | `string?`                         | `null`                     | Sets the width of the image container (e.g., "100px", "5rem").                               |

### Inherited Parameters (`BitComponentBase`)

| Name             | Type                          | Default Value              | Description                                                                                    |
| :--------------- | :---------------------------- | :------------------------- | :--------------------------------------------------------------------------------------------- |
| `AriaLabel`      | `string?`                     | `null`                     | The aria-label for the image container (usually `Alt` on the `<img>` is preferred).           |
| `Class`          | `string?`                     | `null`                     | Custom CSS class(es) applied to the root container `div`.                                    |
| `Dir`            | `BitDir?`                     | `null`                     | Sets the text direction (relevant if text is overlaid or in templates). See `BitDir` enum.     |
| `HtmlAttributes` | `Dictionary<string, object>`  | `new Dictionary<>()`       | Additional HTML attributes applied to the root container `div`.                              |
| `Id`             | `string?`                     | `null`                     | Custom `id` attribute for the root container `div`. If `null`, `UniqueId` is used.           |
| `IsEnabled`      | `bool`                        | `true`                     | Renders the image in a disabled visual state.                                                |
| `Style`          | `string?`                     | `null`                     | Custom inline CSS style(s) applied to the root container `div`.                              |
| `Visibility`     | `BitVisibility`               | `BitVisibility.Visible`    | Controls the visibility of the root container `div`. See `BitVisibility` enum.               |

### Public Members (`BitComponentBase`)

| Name          | Type               | Default Value    | Description                                                                           |
| :------------ | :----------------- | :--------------- | :------------------------------------------------------------------------------------ |
| `UniqueId`    | `string`           | `Guid.NewGuid()` | Readonly unique identifier generated for the component instance. Used if `Id` is null. |
| `RootElement` | `ElementReference` |                  | A reference to the rendered root container `div` element (available after rendering). |

### Supporting Classes and Enums

#### `BitImageClassStyles` Class

Used for `Classes` and `Styles` parameters to target specific parts.

| Property | Type      | Description                                                      |
| :------- | :-------- | :--------------------------------------------------------------- |
| `Root`   | `string?` | CSS class(es) or style(s) for the root container `div` element.  |
| `Image`  | `string?` | CSS class(es) or style(s) for the inner `<img>` element itself. |

#### `BitImageFit` Enum

Determines how the image fits within its frame (`ImageFit` parameter).

| Name           | Value | Description                                                                 |
| :------------- | :---- | :-------------------------------------------------------------------------- |
| `None`         | `0`   | Image is not scaled. Rendered at its natural size.                          |
| `Center`       | `1`   | Image is not scaled but centered within the frame. May be cropped.          |
| `CenterContain`| `2`   | Scales to fit while maintaining aspect ratio, centered within the frame.    |
| `CenterCover`  | `3`   | Scales to fill frame while maintaining aspect ratio, centered. May be cropped.|
| `Contain`      | `4`   | Scales to fit while maintaining aspect ratio. (Alignment may vary).         |
| `Cover`        | `5`   | Scales to fill frame while maintaining aspect ratio. (Alignment may vary). May be cropped. |

#### `BitImageCover` Enum

Hints at the frame's orientation to influence fitting (`Cover` parameter).

| Name        | Value | Description                                                              |
| :---------- | :---- | :----------------------------------------------------------------------- |
| `Landscape` | `0`   | Frame is wider than tall. Height might be prioritized for scaling.       |
| `Portrait`  | `1`   | Frame is taller than wide. Width might be prioritized for scaling.       |

#### `BitImageState` Enum

Represents the loading status of the image (`OnLoadingStateChange` event).

| Name      | Value | Description                         |
| :-------- | :---- | :---------------------------------- |
| `Loading` | `0`   | Image is currently loading.         |
| `Loaded`  | `1`   | Image loaded successfully.          |
| `Error`   | `2`   | Error occurred during image loading. |

#### `BitImageLoading` Enum

Controls browser's native lazy/eager loading (`Loading` parameter).

| Name    | Value | Description                                                       |
| :------ | :---- | :---------------------------------------------------------------- |
| `Eager` | `0`   | Load image immediately (browser default).                         |
| `Lazy`  | `1`   | Defer loading until the image is likely to enter the viewport.    |

#### `BitVisibility` Enum

Used for the inherited `Visibility` parameter.

| Name        | Value | Description                                                        |
| :---------- | :---- | :----------------------------------------------------------------- |
| `Visible`   | `0`   | Element is visible (default).                                      |
| `Hidden`    | `1`   | Element is hidden (`visibility: hidden;`), still occupies space.   |
| `Collapsed` | `2`   | Element is hidden (`display: none;`), does not occupy space.       |

#### `BitDir` Enum

Used for the inherited `Dir` parameter.

| Name   | Value | Description                                     |
| :----- | :---- | :---------------------------------------------- |
| `Ltr`  | `0`   | Left-to-right text direction.                   |
| `Rtl`  | `1`   | Right-to-left text direction.                   |
| `Auto` | `2`   | Browser determines direction based on content. |

---