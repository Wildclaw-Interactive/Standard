# Standard UI

> **Applies to:** Standard `0.1.2-alpha`

Standard UI is Standard's own UI description language and visual-designer model. Avalonia is the current rendering backend; Avalonia types are not part of Standard's public syntax.

```text
.standardui
   ↓
lexer
   ↓
AST
   ↓
semantic binder
   ↓
Standard UI model
   ↓
Avalonia backend
```

## Interface

```standard
Interface MainWindow:
    Title "My App"
    Size 900 by 600
    Background "#17191F"

    Text heading:
        Text "Hello"
        Position 24 by 24
        Size 300 by 40
        Font size 26
    End
End
```

`End` closes both control declarations and the Interface.

## Controls

The current Standard UI control set includes:

```text
Text
Button
Input
Password input
Text area
Check box
Radio button
Switch
Panel
Card
Dropdown
List
Number input
Slider
Progress
Date picker
Time picker
Browser
Separator
```

## Common properties

Most controls support:

```standard
Position 40 by 80
Size 220 by 40
Background "#20242B"
Foreground "#F0F3F7"
Enabled true
Visible true
```

Text-capable controls can use:

```standard
Text "Continue"
Font size 14
```

Inputs can use:

```standard
Placeholder "Type here"
Read only true
```

## Dropdown and List

```standard
Dropdown difficulty:
    Position 24 by 80
    Size 220 by 40
    Placeholder "Choose difficulty"
    Items "Easy" and "Normal" and "Hard"
    Selected "Normal"
    On changed DifficultyChanged
End
```

Commas also work in `Items`:

```standard
Items "Easy", "Normal", "Hard"
```

Runtime Standard code:

```standard
choice = selected item of control difficulty
index = selected index of control difficulty
options = items of control difficulty
count = number of items in control difficulty

Set selected item of control difficulty to "Hard"
Set selected index of control difficulty to 0
Set items of control difficulty to ["Easy", "Normal", "Hard"]
Add "Nightmare" to control difficulty
Remove "Easy" from control difficulty
Clear items of control difficulty
```

## Number input / Slider / Progress

```standard
Number input lives:
    Minimum 1
    Maximum 99
    Value 3
    Step 1
    On changed LivesChanged
End
```

The same numeric bridge is shared with Slider and Progress:

```standard
value = value of control lives
Set value of control lives to 10
```

## Check box / Radio button / Switch

```standard
Radio button light_theme:
    Text "Light"
    Group "theme"
    Checked true
    On changed ThemeChanged
End

Radio button dark_theme:
    Text "Dark"
    Group "theme"
    On changed ThemeChanged
End

Switch notifications:
    Text "Notifications"
    Checked true
    On changed NotificationsChanged
End
```

Read/write checked state from Standard:

```standard
enabled = control notifications is checked
Set control notifications checked to false
```

## Date and Time pickers

```standard
Date picker start_date:
    Selected "2026-10-06"
    On changed DateChanged
End

Time picker start_time:
    Selected "19:30"
    On changed TimeChanged
End
```

They use the same selected-item bridge:

```standard
date = selected item of control start_date
time = selected item of control start_time
Set selected item of control start_date to "2026-12-31"
```

## Browser

```standard
Browser web:
    Position 300 by 80
    Size 560 by 420
    Address "https://example.com"
    On navigated BrowserLoaded
End
```

Runtime operations:

```standard
Navigate browser web to "https://avaloniaui.net"
Refresh browser web
Stop browser web
Go back in browser web
Go forward in browser web
address = address of browser web
```

The backend uses Avalonia's `NativeWebView`. The Standard syntax does not expose Avalonia APIs.

## Events

UI events call parameterless Standard functions:

```standard
Function DifficultyChanged:
    choice = selected item of control difficulty
    Print choice to console
End
```

Supported UI event properties include:

```text
On click
On changed
On navigated
```

The binder validates whether an event/property makes sense for the selected control.

## Designer

The Standard Studio designer supports the controls above in the palette, Layers selection, drag/drop positioning, context-aware properties, Design/UI Code switching, and parser validation.

The designer and code view share the same Standard UI model:

```text
Visual designer ↔ Standard UI model ↔ serializer / parser / AST
```

The Browser is shown as a lightweight placeholder in the WPF bootstrap designer; the built application uses Avalonia's real web view.

## Current limits

- Root layout is still absolute-positioned.
- Panel/Card do not own nested child controls yet.
- No Row/Column/Grid responsive layout yet.
- No reusable UI Components yet.
- Standard Studio itself is still WPF; generated Standard UI apps use Avalonia.
- Standard code now has a lexer/parser/AST and semantic-analysis frontend; code generation still uses the C#/.NET bootstrap backend.

## Starting an interface

A Standard UI is normally opened from project startup code:

```standard
Show interface "MainWindow.standardui"
```

Standard Studio and project composition provide a safety net for simple projects: when an `Auto` or `Desktop` project contains exactly one `.standardui` file and no startup interface is specified, Standard automatically starts that one interface. If a project contains multiple interfaces, use `Show interface` explicitly so startup is never ambiguous.


## Comments

`.standardui` files support the same comments as Standard source:

```standard
Note: one-line UI note

Note:
    Multi-line designer documentation.
    Everything in this block is ignored.
End
```
