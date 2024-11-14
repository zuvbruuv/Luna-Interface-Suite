# Introduction
This Documentation Is Last Updated for Prerelease Beta 2.1
## Why Choose Luna?
  Reliable And Stable
  Beautful Design
  Open Sourced
  Amazing Features like key system, custom configs, prebuilt tabs and more!
  Smooth And Excellent Performance

Now Let's Get Started, Shall We?

**Also hope shlex will add this docs.sirius.menu but its fine here lol**


# Documentation For Luna
## Booting The Library
```lua
local Luna = loadstring(game:HttpGet("https://raw.githubusercontent.com/Nebula-Softworks/Luna-Interface-Suite/refs/heads/main/source.lua", true))()
```
> This loads up the library to use our Elements. No parameters required

> [!NOTE]
> Luna Gives The User The Option To Load, Save And Autoload Their Own Configurations So manually loading them isnt required

## Windows
#### Creating The Window
Sadly, Unlike Older Projects, Luna Can't Have Multiple Windows. But It's Fine! Right?
```lua
local Window = Luna:CreateWindow({
		Name = "Luna Example Window", -- This Is Title Of Your Window
		LogoID = "82795327169782", -- The Asset ID of your logo. Set to nil if you do not have a logo for Luna to use.
		LoadingEnabled = true, -- Whether to enable the loading animation. Set to false if you do not want the loading screen or have your own custom one.
		LoadingTitle = "Luna Interface Suite", -- Header for loading screen
		LoadingSubtitle = "by Nebula Softworks", -- Subtitle for loading screen

		ConfigSettings = {
			RootFolder = nil, -- If you have multiple games for ur hub, set this to ur hub name so there will be different config 
			-- folders for each game script. otherwsie, this is unnessecary
			ConfigFolder = "Example Script"
		},

		KeySystem = false, -- This is still WIP and Luna Will Not use this in the current build. 
		KeySettings = {
			Title = "Luna Example Key",
			Subtitle = "Key System",
			Note = "Best Key System Ever! Also, Please Use A HWID Keysystem like Pelican, Luarmor etc. that provide key strings based on your HWID since putting a simple string is very easy to bypass",
			FileName = "Key", -- the name of the key file. this will be saved in ur RootFolder. However, if you don't have one, it'll save in ur config folder instead
			SaveKey = true, -- The user's key will be saved, but if you change the key, they will be unable to use your script
			KeyLink = "", -- put the site where users will get your key here
			Key = {"Example Key"} -- List of keys that will be accepted by the system, please use a system like Pelican or Luarmor that provide key strings based on your HWID since putting a simple string is very easy to bypass
		}
})
```

