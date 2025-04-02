# BitFileUpload Blazor Component

**Objective:** This document provides context and reference information about the `BitFileUpload` Blazor component, based *solely* on the provided HTML documentation extract. Use this information to understand the component's purpose, features, parameters, and usage.

**Key Component:** `BitFileUpload`

---

## Overview

`BitFileUpload` wraps the standard HTML file input element(s). It facilitates uploading selected files to a specified URL (`UploadUrl`) and supports removing uploaded files via a separate URL (`RemoveUrl`). Key features include:

*   Single or multiple file selection (`Multiple`).
*   Automatic upload immediately after selection (`AutoUpload`).
*   Automatic reset of the component state before browsing (`AutoReset`).
*   Appending newly selected files to the existing list (`Append`).
*   Limiting file size (`MaxSize`).
*   Restricting allowed file types (`AllowedExtensions`).
*   Chunked file uploading (`ChunkedUpload`).
*   Customization of UI elements through templates.

---

## Usage Examples

**1. Basic**

*   **Description**: Default setup for selecting and uploading files.
*   **Code**:
    ```cshtml
    <BitFileUpload Label="Select or drag and drop files" UploadUrl="@UploadUrl" />
    ```
    ```csharp
    @code {
        private string UploadUrl = "/Upload";
    }
    ```

**2. Multiple**

*   **Description**: Allows selecting multiple files by adding the `Multiple` attribute.
*   **Code**:
    ```cshtml
    <BitFileUpload Label="Select or drag and drop files" UploadUrl="@UploadUrl" Multiple />
    ```
    ```csharp
    @code {
        private string UploadUrl = "/Upload";
    }
    ```

**3. AutoUpload**

*   **Description**: Files start uploading automatically after selection when `AutoUpload` is true.
*   **Code**:
    ```cshtml
    <BitFileUpload Label="Select or drag and drop files" UploadUrl="@UploadUrl" AutoUpload />
    ```
    ```csharp
    @code {
        private string UploadUrl = "/Upload";
    }
    ```

**4. AutoReset**

*   **Description**: Clears the component's state (file list) each time the browse dialog is opened when `AutoReset` is true.
*   **Code**:
    ```cshtml
    <BitFileUpload Label="Select or drag and drop files" UploadUrl="@UploadUrl" AutoReset />
    ```
    ```csharp
    @code {
        private string UploadUrl = "/Upload";
    }
    ```

**5. Append**

*   **Description**: Adds newly selected files to the list instead of replacing the current selection when `Append` is true.
*   **Code**:
    ```cshtml
    <BitFileUpload Label="Select or drag and drop files" UploadUrl="@UploadUrl" Append />
    ```
    ```csharp
    @code {
        private string UploadUrl = "/Upload";
    }
    ```

**6. MaxSize**

*   **Description**: Restricts the maximum size (in bytes) for each individual file using the `MaxSize` parameter.
*   **Code**:
    ```cshtml
    <BitFileUpload Label="Select or drag and drop files" UploadUrl="@UploadUrl" MaxSize="1024 * 1024 * 1" /> @* 1 MB Max Size *@
    ```
    ```csharp
    @code {
        private string UploadUrl = "/Upload";
    }
    ```

**7. AllowedExtensions**

*   **Description**: Filters the files that can be selected based on the provided list of extensions in `AllowedExtensions`.
*   **Code**:
    ```cshtml
    <BitFileUpload Label="Select or drag and drop files" UploadUrl="@UploadUrl"
                   AllowedExtensions="@(new List<string> { ".gif",".jpg",".mp4" })" />
    ```
    ```csharp
    @code {
        private string UploadUrl = "/Upload";
    }
    ```

**8. Removable**

*   **Description**: Enables a remove button for uploaded files using `ShowRemoveButton` and specifies the endpoint for removal requests via `RemoveUrl`.
*   **Code**:
    ```cshtml
    <BitFileUpload Label="Select or drag and drop files" UploadUrl="@UploadUrl"
                   ShowRemoveButton RemoveUrl="@RemoveUrl" />
    ```
    ```csharp
    @code {
        private string UploadUrl = "/Upload";
        private string RemoveUrl = "/Remove";
    }
    ```

**9. Events**

*   **Description**: Demonstrates handling events like `OnAllUploadsComplete` (fires when all files finish uploading) and `OnUploading` (fires before an upload starts, allowing modification like adding headers).
*   **Code**:
    ```cshtml
    <BitFileUpload Label="Select or drag and drop files" UploadUrl="@UploadUrl"
                   OnAllUploadsComplete="@(() => onAllUploadsCompleteText = "All File Uploaded")"
                   OnUploading="@(info => info.HttpHeaders = new Dictionary<string, string> { {"key1", "value1"} })" />

    <div>@onAllUploadsCompleteText</div>
    ```
    ```csharp
    @code {
        private string UploadUrl = "/Upload";
        private string onAllUploadsCompleteText = "No File";
    }
    ```

