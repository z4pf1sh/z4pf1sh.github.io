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

It's been 40 years since Windows was first introduced, and even longer for MS-DOS, which was introduced 2 years prior to Windows. Over almost half a century, Windows has evolved through many iterations. Its kernel, for example, has evolved from MS-DOS, to MS-DOS-based, to NT. Till now, the latest version of Windows is Windows 11. There is certainly no denying that every single modern operating system, including Windows, is a feat of engineering. But shiny as it is, Windows is a piece of software that is way too big. And history relics have found their way to today, some hiding in the corners, some visible everyday, most remain untouched for years. This creates a feel of inconsistency, making Windows messy and segmented, sharply visible in user interface.

## Simpler times

Microsoft has a very terrible track record of maintaining stuff. From Silverlight to Zune, from Metro apps to UWP, some of which are confirmed *D-E-A-D* dead, while some are de-facto dead. This has always been a problem troubling Microsoft, despite it being still pretty managable in the XP era. Back then, for native application development, Microsoft offered developers a simple option: [Win32 MFC^:fontawesome-brands-wikipedia-w:^](https://en.wikipedia.org/wiki/Microsoft_Foundation_Class_Library) with C or C++. While developing Windows XP, Microsoft was also working on something called “.NET Framework”, formerly “Next Generation Windows Services” - a revolutionary framework that was set to make native application development way easier, safer, more efficient and reliable than ever before.

.NET Framework was a great idea, with C#, one the bundled languages, it introduced a [generational garbage collection^:fontawesome-brands-wikipedia-w:^](https://en.wikipedia.org/wiki/Tracing_garbage_collection#Generational_GC_(ephemeral_GC)) automatic memory management mechanism to developers familiar with C and C++ syntaxes, freeing them from the hassle of error-prone manual memory management. It's like driving manual vs. automatic transmission cars. Sure, if you are skilled enough, manual could be better than automatic for 85% of the time, but for everyone else automatic is (way) better than manual for 99% of the time. Even better, as a brand new language with a brand new framework, Microsoft took their time to painstakingly wrap traditional C++ Win32 APIs into their brand new form in .NET Framework. Gone are the ugly `typedef`s like `LPCTWSTR` or obsolete ones like `DWORD`, say hello to the new, unified keywords like `string` and `int`. There is no need to listen for [Windows Messages^:fontawesome-brands-wikipedia-w:^](https://en.wikipedia.org/wiki/Message_loop_in_Microsoft_Windows), just use events and their respective handlers. You don't even need to write a main loop, the framework also does that for you, and events are automatically delivered to your application, rather than you having to actively retrieve it first. Things are looking great so far. Everything looks promising, and when it was released in February 13, 2002, developers are quickly adopting to this new piece of technology, in hope to improve their workflow and make future development easier and faster.

The initial framework in .NET Framework for graphical user interfaces is Windows Forms. In a nutshell, it is a wrapper of Win32 APIs used to create native applications with native Windows controls and widgets. So things made with Windows Forms will look and behave just the same as if they've been written with Win32 MFC. Who doesn't like it when you have more than one technical choices to achieve the same thing? As time went on, .NET Framework gained popularity among developers for its ease of use and overall better experience than C++ Win32 development. It seemed like Microsoft finally made a worthy, modern candidate to challenge the almighty Win32's reign.

## Enter WPF

But unfortunately, at this point, Microsoft was already a very bureaucratic corporation. Somewhere in a small office in Redmond, WA, someone suggested that Windows Forms is just not *revolutionary* enough. Think about it, it was just a wrapper for the existing Win32 APIs that it was set to replace in the first place. How could you replace something when you still depend on it?

[^1]: See the [Neowin report :octicons-link-external-16:](https://www.neowin.net/news/windows-95-start-up-music-composed-on-a-mac/).
