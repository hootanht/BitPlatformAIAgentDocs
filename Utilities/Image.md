# Image Component Documentation

This document serves as a comprehensive reference for the **Image** component. The Image component displays a graphic—such as a photo or illustration—and supports extensive customization including dimension control, scaling modes, loading states, and custom styles. Background colors in the examples help to visualize empty space within the image frame.

---

## Overview

The **Image** component is used to render graphical content in your application. It allows you to:
- Display images with alternative text for accessibility.
- Control dimensions (width and height) and aspect ratio.
- Specify how the image fits into its frame (scaling and cropping).
- Handle different loading states (loading, loaded, error) with custom templates.
- Customize the appearance through inline styles or CSS classes.

---

## Usage

### Basic Usage

Render a basic image and a disabled version. In this example, two `BitImage` components are shown—one active and one disabled.

```cshtml
<BitImage Alt="Basic BitImage" Src="images/bit-logo-blue.png" />

<BitImage Alt="Disabled BitImage" IsEnabled="false" Src="images/bit-logo-blue.png" />
```

Below the code samples, the rendered output shows the active image and the disabled image (using a faded style).

---

### Width & Height

You can specify the dimensions of the image either by setting its width, its height, or both. Background colors in these examples help to visualize the image frame.

```cshtml
<!-- Image with a fixed width -->
<BitImage Width="9rem" Alt="BitImage with width" Style="background-color: #00ffff17" Src="images/bit-logo-blue.png" />

<!-- Image with a fixed height -->
<BitImage Height="5rem" Alt="BitImage with height" Style="background-color: #00ffff17" Src="images/bit-logo-blue.png" />

<!-- Image with both width and height set -->
<BitImage Width="256px" Height="128px" Alt="BitImage with width and height" Style="background-color: #00ffff17" Src="images/bit-logo-blue.png" />
```

---

### ImageFit

The `ImageFit` property determines how the image is scaled and cropped to fit its frame. The following examples show different fit options:

```cshtml
<!-- No scaling: the image and frame remain unchanged -->
<BitImage Height="96" Alt="ImageFit: None BitImage" ImageFit="BitImageFit.None" Style="background-color: #00ffff17" Src="images/bit-logo-blue.png" />

<!-- Center: the image is centered and cropped within the frame -->
<BitImage Height="96" Alt="ImageFit: Center BitImage" ImageFit="BitImageFit.Center" Style="background-color: #00ffff17" Src="images/bit-logo-blue.png" />

<!-- Contain: the image scales to be fully visible while preserving aspect ratio -->
<BitImage Height="96" Alt="ImageFit: Contain BitImage" ImageFit="BitImageFit.Contain" Style="background-color: #00ffff17" Src="images/bit-logo-blue.png" />

<!-- Cover: the image scales to fill the frame while preserving aspect ratio -->
<BitImage Height="96" Alt="ImageFit: Cover BitImage" ImageFit="BitImageFit.Cover" Style="background-color: #00ffff17" Src="images/bit-logo-blue.png" />

<!-- CenterContain: the image is centered, scales to be fully contained, and preserves aspect ratio -->
<BitImage Height="96" Alt="ImageFit: CenterContain BitImage" ImageFit="BitImageFit.CenterContain" Style="background-color: #00ffff17" Src="images/bit-logo-blue.png" />

<!-- CenterCover: the image is centered, scales to cover the frame, and preserves aspect ratio -->
<BitImage Height="96" Alt="ImageFit: CenterCover BitImage" ImageFit="BitImageFit.CenterCover" Style="background-color: #00ffff17" Src="images/bit-logo-blue.png" />
```

---

### Cover

The `Cover` property works with `ImageFit` to handle different image orientations. This example shows how the component behaves for both landscape and portrait images when using the CenterCover fit.