**10. Http requests**

*   **Description**: Shows how to add custom HTTP headers and query strings to both the upload (`UploadRequestHttpHeaders`, `UploadRequestQueryStrings`) and remove (`RemoveRequestHttpHeaders`, `RemoveRequestQueryStrings`) requests.
*   **Code**:
    ```cshtml
    <BitFileUpload Label="Select or drag and drop files" UploadUrl="@UploadUrl" RemoveUrl="@RemoveUrl"
                   UploadRequestQueryStrings="@(new Dictionary<string, string>{ {"qs1", "qsValue1" } })"
                   UploadRequestHttpHeaders="@(new Dictionary<string, string>{ {"header1", "value1" } })"
                   RemoveRequestQueryStrings="@(new Dictionary<string, string>{ {"qs2", "qsValue2" } })"
                   RemoveRequestHttpHeaders="@(new Dictionary<string, string>{ {"header2", "value2" } })" />
    ```
    ```csharp
    @code {
        private string UploadUrl = "/Upload";
        private string RemoveUrl = "/Remove";
    }
    ```

**11. Chunked**

*   **Description**: Enables uploading files in smaller chunks using the `ChunkedUpload` parameter. Useful for large files.
*   **Code**:
    ```cshtml
    <BitFileUpload Label="Select or drag and drop files" UploadUrl="@ChunkedUploadUrl" ChunkedUpload />
    ```
    ```csharp
    @code {
        private string ChunkedUploadUrl = "/ChunkedUpload";
    }
    ```

**12. Templates**

