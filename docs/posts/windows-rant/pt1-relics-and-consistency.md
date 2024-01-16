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

Microsoft has a very terrible track record of maintaining stuff. From Silverlight to Zune, from Metro apps to UWP, some of which are confirmed *D-E-A-D* dead, while some are de-facto dead. This has always been a problem troubling Microsoft, despite it being still pretty manageable in the XP era. Back then, for native application development, Microsoft offered developers a simple option: [Win32 MFC^:fontawesome-brands-wikipedia-w:^](https://en.wikipedia.org/wiki/Microsoft_Foundation_Class_Library) with C or C++. While developing Windows XP, Microsoft was also working on something called “.NET Framework”, formerly “Next Generation Windows Services” - a revolutionary framework that was set to make native application development way easier, safer, more efficient and reliable than ever before.

.NET Framework was a great idea, with C#, one the bundled languages, it introduced a [generational garbage collection^:fontawesome-brands-wikipedia-w:^](https://en.wikipedia.org/wiki/Tracing_garbage_collection#Generational_GC_(ephemeral_GC)) automatic memory management mechanism to developers familiar with C and C++ syntaxes, freeing them from the hassle of error-prone manual memory management. It’s like driving manual vs. automatic transmission cars. Sure, if you are skilled enough, manual could be better than automatic for 85% of the time, but for everyone else automatic is (way) better than manual for 99% of the time. Even better, as a brand new language with a brand new framework, Microsoft took their time to painstakingly wrap traditional C++ Win32 APIs into their brand new form in .NET Framework. Gone are the ugly `typedef`s like `LPCTWSTR` or obsolete ones like `DWORD`, say hello to the new, unified keywords like `string` and `int`. There is no need to listen for [Windows Messages^:fontawesome-brands-wikipedia-w:^](https://en.wikipedia.org/wiki/Message_loop_in_Microsoft_Windows), just use events and their respective handlers. You don’t even need to write a main loop, the framework also does that for you, and events are automatically delivered to your application, rather than you having to actively retrieve it first. Things are looking great so far. Everything looks promising, and when it was released in February 13, 2002, developers are quickly adopting to this new piece of technology, in hope to improve their workflow and make future development easier and faster.

The initial framework in .NET Framework for graphical user interfaces is Windows Forms. In a nutshell, it is a wrapper of Win32 APIs used to create native applications with native Windows controls and widgets. So things made with Windows Forms will look and behave just the same as if they’ve been written with Win32 APIs. Who doesn’t like it when you have more than one technical choices to achieve the same thing? As time went on, .NET Framework gained popularity among developers for its ease of use and overall better experience than C++ Win32 development. It seemed like Microsoft finally made a worthy, modern candidate to challenge the almighty Win32’s reign.

## Enter WPF

But unfortunately, at this point, Microsoft was already a very bureaucratic corporation. Somewhere in a small office in Redmond, WA[^2], someone suggested that Windows Forms is just not *revolutionary* enough. Think about it, it was just a wrapper for the existing Win32 APIs that it was set to replace in the first place. How could you replace something when you still depend on it?

The team came up with something codenamed “Avalon”, and planned to make some aggressive and radical technological advancements under the hood. First, UI composition will be accelerated by GPU with DirectX. Then the UI is defined by XAML, instead of drag-and-drop in IDE[^3] or bunches of repetitive `new()` and `Controls.Add()` calls. Proper high-DPI display support became a reality, and dynamic data binding is now the recommended standard approach. Its name is later revealed as “Windows Presentation Foundation”, or WPF for short. WPF was officially released in November 21, 2006, 4 years after Windows Forms. In a technological sense, WPF is a huge leap over Windows Forms. It is no longer just a wrapper for Win32 APIs, but a brand new framework with brand new architecture.

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
    to the `<Window.Resources>` part and et-voilà!

## iPad and rushed response

The iPad, released in April 2010, was set to fill the gap between smartphones and computers. It’s categorized as a “tablet computer”, which apparently caught Microsoft off their guard.

## Universal Windows

## The rise of Chromium

## Project Reunion

## Did Microsoft learn anything?

[^1]: See the [Neowin report :octicons-link-external-16:](https://www.neowin.net/news/windows-95-start-up-music-composed-on-a-mac/).
[^2]: Microsoft headquarters is located in Redmond, Washington, United States.
[^3]: You can still do it in IDE’s designer when developing WPF applications, but it is no longer recommended.
