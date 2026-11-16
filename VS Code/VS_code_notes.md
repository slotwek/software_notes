---
date: 2026-11-16
aliases:
relates_to:
---
# Extensions
[[VS Code - plugins]]

# Command palette
- Execute commands in VS Code - press: `Ctrl + Shift + P` and type your command!
	- Restore default editor font size: `Reset Editor Font Size`
- To zoom in/out the whole application press: `Ctrl + +` or `Ctrl + -`
	- To reset press: `Ctrl + Num 0`
		- I have modified it to `Ctrl + 0` as used in other applications - e.g. Firefox or Chrome
- Switch off the "Minimap" (file preview) search for `View: Toggle Minimap`

# Navigating Palette: `Ctrl + P`
- [Video demonstration](https://youtu.be/lWEKiak0WVU?si=__mIRH66Z1-X4ZzE&t=1838)
- You can quickly open a file by typing the file name
- Jump to line number: `:100` - which will allow you to jump to line 100
- `@name_of_paragraph` - jumps to paragraph, e.g. to Python decorator

# Shortcuts:
- Hide/Show side panel: `Ctrl + B`
- You can modify behaviour of the app by changing: Settings / Keyboard 
	- Changed: `View Reset Zoom` from: `Ctrl + NumPad0` to `Ctrl + 0` 

# Profiles:
*You can create different profiles for different languages you're using. So, they will have the settings you may want to use for that particular language.*
![[VS_Code_-_Profiles.png]]

## AI stuff
_To start with AI press `Ctrl+I`_
In the field write what you want to achieve. In my case:
`How to read csv file with Python pandas` and it generated the code bellow:

> ## Read a CSV file with pandas
>
> ```python
> import pandas as pd
>
> df = pd.read_csv("file.csv")
> print(df.head())
> ```

---
[[VS Code - main]]