*   **Description**: Demonstrates extensive UI customization using `LabelTemplate` (replaces the browse button/area when no files are selected) and `FileViewTemplate` (defines how each selected/uploading/uploaded file is displayed).
*   **Code**: (Includes CSS and helper methods for context)
    ```css
    /* Styles for custom templates */
    .browse-file { border: 1px solid #D2D2D7; border-radius: 2px; padding: 24px; width: 420px; height: 200px; display: flex; flex-direction: column; justify-content: center; align-items: center; gap: 50px; cursor: pointer; }
    .browse-file-header { display: flex; flex-direction: column; justify-content: center; align-items: center; font-size: 16px; }
    .browse-file-header i { font-size: 24px; font-weight: 700; color: #0072CE; }
    .browse-file-header strong { color: #0072CE; }
    .browse-file-footer { display: flex; flex-direction: column; justify-content: center; align-items: center; font-size: 12px; color: #78787D; }
    .file-list { border: 1px solid #D2D2D7; border-radius: 2px; padding: 24px; width: 420px; height: 200px; display: flex; flex-direction: column; justify-content: space-between; }
    .file-info { display: flex; justify-content: space-between; }
    .file-info-name { overflow: hidden; margin-right: 10px; }
    .file-info-title { color: #5A5A5F; line-height: 22px; display: flex; justify-content: space-between; }
    .file-info-subtitle { color: #909096; }
    .file-info-ico { border: 1px solid #F3F3F8; border-radius: 2px; background-color: #F3F3F8; width: 80px; height: 80px; display: flex; justify-content: center; align-items: center; }
    .file-info-ico i { font-size: 24px; }
    .file-info-data { width: 275px; }
    .file-info-btns { display: flex; justify-content: space-between; gap: 8px; }
    .file-info-btns i { display: block; cursor: pointer; }
    .file-info-btns .upload-ico { color: #0072CE; }
    .file-info-btns .remove-ico { color: #F9423A; }
    .file-info-progressbar-container { width: 100%; overflow: hidden; height: 2px; margin-top: 24px; background-color: #D9D9D9; }
    .file-info-progressbar { height: 2px; transition: width 0.15s linear 0s; background-color: #0072CE; }
    .file-info-s-msg { margin-top: 12px; color: #5EB227; }
    .file-info-e-msg { margin-top: 12px; color: #F9423A; }
    .file-list-footer { font-size: 12px; color: #78787D; }
    ```
    ```cshtml
    <BitFileUpload @ref="bitFileUpload" UploadUrl="@UploadUrl" RemoveUrl="@RemoveUrl">
        <LabelTemplate>
            @if (FileUploadIsEmpty())
            {
                <div class="browse-file">
                    <div class="browse-file-header">
                         <i class="bit-icon bit-icon--CloudUpload" />
                         <div>Drag and drop or</div>
                         <div><strong>Browse file</strong></div>
                    </div>
                    <div class="browse-file-footer">
                         <div>Max file size: 2 MB</div>
                         <div>Supported file types: jpg, jpeg, png, bpm</div>
                    </div>
                </div>
            }
        </LabelTemplate>
        <FileViewTemplate Context="file">
             @if (file.Status != BitFileUploadStatus.Removed)
             {
                <div class="file-list">
                    <div class="file-info">
                         <div class="file-info-ico">
                             <i class="bit-icon bit-icon--FileImage" />
                         </div>
                         <div class="file-info-data">
                             <div class="file-info-title">
                                 <div class="file-info-name">@file.Name</div>
                                 <div class="file-info-btns">
                                     <label for="@bitFileUpload.InputId"><i class="bit-icon bit-icon--CloudUpload upload-ico" /></label>
                                     <i class="bit-icon bit-icon--ChromeClose remove-ico" @onclick="HandleRemoveOnClick" />
                                 </div>
                             </div>
                             @if (file.Status is BitFileUploadStatus.InProgress or BitFileUploadStatus.Pending)
                             {
                                 var fileUploadPercent = GetFileUploadPercent(file);
                                 <div class="file-info-subtitle">@GetFileUploadSize(file) - @fileUploadPercent%</div>
                                 <div class="file-info-progressbar-container">
                                     <div class="file-info-progressbar" role="progressbar" style="width:@fileUploadPercent%;"
                                          aria-valuemin="0" aria-valuemax="100" aria-valuenow="@fileUploadPercent"></div>
                                 </div>
                             }
                             else
                             {
                                 <div class="@(file.Status == BitFileUploadStatus.Completed ? "file-info-s-msg" : "file-info-e-msg")">@GetUploadMessageStr(file)</div>
                             }
                         </div>
                    </div>
                    <div class="file-list-footer">
                         <div>Max file size: 2 MB</div>
                         <div>Supported file types: jpg, jpeg, png, bpm</div>
                    </div>
                </div>
             }
        </FileViewTemplate>
    </BitFileUpload>

    <BitButton OnClick="HandleUploadOnClick">Upload</BitButton>
    ```
    ```csharp
    @code {
        [Inject] public IJSRuntime JSRuntime { get; set; } = default!;
        private string UploadUrl => "/Upload";
        private string RemoveUrl => $"/Remove";
        private BitFileUpload bitFileUpload;

        private bool FileUploadIsEmpty() => !bitFileUpload.Files?.Any(f => f.Status != BitFileUploadStatus.Removed) ?? true;

        private async Task HandleUploadOnClick() {
            if (bitFileUpload.Files is null) return;
            await bitFileUpload.Upload();
        }

        private async Task HandleRemoveOnClick() {
            if (bitFileUpload.Files is null) return;
            await bitFileUpload.RemoveFile(); // Assumes only one file or removes the first removable one by default. Needs context if multiple files are present.
        }

        private static int GetFileUploadPercent(BitFileInfo file) { /* ... calculation ... */ return uploadedPercent; }
        private static string GetFileUploadSize(BitFileInfo file) { /* ... calculation ... */ return $"..."; }
        private string GetUploadMessageStr(BitFileInfo file) => file.Status switch { /* ... status messages ... */ };
        private bool IsFileTypeNotAllowed(BitFileInfo file) { /* ... check logic ... */ }
    }
    ```

**13. Public API**

*   **Description**: Shows how to programmatically trigger the file browse dialog using `@ref` and the `Browse()` method on the component instance.
*   **Code**:
    ```cshtml
    <BitFileUpload @ref="bitFileUploadWithBrowseFile" Label="" UploadUrl="@UploadUrl" RemoveUrl="@RemoveUrl" />
    <BitButton OnClick="HandleBrowseFileOnClick">Browse file</BitButton>
    ```
    ```csharp
    @code {
        private string UploadUrl = "/Upload";
        private string RemoveUrl = "/Remove";
        private BitFileUpload bitFileUploadWithBrowseFile;

        private async Task HandleBrowseFileOnClick()
        {
            await bitFileUploadWithBrowseFile.Browse();
        }
    }
    ```

---

## API Reference

**BitFileUpload Parameters**

