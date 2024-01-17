---
draft: true
date: 2024-01-08
categories:
  - technology
  - microsoft
  - windows
  - ui
authors:
  - z4pf1sh
---

# I - Relics & Consistency - The Unhinged Rant About Windows

Born on November 10, 1983, Windows, at the time still based on MS-DOS, finally introduces the graphical user interface (GUI) to people using IBM PC (or its clones).

Follow the path of history, as we shed some light onto one of the greatest weaknesses in terms of user experience of Windows - historical relics and inconsistency.

<!-- more -->

!!! info "This series was written on a Mac"

    Just like the Windows 95 boot sound[^1].

It’s been 40 years since Windows was first introduced, and even longer for MS-DOS, which was introduced 2 years prior to Windows. Over almost half a century, Windows has evolved through many iterations. Its kernel, for example, has evolved from MS-DOS, to MS-DOS-based, to NT. Till now, the latest version of Windows is Windows 11. There is certainly no denying that every single modern operating system, including Windows, is a feat of engineering. But shiny as it is, Windows is a piece of software that is way too big. And history relics have found their way to today, some hiding in the corners, some visible everyday, most remain untouched for years. This creates a feel of inconsistency, making Windows messy and segmented, sharply visible in user interface.

## Simpler times

Microsoft has a very terrible track record of maintaining stuff. From Silverlight to Zune, from Metro apps to UWP, some of which are confirmed *D-E-A-D* dead, while some are de-facto dead. This has always been a problem troubling Microsoft, despite it being still pretty manageable in the XP era. Back then, for native application development, Microsoft offered developers a simple option: [:fontawesome-brands-wikipedia-w: Win32 MFC](https://en.wikipedia.org/wiki/Microsoft_Foundation_Class_Library) with C or C++. While developing Windows XP, Microsoft was also working on something called “.NET Framework”, formerly “Next Generation Windows Services” - a revolutionary framework that was set to make native application development way easier, safer, more efficient and reliable than ever before.

.NET Framework was a great idea, with C#, one the bundled languages, it introduced a [:fontawesome-brands-wikipedia-w: generational garbage collection](https://en.wikipedia.org/wiki/Tracing_garbage_collection#Generational_GC_(ephemeral_GC)) automatic memory management mechanism to developers familiar with C and C++ syntaxes, freeing them from the hassle of error-prone manual memory management. It’s like driving manual vs. automatic transmission cars. Sure, if you are skilled enough, manual could be better than automatic for 85% of the time, but for everyone else automatic is (way) better than manual for 99% of the time. Even better, as a brand new language with a brand new framework, Microsoft took their time to painstakingly wrap traditional C++ Win32 APIs into their brand new form in .NET Framework. Gone are the ugly `typedef`s like `LPCTWSTR` or obsolete ones like `DWORD`, say hello to the new, unified keywords like `string` and `int`. There is no need to listen for [:fontawesome-brands-wikipedia-w: Windows Messages](https://en.wikipedia.org/wiki/Message_loop_in_Microsoft_Windows), just use events and their respective handlers. You don’t even need to write a main loop, the framework also does that for you, and events are automatically delivered to your application, rather than you having to actively retrieve it first. Things are looking great so far. Everything looks promising, and when it was released in February 13, 2002, developers are quickly adopting to this new piece of technology, in hope to improve their workflow and make future development easier and faster.

The initial framework in .NET Framework for graphical user interfaces is Windows Forms. In a nutshell, it is a wrapper of Win32 APIs used to create native applications with native Windows controls and widgets. So things made with Windows Forms will look and behave just the same as if they’ve been written with Win32 APIs. Who doesn’t like it when you have more than one technical choices to achieve the same thing? As time went on, .NET Framework gained popularity among developers for its ease of use and overall better experience than C++ Win32 development. It seemed like Microsoft finally made a worthy, modern candidate to challenge the almighty Win32’s reign.

## Enter WPF

But unfortunately, at this point, Microsoft was already a very bureaucratic corporation. Somewhere in a small office in Redmond, WA[^2], someone suggested that Windows Forms is just not *revolutionary* enough. Think about it, it was just a wrapper for the existing Win32 APIs that it was set to replace in the first place. How could you replace something when you still depend on it?

The team came up with something codenamed “Avalon”, and planned to make some aggressive and radical technological advancements under the hood. First, UI composition will be accelerated by GPU with DirectX. Then, inspired by the web, the UI is now defined by XAML, instead of drag-and-drop in IDE[^3] or bunches of repetitive `new()` and `Controls.Add()` calls. Proper high-DPI display support became a reality, and dynamic data binding is now the recommended standard approach. Its name is later revealed as “Windows Presentation Foundation”, or WPF for short. WPF was officially released in November 21, 2006, 4 years after Windows Forms. In a technological sense, WPF is a huge leap over Windows Forms. It is no longer just a wrapper for Win32 APIs, but a brand new framework with brand new architecture.

However, as WPF no longer depends on the Win32 API set used by Windows Forms to composite UI, it needs to implement its own composition mechanism. Like any other WPF component, the rendering engine is built from the ground-up, requiring WPF itself to render controls mimicking the style and behavior of native Windows controls, as if they’ve been drawn with Win32 APIs. Despite all the hard work put into it, to users, it is still a simulation, and still gives out an odd feeling that something’s off. This is strike one in user interface inconsistency. On the bright side, though, WPF did a fantastic job of recreating the original Windows feel. In addition to the XP-style “Luna” theme, WPF also added Aero (Windows Vista and 7) and Metro (Windows 8 and 8.1) theme later, and will automatically try to use the best match for current version of Windows. In fact, if you feel nostalgic, you can even instruct WPF to render in Luna theme on Windows 11.

??? note "List of built-in themes of WPF"

    WPF has become open-source since late 2018, which made it easier for us to peek at its inside.
    A complete list of built-in themes of WPF could be found easily at its [:fontawesome-brands-github: GitHub repository](https://github.com/dotnet/wpf/tree/main/src/Microsoft.DotNet.Wpf/src/Themes).

    As of writing, there are 8 built-in themes available:

    | Assembly                         | XAML                        | Theme                                         |
    | :------------------------------- | :-------------------------- | :-------------------------------------------- |
    | `PresentationFramework.Classic`  | `Classic.xaml`              | Windows Classic theme                         |
    | `PresentationFramework.Luna`     | `Luna.NormalColor.xaml`     | Classic blue Luna theme                       |
    | `PresentationFramework.Luna`     | `Luna.Metallic.xaml`        | Silver Luna theme                             |
    | `PresentationFramework.Luna`     | `Luna.HomeStead.xaml`       | Olive Luna theme                              |
    | `PresentationFramework.Royale`   | `Royale.NormalColor.xaml`   | Luna theme on Windows XP Media Center Edition |
    | `PresentationFramework.Aero`     | `Aero.NormalColor.xaml`     | Aero theme on Windows Vista & 7               |
    | `PresentationFramework.Aero2`    | `Aero2.NormalColor.xaml`    | Aero theme on Windows 8 & 8.1                 |
    | `PresentationFramework.AeroLite` | `AeroLite.NormalColor.xaml` | Aero theme on Windows 10                      |

    You can also see the [archived MSDN blog :octicons-link-external-16:](https://learn.microsoft.com/en-us/archive/blogs/wpfsdk/using-themes-with-custom-controls) (now on Microsoft Learn) for reference.

??? example "Applying styles to your own application"

    To use one of the built-in styles, Olive Luna, for example, make sure your `App.xaml` looked like this:

    ```xml
    <Application ...>
        <Application.Resources>
            <ResourceDictionary>
                <ResourceDictionary.MergedDictionaries>
                    <ResourceDictionary Source="/PresentationFramework.Luna,Version=0.0.0.0,PublicKeyToken=31bf3856ad364e35;component/Themes/Luna.HomeStead.xaml" />
                </ResourceDictionary.MergedDictionaries>
            </ResourceDictionary>
        </Application.Resources>
    </Application>
    ```

    If you do not wish to apply it globally, you can apply it to specific windows as well. Just move the innermost part
    to the `<Window.Resources>` part and et voilà!

## iPad and Metro

The iPad, released in April 2010, was set to fill the gap between smartphones and computers. It’s categorized as a “tablet computer”, and was a hit, which posed a significant threat to Microsoft and apparently caught them off guard. As part of Microsoft’s “strengthen the monopoly by making Windows run everywhere” plan, Microsoft decided that they better enter the tablet computer market as well. Coincidentally, as the other company in the *Wintel* alliance, Intel was also looking for a way to fight against the rise of smartphones and tablet computers. Neither of the two companies wanted the “lifestyle company in Cupertino”[^4] to eat away their precious market share. So once again, the two giants sat down together to discuss about the future of Windows and PCs.

### Microsoft’s view

On Microsoft’s side, to make Windows run (well) on tablet computers, would obviously require a touch-first, or at least touch-friendly user interface, along with other major overhauls under the hood to make Windows “mobile” enough to compete with the iPad and others. But Microsoft seemed confident.

> Windows PCs will continue to adapt and evolve, and Windows will be everywhere on every kind of device without compromise.
>
> \- Steve Ballmer, Microsoft CEO[^5]

Good one, Steve. As part of their plan, the next generation of Windows would feature:

- A new, touch-friendly UI
- An app ecosystem like the App Store
- Full UEFI boot support
- The ability to run on ARM-based systems
- Quick wake, sleep, boot up and shut down speed

... and everything else to make Windows competitive enough against iPads running iOS.

Microsoft also proposed something called “[:fontawesome-brands-wikipedia-w: Connected Standby](https://en.wikipedia.org/wiki/InstantGo)”, a feature allowing Windows devices to stay always connected to Wi-Fi networks to continuously receive messages and updates like tablet computers running iOS and Android, and have comparable responsiveness of them when going to sleep and waking up. It was a good concept, but was implemented so horribly that it will later be proven more as a trouble rather than convenience in the years to come[^6].

### Intel’s view

Meanwhile, on Intel’s side, some of the features proposed by Microsoft must be implemented by Intel to become a reality. And Intel also needs to figure out their stuff to enable x86 systems to fit in the form of a tablet computer. Here are some major differences between desktop and laptop PCs and tablet computers in terms of hardware:

| Feature                                  | PCs              | Tablet computers        |
| :--------------------------------------- | :--------------- | :---------------------- |
| :material-cursor-default: Input          | Mouse & keyboard | Multi-touch             |
| :material-fan: Thermal management        | Active           | Passive                 |
| :material-harddisk: Storage media        | Mainly spinning  | Solid-state             |
| :material-connection: Connectivity       | Mainly wired     | Wireless                |
| :material-memory: Level of integration   | Low              | High                    |
| :material-power: Power model             | On & off         | Wake & sleep, always on |
| :material-battery-charging: Power budget | High             | Low (smaller batteries) |

To make x86 platform suitable for mobile computing on tablet computers, Intel’s job is far more complicated than simply putting new low-TDP Atom or Celeron CPUs onto the market. In order to fit in the limited space of tablet computers, they need to provide high level of integration by making not just CPUs, but SoCs (System on a Chip), combining functionalities previously enabled by chips on motherboard like audio into the processor. Intel also needs to renovate their platform to fit Microsoft’s needs, particularly when it comes to Connected Standby.

### Windows 8

In October 2012[^7], a disaster called Windows 8 was released. To end users, the most obvious change is of course the design. When Windows 8 is first booted, the user is greeted with the OOBE (Out-of-box experience) screen featuring the new, minimalist flat design called “Metro”[^8]. If your graphics drivers are up and ready, the elegant, smooth animations and bold new colors will definitely give you a refreshing feel. Then you’re greeted with the brand new, full-screen Start Menu, maybe leaving you confused: where is my desktop? After spotting a rectangular tile called “Desktop” mixed in other rectangles, and a firm mouse click, congratulations, you have finally found your way to the familiar Windows desktop you know and love[^9]. Home sweet home, the recycle bin, the desktop wallpaper and the taskbar, they are all there, refreshed yet still with the spirit of Windows, and the Start But-wait, hold up, where has the Start Button gone?

Great, now you have it. *It’s not a bug, it’s a feature.*™ The Start Button is officially gone. In Microsoft’s defense, you can still open Start Menu with the Start key on your keyboard, or the physical Start button on your tablet, or in the Charms menu. You can also move your mouse cursor to the bottom left corner of the screen, revealing the Start Button.

Oh, and the Charms menu, one of the “corner/edge actions”, which features five submenus: Search, Share, Start (colored in current accent color), Devices, Settings, is a core design of Windows 8. As part of Windows 8’s touch-optimized design paradigm, gestures are important. For touch input, swiping left from the right edge brings up the Charms menu, swiping right from the left edge cycles through recently opened *Metro* apps and the Desktop, and swiping down from the top edge closes current app (including Desktop)[^10]. For mouse and keyboard input, move your mouse cursor to the two corners on the right side of the display, and then vertically to bring up the Charms menu. Move it to the two corners on the left side of the display and then vertically to bring up the recently opened *Metro* apps list. Clicking the top-left corner will cycle through recently opened *Metro* apps and the Desktop. Oh, you can also bring up the Charms menu by pressing ++win+c++ key combo.

It’s already getting very boring and complicated. You thought to your self: “ok, I’ve had enough”. When you try to shut it down, if you’re on a tablet, then great, just hold the power button and swipe down when the meticulously crafted “Slide to shut down your PC” screen shows up. However, if you are unfortunately on a desktop or laptop, you may discover yet another surprise: “how the heck am I gonna shut this thing down” as there’s no freaking power button or menu on the Start Menu? Then you start searching for “how to shut down Windows 8”, as you find hundreds of thousands of confused users, just like you, asking the same question of how to turn off a computer, with Windows 8 installed. Turns out it’s buried so deeply into the Charms menu that pressing ++alt+f4++ on the desktop and selecting Shut down, or even pressing ++win+r++ and then typing `shutdown /s /t 0` is faster than using Charms menu to turn off the computer. To turn off your computer, open Charms menu however you like, then click or tap “Settings”, then “Power”, then “Shut down”. It was so bad that Microsoft quickly released Windows 8.1 exactly a year later in an attempt to fix the hate it received. Windows 8.1 brought back the Start Button, made it possible to enter the desktop once logged in, and added a power button on the Start Menu, among other fixes and touchups.

### Metro apps

I kept mentioning *Metro* apps, but did you really know what they are? They are also known as “Windows Store apps”, built on the new framework called “Windows Runtime” or WinRT (not to be confused with Windows RT, which we will discuss about later). Contrary to its name, it is not a runtime, but a new set of APIs for a new kind of applications that is *Metro* apps, they are mostly packaged, run in a sandbox, published to and acquired from Microsoft Store (formerly Windows Store), and require permissions and user approvals to use specific functionalities, kind of like on mobile operating systems such as Android and iOS. You can see it as Microsoft’s attempt to bring Android & iOS-style apps to Windows. They all run full-screen, are touch-first, and share the Microsoft Design Language.

There you go, after traditional Windows APIs and WPF, here comes the third kind of applications on Windows. The good thing, and also a problem is that they all run on Windows 8. Counting the classic Windows style and the Ribbon UI introduced with Office 2007, Microsoft has already got at least 5 styles of user interfaces and 3 frameworks, scattered across the operating system.

### Windows RT

## Universal Windows

## The rise of Chromium

## Project Reunion

## Did Microsoft learn anything?

[^1]: See the [Neowin report :octicons-link-external-16:](https://www.neowin.net/news/windows-95-start-up-music-composed-on-a-mac/).
[^2]: Microsoft headquarters is located in Redmond, Washington, United States.
[^3]: You can still do it in IDE’s designer when developing WPF applications, but it is no longer recommended.
[^4]: Years later in 2021, Intel’s new CEO (also an Intel veteran), Pat Gelsinger reportedly said the quote in a report by [The Verge :octicons-link-external-16:](https://www.theverge.com/2021/1/15/22232554/intel-ceo-apple-lifestyle-company-cpus-comment). Referring to Apple Inc.
[^5]: Quote source: [ZDNET report :octicons-link-external-16:](https://www.zdnet.com/article/ces-windows-to-run-on-arm-chips-says-microsoft/).
[^6]: See LTT’s rant about Modern Standby: [:fontawesome-brands-youtube: Microsoft is Forcing me to Buy MacBooks - Windows Modern Standby](https://www.youtube.com/watch?v=OHKKcd3sx2c).
[^7]: Time of General Availability (GA), Windows 8 RTM (Released to Manufacturing) was earlier on August 1, 2012.
[^8]: Per Microsoft, *Metro* has always meant to be an internal codename only. Its other name, “Modern UI” came from Microsoft executive Qi Lu [on the MIXX conference :octicons-link-external-16:](https://news.microsoft.com/2012/10/01/qi-lu-iab-mixx-conference-keynote/). Later Microsoft confirmed ([ZDNET report :octicons-link-external-16:](https://www.zdnet.com/article/microsoft-design-language-the-newest-official-way-to-refer-to-metro/)) its official name as “Microsoft Design Language”.
[^9]: Your milage may vary.
[^10]: While “Desktop”, as a *Metro* app, is closed, all Windows desktop applications and their windows remained open. You normally cannot return to desktop until you click or tap the Desktop tile in the Start Menu again. This adds another layer of confusion to users.
