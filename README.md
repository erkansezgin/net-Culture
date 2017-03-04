# Culture

[![][build-img]][build]
[![][nuget-img]][nuget]

Sets a default for [Thread.CurrentCulture] or [ThreadCurrentUICulture].

[build]:                  https://ci.appveyor.com/api/projects/status/github/tallesl/net-culture
[build-img]:              https://ci.appveyor.com/api/projects/status/github/tallesl/net-socket?svg=true
[nuget]:                  https://www.nuget.org/packages/Culture
[nuget-img]:              https://badge.fury.io/nu/Culture.svg
[Thread.CurrentCulture]:  https://msdn.microsoft.com/library/System.Threading.Thread.CurrentCulture
[ThreadCurrentUICulture]: https://msdn.microsoft.com/library/System.Threading.Thread.CurrentUICulture

## Usage

```cs
using CultureLibrary;

var br = new CultureInfo("pt-BR");
Culture.SetDefault(br);
Culture.SetUIDefault(br);
```

## How it works

First, attempts to set [CultureInfo.DefaultThreadCurrentCulture] (or [CultureInfo.DefaultThreadCurrentUICulture] for
UI), a .NET 4.5 property.

Then, if the first didn't succeed, attempts to set `s_userDefaultCulture` (or `s_userDefaultUICulture` for UI), a .NET
4.0 hidden field.

Finally, if both first and second steps didn't succeed, attempts to set `m_userDefaultCulture` (or
`m_userDefaultUICulture` for UI), a .NET 2.0 hidden field.

Kudos to [this SO answer] for pointing out those private fields.

[CultureInfo.DefaultThreadCurrentCulture]:   https://msdn.microsoft.com/library/System.Globalization.CultureInfo.DefaultThreadCurrentCulture
[CultureInfo.DefaultThreadCurrentUICulture]: https://msdn.microsoft.com/library/System.Globalization.CultureInfo.DefaultThreadCurrentUICulture
[this SO answer]:                            http://stackoverflow.com/a/7536117