| Name                          | Type                                     | Default                            | Description                                                                               |
| :---------------------------- | :--------------------------------------- | :--------------------------------- | :---------------------------------------------------------------------------------------- |
| `Accept`                      | `string?`                                | `null`                             | `accept` attribute for the HTML file input.                                             |
| `AllowedExtensions`           | `IReadOnlyCollection<string>`            | `["*"]`                            | List of allowed file extensions (e.g., ".jpg", ".png"). `"*"` allows all.                |
| `Append`                      | `bool`                                   | `false`                            | Appends newly selected files instead of replacing existing ones.                        |
| `AutoChunkSize`               | `bool`                                   | `false`                            | Dynamically calculates chunk size based on network speed (512KB-10MB).                  |
| `AutoReset`                   | `bool`                                   | `false`                            | Resets the file list before browsing.                                                   |
| `AutoUpload`                  | `bool`                                   | `false`                            | Starts upload immediately after file selection.                                         |
| `ChunkedUpload`               | `bool`                                   | `false`                            | Enables chunked file uploading.                                                         |
| `ChunkSize`                   | `long?`                                  | `null`                             | Size of each chunk in bytes for chunked upload.                                         |
| `FailedRemoveMessage`         | `string`                                 | `File remove failed`             | Message shown when file removal fails.                                                  |
| `FailedUploadMessage`         | `string`                                 | `File upload failed`             | Message shown when file upload fails.                                                   |
| `HideFileView`                | `bool`                                   | `false`                            | Hides the area where selected/uploading files are listed.                               |
| `Label`                       | `string`                                 | `Browse`                           | Text for the file selection button/area.                                                |
| `LabelTemplate`               | `RenderFragment?`                        | `null`                             | Custom template for the file selection button/area.                                     |
| `MaxSize`                     | `long`                                   | `0`                                | Maximum allowed size per file in bytes (0 for unlimited).                               |
| `MaxSizeErrorMessage`         | `string`                                 | `File size exceeds max limit`      | Error message shown when a file exceeds `MaxSize`.                                        |
| `Multiple`                    | `bool`                                   | `false`                            | Allows selecting multiple files.                                                        |
| `NotAllowedExtensionErrorMessage`| `string`                                | `File type not allowed`            | Error message shown when a file's extension is not in `AllowedExtensions`.              |
| `OnAllUploadsComplete`        | `EventCallback<BitFileInfo[]>`           |                                    | Callback invoked when all selected files have finished uploading (successfully or not). |
| `OnChange`                    | `EventCallback<BitFileInfo[]>`           |                                    | Callback invoked whenever the status of any file changes.                               |
| `OnProgress`                  | `EventCallback<BitFileInfo>`             |                                    | Callback invoked periodically during upload, providing progress info for a file.        |
| `OnRemoveComplete`            | `EventCallback<BitFileInfo>`             |                                    | Callback invoked when a file is successfully removed via `RemoveUrl`.                   |
| `OnRemoveFailed`              | `EventCallback<BitFileInfo>`             |                                    | Callback invoked when removing a file via `RemoveUrl` fails.                          |
| `OnUploading`                 | `EventCallback<BitFileInfo>`             |                                    | Callback invoked just before a file upload starts (can modify headers here).            |
| `OnUploadComplete`            | `EventCallback<BitFileInfo>`             |                                    | Callback invoked when a single file upload completes successfully.                      |
| `OnUploadFailed`              | `EventCallback<BitFileInfo>`             |                                    | Callback invoked when a single file upload fails.                                       |
| `RemoveRequestHttpHeaders`    | `IReadOnlyDictionary<string, string>`    | `new Dictionary<>()`               | Custom HTTP headers for the remove request.                                             |
| `RemoveRequestQueryStrings`   | `IReadOnlyDictionary<string, string>`    | `new Dictionary<>()`               | Custom query strings for the remove request.                                            |
| `RemoveUrl`                   | `string?`                                | `null`                             | URL endpoint for removing uploaded files.                                               |
| `ShowRemoveButton`            | `bool`                                   | `false`                            | Shows a remove button for uploaded files (requires `RemoveUrl`).                      |
| `SuccessfulUploadMessage`     | `string`                                 | `File upload successful`           | Message shown when a file upload completes successfully.                              |
| `UploadRequestHttpHeaders`    | `IReadOnlyDictionary<string, string>`    | `new Dictionary<>()`               | Custom HTTP headers for the upload request.                                             |
| `UploadRequestQueryStrings`   | `IReadOnlyDictionary<string, string>`    | `new Dictionary<>()`               | Custom query strings for the upload request.                                            |
| `UploadUrl`                   | `string`                                 | **Required**                       | URL endpoint for uploading files.                                                       |
| `FileViewTemplate`            | `RenderFragment<BitFileInfo>?`          | `null`                             | Custom template for displaying each file in the list.                                   |
| *(Inherited)*                | *(See BitComponentBase)*                 |                                    |                                                                                         |