```cshtml
<!-- CenterCover with Landscape cover style -->
<BitImage Height="96" Alt="Landscape BitImage with ImageFit: CenterCover" 
          ImageFit="BitImageFit.CenterCover" Cover="BitImageCover.Landscape" Src="images/bit-logo-blue.png" />

<!-- CenterCover with Portrait cover style -->
<BitImage Height="144" Width="96" Alt="Portrait BitImage with ImageFit: CenterCover" 
          ImageFit="BitImageFit.CenterCover" Cover="BitImageCover.Portrait" Src="images/bit-logo-blue.png" />
```

---

### MaximizeFrame

Set the `MaximizeFrame` property to allow the image frame to expand and fill its parent container.

```cshtml
<BitImage Alt="Maximized BitImage" MaximizeFrame="true" Src="images/bit-logo-blue.png" />
```

---

### ImageState

Manage the image loading state by showing different templates when the image is loading or encounters an error. The following example demonstrates using custom templates for these states.

```cshtml
<BitButton OnClick="@( () => loadLoading = true )">Load image</BitButton>
@if (loadLoading)
{
    <BitImage Alt="Loading ImageState" Src="/api/Image/GetImage" Width="200px">
        <LoadingTemplate>
            <b>loading...</b>
        </LoadingTemplate>
    </BitImage>
}

<BitButton OnClick="@( () => loadError = true )">Load image</BitButton>
@if (loadError)
{
    <BitImage Alt="Error ImageState" Src="/api/Image/GetImageError" Width="200px">
        <LoadingTemplate>
            <b>...</b>
        </LoadingTemplate>
        <ErrorTemplate>
            <b>error!!!</b>
        </ErrorTemplate>
    </BitImage>
}

@code {
    // Example code to handle image state
    bool loadLoading;
    bool loadError;
    // Additional logic as needed...
}
```

---

### Style & Class

Customize the Image component by applying custom styles and CSS classes. You can use inline styles or bind external CSS classes to alter the look of the image or its container.

```cshtml
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

<!-- Using inline style -->
<BitImage Alt="Styled BitImage" Style="border: 2px solid goldenrod; border-radius: 5px; width: 258px;" Src="images/bit-logo-blue.png" />

<!-- Using a custom CSS class -->
<BitImage Alt="Styled BitImage" Class="custom-class" Src="images/bit-logo-blue.png" />

<!-- Using custom styles via bound properties -->
<BitImage Alt="Styled BitImage" Styles="@(new BitImageClassStyles { Image = "filter: blur(5px)" })" Src="images/bit-logo-blue.png" />

<!-- Using custom classes via bound properties -->
<BitImage Alt="Styled BitImage" Classes="@(new BitImageClassStyles { Image = "custom-image" })" Src="images/bit-logo-blue.png" />
```

---

## API

### BitImage Parameters

| **Name**           | **Type**                         | **Default Value**                          | **Description**                                                                                  |
| ------------------ | -------------------------------- | ------------------------------------------ | ------------------------------------------------------------------------------------------------ |
| Alt                | `string?`                        | `null`                                     | Specifies an alternate text for the image.                                                     |
| Classes            | `BitImageClassStyles?`           | `null`                                     | Custom CSS classes for different parts of the BitImage.                                          |
| Cover              | `BitImageCover?`                 | `null`                                     | Specifies the cover style to be used for this image.                                             |
| ErrorTemplate      | `RenderFragment?`                | `null`                                     | Custom template used to display the error state of the image.                                    |
| FadeIn             | `bool`                           | `true`                                     | If true, fades the image in when it is loaded.                                                   |
| Height             | `string?`                        | `null`                                     | Specifies the image height value.                                                              |
| ImageAttributes    | `Dictionary<string, object>`     | `new Dictionary<string, object>()`         | Additional attributes for the image element.                                                   |
| ImageFit           | `BitImageFit?`                   | `null`                                     | Determines how the image is scaled and cropped within its frame.                                 |
| Loading            | `BitImageLoading?`               | `null`                                     | Specifies the image loading behavior (lazy or eager).                                            |
| LoadingTemplate    | `RenderFragment?`                | `null`                                     | Custom template for the image loading state.                                                   |
| MaximizeFrame      | `bool`                           | `false`                                    | If true, the image frame expands to fill its parent container.                                   |
| OnClick            | `EventCallback<MouseEventArgs>`  | `null`                                     | Callback for when the image is clicked.                                                        |
| OnLoadingStateChange | `EventCallback<BitImageState>` | `null`                                     | Callback method for when the image load state changes.                                           |
| StartVisible       | `bool`                           | `true`                                     | If true, the image starts visible and is hidden on error; otherwise, it is hidden until loaded.    |
| Src                | `string?`                        | `null`                                     | Specifies the source URL of the image.                                                         |
| Styles             | `BitImageClassStyles?`           | `null`                                     | Custom CSS styles for different parts of the BitImage.                                           |
| Title              | `string?`                        | `null`                                     | The title shown on mouse hover over the image.                                                 |
| Width              | `string?`                        | `null`                                     | Specifies the image width value.                                                               |

