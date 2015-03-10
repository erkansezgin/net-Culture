# DefaultThreadCulture

[![build](https://ci.appveyor.com/api/projects/status/github/tallesl/DefaultThreadCulture)](https://ci.appveyor.com/project/TallesL/DefaultThreadCulture)
[![nuget package](https://badge.fury.io/nu/DefaultThreadCulture.png)](http://badge.fury.io/nu/DefaultThreadCulture)

Sets a default for [Thread.CurrentCulture](https://msdn.microsoft.com/library/system.threading.thread.currentculture.aspx) or [ThreadCurrentUICulture](https://msdn.microsoft.com/library/system.threading.thread.currentuiculture.aspx). Works from .NET 4.5 to 2.0.

## Usage

```cs
using DefaultThreadCulture;

var brazilianPortuguese = new CultureInfo("pt-BR");
DefaultThreadCurrentCulture.SetCulture(brazilianPortuguese);
DefaultThreadCurrentCulture.SetUICulture(brazilianPortuguese);
```

## How it works

First, attempts to set [CultureInfo.DefaultThreadCurrentCulture](https://msdn.microsoft.com/library/system.globalization.cultureinfo.defaultthreadcurrentculture.aspx) (or [CultureInfo.DefaultThreadCurrentUICulture](https://msdn.microsoft.com/library/system.globalization.cultureinfo.defaultthreadcurrentuiculture.aspx) for UI), a .NET 4.5 hidden property.

Then, if the first didn't succeed, attempts to set `s_userDefaultCulture` (or `s_userDefaultUICulture` for UI), a .NET 4.0 hidden field.

Finally, if both first and second steps didn't succeed, attempts to set `m_userDefaultCulture` (or `m_userDefaultUICulture` for UI), a .NET 2.0 hidden field.

Kudos to [this SO answer](http://stackoverflow.com/a/7536117) for poiting out those private fields.
