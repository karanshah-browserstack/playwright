# class: FileChooser
* since: v1.8

[FileChooser] objects are dispatched by the page in the [`event: Page.fileChooser`] event.

```js
// Note that Promise.all prevents a race condition
// between clicking and waiting for the file chooser.
const [fileChooser] = await Promise.all([
  // It is important to call waitForEvent before click to set up waiting.
  page.waitForEvent('filechooser'),
  // Opens the file chooser.
  page.locator('text=Upload').click(),
]);
await fileChooser.setFiles('myfile.pdf');
```

```java
FileChooser fileChooser = page.waitForFileChooser(() -> page.locator("upload").click());
fileChooser.setFiles(Paths.get("myfile.pdf"));
```

```python async
async with page.expect_file_chooser() as fc_info:
    await page.locator("upload").click()
file_chooser = await fc_info.value
await file_chooser.set_files("myfile.pdf")
```

```python sync
with page.expect_file_chooser() as fc_info:
    page.locator("upload").click()
file_chooser = fc_info.value
file_chooser.set_files("myfile.pdf")
```

```csharp
var fileChooser = await page.RunAndWaitForFileChooserAsync(async () =>
{
    await page.Locator("upload").ClickAsync();
});
await fileChooser.SetFilesAsync("temp.txt");
```

## method: FileChooser.element
* since: v1.8
- returns: <[ElementHandle]>

Returns input element associated with this file chooser.

## method: FileChooser.isMultiple
* since: v1.8
- returns: <[boolean]>

Returns whether this file chooser accepts multiple files.

## method: FileChooser.page
* since: v1.8
- returns: <[Page]>

Returns page this file chooser belongs to.

## async method: FileChooser.setFiles
* since: v1.8

Sets the value of the file input this chooser is associated with. If some of the `filePaths` are relative paths, then
they are resolved relative to the current working directory. For empty array, clears the selected files.

### param: FileChooser.setFiles.files = %%-input-files-%%
* since: v1.8

### option: FileChooser.setFiles.noWaitAfter = %%-input-no-wait-after-%%
* since: v1.8

### option: FileChooser.setFiles.timeout = %%-input-timeout-%%
* since: v1.8