### BitComponentBase Parameters

| **Name**         | **Type**                         | **Default Value**                         | **Description**                                                                             |
| ---------------- | -------------------------------- | ----------------------------------------- | ------------------------------------------------------------------------------------------- |
| AriaLabel        | `string?`                        | `null`                                    | The aria-label for screen readers.                                                          |
| Class            | `string?`                        | `null`                                    | Custom CSS class for the root element of the component.                                     |
| Dir              | `BitDir?`                        | `null`                                    | Determines the component direction (e.g., Ltr, Rtl, Auto).                                   |
| HtmlAttributes   | `Dictionary<string, object>`     | `new Dictionary<string, object>()`         | Additional attributes for the root element.                                                 |
| Id               | `string?`                        | `null`                                    | Custom id for the root element. If null, a unique id will be generated.                       |
| IsEnabled        | `bool`                           | `true`                                    | Indicates whether the component is enabled.                                                 |
| Style            | `string?`                        | `null`                                    | Custom CSS style for the root element of the component.                                     |
| Visibility       | `BitVisibility`                  | `BitVisibility.Visible`                   | Controls the visibility of the component (visible, hidden, or collapsed).                     |

### BitComponentBase Public Members

| **Name**    | **Type**            | **Default Value**       | **Description**                                                                              |
| ----------- | ------------------- | ----------------------- | -------------------------------------------------------------------------------------------- |
| UniqueId    | `Guid`              | `Guid.NewGuid()`        | A read-only unique identifier assigned when the component instance is constructed.          |
| RootElement | `ElementReference`  | *(none)*                | A reference to the root HTML element of the component.                                      |

### BitImageClassStyles Properties

| **Name** | **Type**  | **Default Value** | **Description**                                               |
| -------- | --------- | ----------------- | ------------------------------------------------------------- |
| Root     | `string?` | `null`            | Custom CSS classes/styles for the root element of the image.  |
| Image    | `string?` | `null`            | Custom CSS classes/styles for the image element itself.       |

---

## Enumerations

### BitImageFit Enum

| **Name**         | **Value** | **Description**                                                      |
| ---------------- | --------- | -------------------------------------------------------------------- |
| None             | `0`       | Neither the image nor the frame are scaled.                          |
| Center           | `1`       | The image is centered within the frame without scaling.              |
| CenterContain    | `2`       | The image is centered and fully contained while maintaining its aspect ratio. |
| CenterCover      | `3`       | The image is centered and scaled to cover the frame while preserving aspect ratio. |

### BitImageCover Enum

| **Name**    | **Value** | **Description**                                                                                 |
| ----------- | --------- | ----------------------------------------------------------------------------------------------- |
| Landscape   | `0`       | The image is shown at 100% height of the container and the width scales accordingly.            |
| Portrait    | `1`       | The image is shown at 100% width of the container and the height scales accordingly.            |

### BitImageState Enum

| **Name** | **Value** | **Description**                                         |
| -------- | --------- | ------------------------------------------------------- |
| Loading  | `0`       | The image is currently loading from its source.       |
| Loaded   | `1`       | The image has been loaded successfully.               |
| Error    | `2`       | An error occurred while loading the image.            |