#### Luna Icons
Luna Uses Custom Icons so u do not have to find ans upload your own!
We have 2 sources ; [Lucide](https://lucide.dev) and Material (Docs For Material Is Coming Soon)
Simply grab the name of your icon and paste it into the icon parameter. Make sure to change ImageSource to the source you're using.

#### Creating A Tab
This will show u how to create the instance of a tab. I reccomend storing them in a table but it is fine for the docs.
```lua
local Tab = Window:CreateTab({
			Name = "Tab Example",
			Icon = "view_in_ar",
			ImageSource = "Material",
			ShowTitle = true -- This will determine whether the big header text in the tab will show
})
```

#### Creating A Section
Sections Help Organize Your Script. Ability to add Elements To Sections is coming soon
```lua
Tab:CreateSection("Section Example")
```
##### Section Methods
> This requires the section to be a variable first!
```
Section:Set("New Section Name")
Section:Destroy() -- Destroys the section
```

#### Destroying The Interface
Destroys the UI And Elements
> [!WARNING]
> Destroying Luna Does Not Toggle Off Your Scripts So When Destroying, make sure you disable them first
```
Luna:Destroy()
```

## Interactions

### Adding Interactive Elements
#### Notifying The User (Notifications)
```lua
Luna:Notification({ 
		Title = "Luna Notification Example",
		Icon = "notifications_active",
		ImageSource = "Material",
		Content = "This Is A Preview Of Luna's Dynamic Notification System Entailing Estimated/Calculated Wait Times, A Sleek Design, Icons, And A Glassmorphic Look"
})
```

> [!TIP]
> While You Can Do Element.Callback = function() ... end when creating the element, I Reccomend using :Set() to set the callback after creating Your UI
> It is better to seperate Interface and functionallity however it is your opinion
> All Elements Except Color Picker And Slider Have Description Options, however overusing them can make your UI look weird.

#### Creating A Button
```lua
local Button = Tab:CreateButton({
		Name = "Button Example!",
		Description = nil -- Creates A Description For Users to know what the button does (looks bad if you use it all the time),
    Callback = function()
         -- The function that takes place when the button is pressed
    end
})
```

#### Creating A Toggle
```lua
local Toggle = Tab:CreateToggle({
		Name = "Toggle Example",
		Description = nil,
		CurrentValue = false,
		Flag = "Toggle", -- A flag is the identifier for the configuration file, make sure every element has a different flag if you're using configuration saving to ensure no overlaps
    Callback = function(Value)
       -- The function that takes place when the toggle is switched
       -- The variable (Value) is a boolean on whether the toggle is true or false
    end
})
```

#### Creating A Color Picker
> [!CAUTION]
> The Color Picker Is Not Currently in the version "Prerelease Beta 2.1"

#### Creating A Slider
```lua
local Slider = Tab:CreateSlider({
		Name = "Slider Example",
		Range = {0, 200}, -- The Minimum And Maximum Values Respectively
		Increment = 5, -- Basically The Changing Value/Rounding Off
		CurrentValue = 100, -- The Starting Value
		Flag = "Slider", -- A flag is the identifier for the configuration file, make sure every element has a different flag if you're using configuration saving to ensure no overlaps
    Callback = function(Value)
       -- The function that takes place when the slider changes
       -- The variable (Value) is a number which correlates to the value the slider is currently at
    end
})
```

#### Creating A Dynamic Input (Adaptive Input AKA Textbox)
> [!WARNING]
> For Some Reason Set Doesnt work on CurrentValue/Text ; the event doesnt fire. 
> We Are Looking In This Problem And We Will Fix It As Soon As Possible
```lua
local Input = Tab:CreateInput({
		Name = "Dynamic Input Example",
		Description = nil,
		PlaceholderText = "Input Placeholder",
		CurrentValue = "", -- the current text
		Numeric = false, -- When true, the user may only type numbers in the box (Example walkspeed)
		MaxCharacters = nil, -- if a number, the textbox length cannot exceed the number
		Enter = false, -- When true, the callback will only be executed when the user presses enter.
    Callback = function(Text)
       -- The function that takes place when the input is changed
       -- The variable (Text) is a string for the value in the text box
    end
})
```

#### Creating A Dropdown Menu
> Currently, The Only Special Type is Player.
> If SpecialType equals Player, then the dropdown options will be the list of players
```lua
local Dropdown = Tab:CreateDropdown({
		Name = "Dropdown Example",
    Description = nil,
    Options = {"Option 1","Option 2"},
    CurrentOption = {"Option 1"},
    MultipleOptions = false,
    SpecialType = nil,
    Flag = "Dropdown", -- A flag is the identifier for the configuration file, make sure every element has a different flag if you're using configuration saving to ensure no overlaps
    Callback = function(Options)
     -- The function that takes place when the selected option is changed
     -- If MultipleOptions is true then The variable (Options) is a table of strings for the current selected options. Else, it is a string of the currentoption
    end
})
```

#### Updating And Element Plus Universal Features
> [!IMPORTANT]
> For Any Of These To Work, The Element Needs to be defined as a variable

To Access An Element's Values, you can simply do:
```lua
ElementName.Settings
```
To Update An Element's Values Or Settings you can use :Set
> [!TIP]
> For Dropdowns, if you want to add an option instead of refreshing, you can do `local table = Dropdown.Settings.Options; table.insert(table, "New option name"); Dropdown:Set({ Options = table })`
```lua
ElementName:Set(
  put your new settings table here. unspecified elements will use the previous values.
)
```

To Destroy An Element, You Can Use :Destroy
```lua
ElementName:Destroy()
```

### Binding Keys
> [!NOTE]
> While using :CreateKeybind() is fine, it is superseded by :CreateBind() and shouldn't be used for future work as it won't receive updates.

#### Creating A Keybind
```lua
local Bind = TabCreateBind({
		Name = "Bind Example",
		Description = nil,
		CurrentKeybind = "Q", -- Check Roblox Studio Docs For KeyCode Names
		HoldToInteract = false, -- When true, Instead of toggling, You hold to achieve the active state of the Bind
    Flag = "Bind",
    Callback = function(BindState)
     -- The function that takes place when the keybind is pressed
     -- The variable (BindState) is a boolean for whether the Bind is being held or not (HoldToInteract needs to be true) OR it is whether the Bind is active
    end
})
```
#### Updating Binded Keys
Updating Binded Keys Is The Same As Updating Other Elements
To Access An Element's Values, you can simply do:
```lua
ElementName.Settings
```
To Update An Element's Values Or Settings you can use :Set
```lua
ElementName:Set(
  put your new settings table here. unspecified elements will use the previous values.
)
```

To Destroy An Element, You Can Use :Destroy
```lua
ElementName:Destroy()
```

## UI Components

### Textual Elements

> [!NOTE]
> Luna Paragraphs Automatically Size To Your text!

#### Creating A Label
```lua
local Label = Tab:CreateLabel({
		Text = "Label Example",
		Style = 1 -- Luna Labels Have 3 Styles : A Basic Label, A Green Information Label and A Red Warning Label. Look At The Following Image For More Details
})
```
> [!TIP]
> Here Are The Styles For Labels
> ![Label Styles](https://github.com/user-attachments/assets/9cfc01c7-3017-43a6-a732-6249ffb51993)

#### Creating A Paragraph
```lua
local Paragraph = Tab:CreateParagraph({
		Title = "Paragraph Example ",
		Text = "This Is A Paragraph. You Can Type Very Long Strings Here And They'll Automatically Fit! This Counts As A Description Right? Right? Right? Right? Right? Right? Right? Right? Right? Right? Right? Right? Right? Right? Right? Also Did I Mention This Has Rich Text? Also Did I Mention This Has Rich Text? Also Did I Mention This Has Rich Text? Also Did I Mention This Has Rich Text? Also Did I Mention This Has Rich Text? Also Did I Mention This Has Rich Text?"
})
```

#### Updating Textual Elements
They are the same as regular elements.
To Access An Element's Values, you can simply do:
```lua
ElementName.Settings
```
To Update An Element's Values Or Settings you can use :Set
```lua
ElementName:Set(
  put your new settings table here. unspecified elements will use the previous values.
)
```

To Destroy An Element, You Can Use :Destroy
```lua
ElementName:Destroy()
```

## Extras
### Credits

Main Developers:
`hunter` - Lead/Main Developer, UI Designing, Some Programming, Documentation, and Logo
`JustHey` - Co Developer, Major Bug Fixing, Configuration Handling
Wally - Dragging And Certain Other Mechanics
Inori - Configurations
`shlexr and iRay` -  Rayfield (PCall Parsing, Notifications, Slider)

Helpers/Side Developers:
`Throit` - Color Picker
`Tarmac and qweery` - Icon Modules
kirill9655 - Loading Circle and Certain Images
Sirius Discord Members - Feedback, Suggestions And Testers

> [!NOTE]
> If Your Name Is in a `box like this`, it means you contributed a lot.

### Script Template/Example
COMING SOON