**BitFileUpload Public Members**

| Name           | Type                                | Description                                                                 |
| :------------- | :---------------------------------- | :-------------------------------------------------------------------------- |
| `Files`        | `IReadOnlyList<BitFileInfo>?`       | A readonly list of the currently selected/uploaded files.                 |
| `UploadStatus` | `BitFileUploadStatus`               | The overall status of the file uploader component.                        |
| `InputId`      | `string?`                           | The generated ID of the hidden HTML file input element.                   |
| `IsRemoving`   | `bool`                              | Indicates if a file removal operation is currently in progress.           |
| `Upload`       | `(BitFileInfo?, string?) => Task`   | Starts uploading either a specific file or all pending files.             |
| `PauseUpload`  | `(BitFileInfo?) => void`            | Pauses the upload for a specific file or all ongoing uploads.           |
| `CancelUpload` | `(BitFileInfo?) => void`            | Cancels the upload for a specific file or all ongoing uploads.            |
| `RemoveFile`   | `(BitFileInfo?) => Task`            | Initiates removal for a specific file or the first removable file.        |
| `Browse`       | `() => Task`                        | Programmatically opens the file selection dialog.                         |
| `Reset`        | `() => Task`                        | Resets the component, clearing the file list and status.                |
| *(Inherited)*  | *(See BitComponentBase)*            |                                                                             |

**BitComponentBase Parameters & Members (Inherited)**

*(Refer to the `BitCheckbox` reference file for details on `AriaLabel`, `Class`, `Dir`, `HtmlAttributes`, `Id`, `IsEnabled`, `Style`, `Visibility`, `UniqueId`, `RootElement`)*

**BitFileInfo Properties**

| Name                  | Type                                  | Default        | Description                                                                          |
| :-------------------- | :------------------------------------ | :------------- | :----------------------------------------------------------------------------------- |
| `ContentType`         | `string`                              | `string.Empty` | MIME type of the file.                                                               |
| `Name`                | `string`                              | `string.Empty` | Name of the file.                                                                    |
| `Size`                | `long`                                |                | Total size of the file in bytes.                                                     |
| `FileId`              | `string`                              | `string.Empty` | Unique GUID assigned to the file instance by the component.                          |
| `Index`               | `int`                                 |                | Index of the file within the selected batch.                                         |
| `LastChunkUploadedSize`| `long`                                |                | Size in bytes of the most recently uploaded chunk (for chunked uploads).           |
| `TotalUploadedSize`   | `long`                                |                | Total bytes uploaded so far for this file.                                           |
| `Message`             | `string?`                             | `null`         | Error message associated with validation or upload failure.                          |
| `Status`              | `BitFileUploadStatus`                 | `Pending`      | Current status of the file (Pending, InProgress, Paused, Canceled, Completed, etc.). |
| `HttpHeaders`         | `IReadOnlyDictionary<string, string>?`| `null`         | HTTP headers associated with the file's upload request (can be set in `OnUploading`). |

**Enums**

*   **BitFileUploadStatus**: Defines the possible states of a file during the upload process (`Pending`, `InProgress`, `Paused`, `Canceled`, `Completed`, `Failed`, `Removed`, `RemoveFailed`, `NotAllowed`).
*   **BitVisibility**: Defines visibility states (`Visible`, `Hidden`, `Collapsed`).
*   **BitDir**: Defines text direction (`Ltr`, `Rtl`, `Auto`).

---

## Feedback

*   Provide feedback via the **GitHub repo**: [File an Issue](https://github.com/bitfoundation/bitplatform/issues/new/choose) or [Start a Discussion](https://github.com/bitfoundation/bitplatform/discussions/new/choose).
*   Review/Edit this demo page: [Review](https://github.com/bitfoundation/bitplatform/blob/develop/src/BlazorUI/Demo/Client/Bit.BlazorUI.Demo.Client.Core/Pages/Components/Inputs/FileUpload/BitFileUploadDemo.razor) / [Edit](https://github.com/bitfoundation/bitplatform/edit/develop/src/BlazorUI/Demo/Client/Bit.BlazorUI.Demo.Client.Core/Pages/Components/Inputs/FileUpload/BitFileUploadDemo.razor)
*   Review/Edit the component source: [Review](https://github.com/bitfoundation/bitplatform/blob/develop/src/BlazorUI/Bit.BlazorUI/Components/Inputs/FileUpload/BitFileUpload.razor) / [Edit](https://github.com/bitfoundation/bitplatform/edit/develop/src/BlazorUI/Bit.BlazorUI/Components/Inputs/FileUpload/BitFileUpload.razor)

