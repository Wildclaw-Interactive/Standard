# Third-Party Notices

Standard's proprietary `LICENSE.txt` applies only to Standard-owned software. Third-party libraries remain governed by their own licenses.

Standard is distributed by Wildclaw Interactive. Release packaging must preserve all notices required by the exact versions actually shipped.

## AvalonEdit 6.3.1.120

Standard Studio uses AvalonEdit as its source editor.

Upstream project: https://github.com/icsharpcode/AvalonEdit

AvalonEdit is distributed under the MIT License.

Copyright notices remain the property of the AvalonEdit / SharpDevelop contributors.

MIT License:

> Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the "Software"), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:
>
> The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.
>
> THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.

## Avalonia 12.1.3

Standard UI uses Avalonia as its current cross-platform rendering backend.

Upstream project: https://github.com/AvaloniaUI/Avalonia

Avalonia is distributed under the MIT License. Its official upstream license and NOTICE material must be retained as required when Avalonia binaries are redistributed.

MIT License:

> Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the "Software"), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:
>
> The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.
>
> THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.

## Avalonia.Controls.WebView 12.1.0

Used by the Standard UI Browser/WebView control. The upstream project is distributed under the MIT License. Include its upstream copyright/license notice when its binaries are included in a release or generated application.

## Microsoft .NET

Standard currently targets .NET 8 and uses the .NET SDK as its bootstrap build tool. Self-contained published Standard binaries and generated applications may include Microsoft/.NET runtime components with their own license and third-party notices.

When producing a public binary package, preserve the Microsoft/.NET license and third-party notices required by the exact runtime files included by `dotnet publish`.

## Release checklist

Before uploading a release artifact:

1. inspect the exact published binary folder;
2. identify all shipped third-party assemblies/components;
3. include the matching upstream notices/licenses;
4. do not replace third-party terms with Standard's proprietary license; and
5. keep `LICENSE.txt`, `REDISTRIBUTABLES.txt`, and this file together with the release.