### BitImageLoading Enum

| **Name** | **Value** | **Description**                                                                                   |
| -------- | --------- | ------------------------------------------------------------------------------------------------- |
| Eager    | `0`       | The image loads immediately when the element is processed (default behavior).                    |
| Lazy     | `1`       | The image loads only when it is likely to be needed, reducing initial load time.                 |

### BitVisibility Enum

| **Name**    | **Value** | **Description**                                                      |
| ----------- | --------- | -------------------------------------------------------------------- |
| Visible     | `0`       | The component is visible.                                            |
| Hidden      | `1`       | The component is hidden but still occupies space (via `visibility:hidden`). |
| Collapsed   | `2`       | The component is hidden and does not occupy any space (`display:none`).  |

### BitDir Enum

| **Name** | **Value** | **Description**                                                                                   |
| -------- | --------- | ------------------------------------------------------------------------------------------------- |
| Ltr      | `0`       | Left-to-right direction (e.g., for English).                                                      |
| Rtl      | `1`       | Right-to-left direction (e.g., for Arabic).                                                       |
| Auto     | `2`       | Automatically determines direction based on content.                                             |

---

## Feedback

Your feedback is essential for improving the Image component. You can contribute or report issues using the following channels:

- **GitHub Repository:**  
  [View Repository](https://github.com/bitfoundation/bitplatform)

- **File a New Issue:**  
  [Open Issue](https://github.com/bitfoundation/bitplatform/issues/new/choose)

- **Start a Discussion:**  
  [New Discussion](https://github.com/bitfoundation/bitplatform/discussions/new/choose)

- **Review/Edit Image Demo:**  
  [Review Image Demo](https://github.com/bitfoundation/bitplatform/blob/develop/src/BlazorUI/Demo/Client/Bit.BlazorUI.Demo.Client.Core/Pages/Components/Utilities/Image/BitImageDemo.razor)  
  [Edit Image Demo](https://github.com/bitfoundation/bitplatform/edit/develop/src/BlazorUI/Demo/Client/Bit.BlazorUI.Demo.Client.Core/Pages/Components/Utilities/Image/BitImageDemo.razor)

- **Review/Edit Image Component:**  
  [Review Image Component](https://github.com/bitfoundation/bitplatform/blob/develop/src/BlazorUI/Bit.BlazorUI/Components/Utilities/Image/BitImage.razor)  
  [Edit Image Component](https://github.com/bitfoundation/bitplatform/edit/develop/src/BlazorUI/Bit.BlazorUI/Components/Utilities/Image/BitImage.razor)

---

## Explanation for AI Agent Usage

This Markdown file is intended as a detailed reference for the **Image** component. An AI agent using this document should be able to:

- **Understand Component Purpose:**  
  Recognize that the Image component renders a graphic with customizable dimensions, fit modes, and loading states.

- **Generate Code Examples:**  
  Use the provided examples to produce similar code snippets that demonstrate how to set dimensions, handle image fitting (such as Center, Contain, Cover, etc.), and manage state transitions (loading, loaded, error).

- **Extract API Metadata:**  
  Parse the API tables to retrieve property names, types, default values, and descriptions for both the BitImage and the underlying BitComponentBase, as well as custom style configurations via BitImageClassStyles.

- **Interpret Enumerations:**  
  Utilize the enum definitions (e.g., BitImageFit, BitImageCover, BitImageState, BitImageLoading, BitVisibility, and BitDir) to determine the behavior and presentation of images.

- **Apply Styling & Classes:**  
  Understand how inline styles, custom CSS classes, and bound style properties can be used to alter the appearance of the image component.

- **Provide Feedback Links:**  
  Direct users to the GitHub pages for reviewing, reporting issues, or contributing improvements.

This reference ensures that both human developers and automated systems have all the necessary details to effectively implement, customize, and troubleshoot the Image component within the Bit BlazorUI framework.

---

*End of Image Component Documentation.*