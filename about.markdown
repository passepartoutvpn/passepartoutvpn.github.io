---
layout: page
---

## About

- [The Team](#the-team)
- [How Passepartout was born](#how-passepartout-was-born)
- [PassepartoutKit: The "new" TunnelKit](#passepartoutkit-the-new-tunnelkit)
- [The story behind TunnelKit](#the-story-behind-tunnelkit)

### The Team

I'm [Davide][web-author], the "team" behind every aspect of Passepartout.

Bear with me because my duties entail, among others:

- Planning ([GitHub Projects][duties-planning])
- Design and Development ([GitHub][duties-code])
- Testing ([TestFlight][duties-testflight])
- CI/CD ([GitHub Actions][duties-ci-cd])
- Localization (GPT)
- Customer Care ([Reddit][duties-reddit], App Store)
- This website

### How Passepartout was born

Today, Passepartout is a comprehensive networking/privacy tool [for iPhone, iPad, Mac, and Apple TV][web-appstore].

How did it start?

During my days at PIA, I wondered why there were so many VPN providers doing the same over and over with different skins: an app with a VPN on/off toggle.

I came up with the idea of a *single key* that would open *multiple doors*, be it different protocols, providers, or platforms. That's [what the word *Passepartout* stands for in French][web-passepartout-meaning], a *master key*.

Frustrated by the abandonment of OpenVPN Connect, I first published Passepartout in 2018 as an OpenVPN client for iOS based on [TunnelKit](#the-story-behind-tunnelkit), an alternative implementation of OpenVPN that I started in 2017. Through the years, the app has become multiplatform, and WireGuard support was also added.

<a href="/s/about/01.png"><img src="/s/about/01.png" alt="The old Mac app" style="width: 100%" />

### PassepartoutKit: The "new" TunnelKit

Unfortunately, TunnelKit was not designed for the original concept of Passepartout, so [the app ended up lagging behind its limitations][reddit-tunnelkit]. Beyond that, the library architecture was in general very primitive, tightly coupled to OpenVPN and OpenSSL, and hard to test.

That's why I dedicated a relevant part of 2023/2024 to a completely new library, [PassepartoutKit][github-passepartoutkit], a huge rewrite that was, however, worth the pain. It's a well-thought architecture that leverages the experience I gained with TunnelKit and WireGuardKit for OpenVPN and WireGuard connectivity.

*PassepartoutKit* is a game changer in that:

- It is much easier to deploy and use
- It is more stable, for using strict [Swift Concurrency][web-swift-concurrency]
- It is agnostic of OpenSSL, WireGuard, and even [Network Extension][web-network-extension]
- It handles multiple protocols in a single [Packet Tunnel Provider][web-packet-tunnel-provider]
- It is not bound to VPN
- It opens the doors to other platforms like Windows and Android
- Last but not least, it is widely mockable/testable

Contrary to TunnelKit, which is available under the GPL, *PassepartoutKit* is currently closed-source.

Feel free to [contact me][email-info] for licensing or further information.

<a href="/s/about/02.png"><img src="/s/about/02.png" alt="A glance at PassepartoutKit documentation" style="width: 100%" />

### The story behind TunnelKit

[TunnelKit][github-tunnelkit] is a custom Swift/ObjC implementation of the OpenVPN protocol, written from scratch and now superseded by *PassepartoutKit*.

It all started in 2017, when a former colleague at [Private Internet Access][web-pia] sent me some Ruby snippets that would connect to an OpenVPN server. He would then ask me: "would you port this to the iPhone?"

Well, not only did I, but the guy left the company a few weeks later. I took care of the project alone for the next 7 years.

TunnelKit is the only stable OpenVPN implementation in native Swift/ObjC out there and, believe it or not, it is relied on by *millions* of users, be it via my apps or providers like [Hide.me][web-hideme], [PIA][web-pia], or [ProtonVPN][web-protonvpn].

A pretty _big_ project, huh?

<a href="/s/about/03.png"><img src="/s/about/03.png" alt="An old excerpt from TunnelKit" style="width: 100%" />

[web-author]: {{ site.author_url }}
[web-appstore]: {{ site.itunes_url }}

[duties-testflight]: {{ site.testflight_url }}
[duties-reddit]: {{ site.reddit.url }}
[duties-code]: https://github.com/passepartoutvpn
[duties-planning]: https://github.com/orgs/passepartoutvpn/projects
[duties-ci-cd]: https://github.com/passepartoutvpn/passepartout/actions

[github-passepartoutkit]: https://github.com/passepartoutvpn/passepartoutkit
[github-tunnelkit]: https://github.com/passepartoutvpn/tunnelkit
[reddit-tunnelkit]: https://www.reddit.com/r/passepartout/comments/1bw4esv/the_looks_of_tunnelkit_20172024/

[web-author]: https://davidederosa.com/
[web-hideme]: https://hide.me/
[web-pia]: https://www.privateinternetaccess.com/
[web-protonvpn]: https://protonvpn.com/
[web-passepartout-meaning]: https://dictionary.cambridge.org/dictionary/french-english/passe-partout
[web-swift-concurrency]: https://docs.swift.org/swift-book/documentation/the-swift-programming-language/concurrency/
[web-network-extension]: https://developer.apple.com/documentation/networkextension
[web-packet-tunnel-provider]: https://developer.apple.com/documentation/networkextension/nepackettunnelprovider

[email-info]: mailto:{{ site.email.info }}
