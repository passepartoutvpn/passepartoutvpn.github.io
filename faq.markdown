---
layout: page
---

## Frequently Asked Questions

- [The app is asking me to purchase a feature I don't use](#the-app-is-asking-me-to-purchase-a-feature-i-dont-use)
- [Apple TV profiles do not sync after upgrading](#apple-tv-profiles-do-not-sync-after-upgrading)
- [Apple TV profiles stopped working due to paid features](#apple-tv-profiles-stopped-working-due-to-paid-features)
- [The app is stuck on 'Verifying...'](#the-app-is-stuck-on-verifying)
- [Where do I put my OpenVPN credentials?](#where-do-i-put-my-openvpn-credentials)
- [Can I share the purchases with my family?](#can-i-share-the-purchases-with-my-family)
- [Why use iCloud to share profiles with the Apple TV?](#why-use-icloud-to-share-profiles-with-the-apple-tv)
- [My profile does not appear on the Apple TV](#my-profile-does-not-appear-on-the-apple-tv)
- [I am concerned with iCloud privacy](#i-am-concerned-with-icloud-privacy)
- [I cannot see my profiles on another device](#i-cannot-see-my-profiles-on-another-device)
- [Why don't Shortcuts execute in the background?](#why-dont-shortcuts-execute-in-the-background)
- [I'd like to use WireGuard with providers](#id-like-to-use-wireguard-with-providers)
- [I'd like to see a Widget](#id-like-to-see-a-widget)
- [I'm unable to add my Wi-Fi to on-demand networks](#im-unable-to-add-my-wi-fi-to-on-demand-networks)
- [I had purchased this app before yet it prompts me for purchases](#i-had-purchased-this-app-before-yet-it-prompts-me-for-purchases)
- [I had purchased this app before yet TestFlight builds are restricted](#i-had-purchased-this-app-before-yet-testflight-builds-are-restricted)
- [My provider is not listed](#my-provider-is-not-listed)
- [I'm on Wi-Fi but my device shows I'm connected via LTE](#im-on-wi-fi-but-my-device-shows-im-connected-via-lte)
- [Why is location access required when adding a Wi-Fi network to on-demand?](#why-is-location-access-required-when-adding-a-wi-fi-network-to-on-demand)
- [I can connect to the VPN but the Internet does not work](#i-can-connect-to-the-vpn-but-the-internet-does-not-work)
- [The VPN fails with "Auth failed" or immediately disconnects with "Encryption failed"](#the-vpn-fails-with-auth-failed-or-immediately-disconnects-with-encryption-failed)
- [My provider returns "Auth failed" but my credentials are correct](#my-provider-returns-auth-failed-but-my-credentials-are-correct)
- [My personal server returns "TLS failed"](#my-personal-server-returns-tls-failed)
- [The configuration file lacks a required option (cipher)](#the-configuration-file-lacks-a-required-option-cipher)
- [The configuration file contains an unsupported option (external file)](#the-configuration-file-contains-an-unsupported-option-external-file)
- [It seems that my traffic doesn't necessarily go through the VPN](#it-seems-that-my-traffic-doesnt-necessarily-go-through-the-vpn)
- [I'd like to see my IP address in the app](#id-like-to-see-my-ip-address-in-the-app)
- [Mullvad ignores my custom DNS settings](#mullvad-ignores-my-custom-dns-settings)

### The app is asking me to purchase a feature I don't use

__DO NOT make the purchase__. This is a bug and it is resolved in the latest version (3.0.2+), please upgrade.

Check [this thread for updates](https://www.reddit.com/r/passepartout/comments/1i48waz/issues_in_300_to_be_resolved_asap/).

#### Apple TV required for old iOS/macOS purchasers

(Jan 22) Please update the app, this is fixed.

#### Migrated profiles may erroneously require the on-demand feature

(Jan 22) Please update the app, this is fixed.

The temporary workaround is:

- Edit the migrated profile
- Tap "On-demand"
- You surely have empty rules
- Set "Policy" to "All networks"

The orange icon will go away and you will connect as usual.

### Apple TV profiles do not sync after upgrading

For profiles to sync properly on your TV, ALL apps must be upgraded to 3.0.0, not only the Apple TV. Make sure to upgrade your iOS and macOS apps and you should be good to go.

### The app is stuck on 'Verifying...'

Validating Apple purchases for the first time may take up to one minute, especially if the device was just booted. If warning signs appear on your profiles -meaning that validation failed-, please close and reopen the app and everything should be fine.

### Where do I put my OpenVPN credentials?

Some users are having a hard time finding the OpenVPN credentials.

Truth is, when you edit a profile on iOS/macOS via the "..." button, you will see a list of "Modules", like "OpenVPN". Those rows are actually clickable. Touch "OpenVPN" and you will find a "Credentials" entry.

The UX of 3.0.0 will go through incremental refinements, so this will certainly be improved based on your feedback.

### Can I share the purchases with my family?

Yes, all purchases support Family Sharing.

### Why use iCloud to share profiles with the Apple TV?

As of December 2024, the Apple TV is still limited when it comes to file transfers. AirDrop and iCloud Drive are the most natural options for one-off "import and delete" of a profile, but they are not available. Another option is setting up a local server with a QR, but I find it quite a cumbersome UX.

Therefore, given that Passepartout supports end-to-end CloudKit encryption, iCloud proved a decent trade-off between usability and privacy. Besides the convenience of the simple toggle, the iOS/macOS apps act as a remote to reflect local changes instantly on your Apple TV. This benefits the UX of the TV app dramatically, where you only use the remote to change the profile or toggle the connection.

Bear in mind that only "Apple TV" profiles are shared and synchronized over iCloud implicitly. Other profiles follow the "iCloud > Enabled" toggle (in 3.0.0) or the global iCloud app preference (before 3.0.0).

### My profile does not appear on the Apple TV

If you are using the latest app, and the iCloud and TV icons are barred, this is a sign of iCloud not working or a feature not being credited. Kill and reopen the app, and make sure that the "iCloud" or "Apple TV" features are enabled in Settings > Purchases.

Make sure that the Apple ID of the **default account** of the Apple TV is the same Apple ID of the iOS/macOS device you are sharing the profile from. I could be wrong, but it seems to me that other accounts don't get proper iCloud updates like the default account, i.e. the one you set up the Apple TV with.

### I am concerned with iCloud privacy

Starting from version 2.2.0, iCloud synchronization is opt-in and disabled by default. Those upgrading to 2.2.0 will still see the option enabled to reflect the current app state, but you may disable it at any time. Rest assured that version 2.3.0, however, introduces end-to-end profile encryption.

If you mean to recover the best privacy, after disabling iCloud from the app, you may erase the existing store so that your profiles only stay on your device. If that is not enough, enter your iCloud settings, look for Passepartout inside "Manage Account Storage" and tap "Delete Data From iCloud".

### I cannot see my profiles on another device

If you have iCloud enabled and have updated the app to 2.3.0 on one device, other devices with an older version may be unable to read the profiles because of end-to-end encryption. Update all your devices to 2.3.0 to recover them.

Also there was another bug in 2.3.0 that was preventing profiles from being saved to iCloud at all. Cycling the "Sync with iCloud" toggle should restore proper syncing.

### Why don't Shortcuts execute in the background?

They finally do!

Starting from version 3.0.0, Passepartout stores one VPN configuration per profile. This means you can build your workflows directly from the Apple Shortcuts app and that they can execute in the background.

Use the "Set VPN" action in Shortcuts and pick your profiles by name. Beware that having on-demand enabled may affect some automation.

The "Connect to provider server" automation is a bit more complex but will be restored soon.

#### 2.3.x

Unfortunately, Apple is guilty of not fixing a related bug. I mean, it's been there for years -since iOS 9 with my first bug report dating back to 2017- without them caring at all. No feedback and not even a proper response. And of course, no progress.

This is one of the several threads remarking the issue:

<https://forums.developer.apple.com/thread/96020>

Now, due to this bug, App Extensions can't control VPN using custom protocols -Siri Intents Extension in this case, in order to run shortcuts in the background. Only native VPN protocols work (IKEv2, IPsec etc.).

In short, there's really *nothing* I can do about it.

### I'd like to use WireGuard with providers

I'm working on it.

### I'd like to see a Widget

I'm working on it.

### I'm unable to add my Wi-Fi to on-demand networks

#### 1.9.0 [iOS]

If you see the "You are not connected to any Wi-Fi network." message, it's coming from a [known iOS 13 bug](https://forums.developer.apple.com/thread/123544).

Until Apple fixes it, you may want to try these workarounds:

- Reboot the device
- Reinstall the app from scratch

Unfortunately neither is guaranteed to work. While extremely sorry for the inconvenience, I can't do more than this about this iOS bug.

Anyway, you can follow [this Reddit discussion](https://www.reddit.com/r/passepartout/comments/dt0fxy/read_this_if_you_cannot_add_your_wifi_to_trusted/) for updates.

#### 1.8.1 and before [iOS]

The effect of the new location access requirement in iOS 13 is the inability to add the connected Wi-Fi network. The app will either trust a bogus "Wi-Fi" or "WLAN" SSID name, or present the alert "You are not connected to any Wi-Fi network.".

To work around this issue:

- Add the network while the VPN is enabled and connected through such network.
- Upgrade Passepartout to the latest version (much, much better option).

### I had purchased this app before yet it prompts me for purchases

Since iOS version 1.9.0, Passepartout switched to a freemium model, which means free to download with paid in-app purchases. Of course, those who purchased former versions of the app will retain full access to all features and providers, except for the "Apple TV" feature which is a separate purchase. Most of the time the upgrade will be seamless. In some cases, however, it will take those users an extra step to restore app functionalities.

Any of the hints below will fix the issue 100% of the times:

- Kill and relaunch the app. This is preferred when you re-download the app from scratch.
- When prompted for purchase, tap "Restore purchases". You will only be asked for your Apple ID credentials, no money involved.

If you still struggle, don't hesitate to get in touch.

### I had purchased this app before yet TestFlight builds are restricted

Starting from 2.2.0, Public Beta builds from TestFlight recognize in-app purchases that you formerly made on the App Store.

For that to happen:

- Install the app from App Store first
- If a paywall is triggered, restore your purchases
- DO NOT uninstall the app, install a TestFlight build over the one you have
- You should now see, in beta, the features you purchased on the App Store

On the other hand, if you install a TestFlight build from scratch, paid features will not be available.

*WARNING: this trick is only effective on iOS.*

### My provider is not listed

You should contact with your provider to double check if there is interest in being added to Passepartout. Beware that some may be concerned instead. Ultimately, you can submit your provider request for a viability review to [{{ site.email.providers }}](mailto:{{ site.email.providers }}).

### I'm on Wi-Fi but my device shows I'm connected via LTE

The Wi-Fi/LTE icon (replace LTE with any cellular signal) while on VPN has been broken since iOS 10 or the like. It's something that Apple is unable to fix or doesn't bother fixing.

You should do a simple test. Verify your data consumption with your LTE provider website, normally phone providers have that. Now, when on VPN and the LTE icon appears in spite of Wi-Fi, download a relevant chunk of data. You may then learn that the plan is unaffected, implying that you're actually connected via Wi-Fi.

I haven't found a workaround for this and it's been there for almost two years. Yeah, it's a shame.

### Why is location access required when adding a Wi-Fi network to on-demand?

Starting from iOS 12 (or 13?), iOS has restricted what apps can learn about Wi-Fi networks. Location access has become a requirement to access the SSID of the connected Wi-Fi, which is crucial to add it to on-demand networks.

That's why, starting from iOS app 1.9.0, Passepartout will prompt you for a location permission when adding a Wi-Fi network. Make sure that location services (under "Privacy") are enabled on your device, otherwise the app will be unable to ask the permission in the first place.

### I can connect to the VPN but the Internet does not work

#### MTU

Historically, Passepartout has used a low MTU setting (1250 bytes) in order to maximize compatibility, at the cost of performance. iOS version 1.13.0 -and any macOS version- supports tunnel MTU customization. With this update, it sounded reasonable to also leverage a standard (higher) MTU (usually 1500).

If such a change is making the app struggle in your environment, I encourage you to try lowering the MTU.

Add a "Routing" module to your profile and specify a custom MTU value. Decrease incrementally until you restore the VPN operation.

##### 2.3.x

You can change the MTU by setting MTU to "Manual" in "Network settings". You will then be able to pick something down to 1200 bytes.

#### Compression

Most of the time there could be a mismatch in compression framing. E.g. server is using LZO compression framing whereas the client is not, or vice versa. Sometimes the app gracefully shuts down with "Compression unsupported", sometimes the error can be subtle and packet transmission could just fail silently, resulting in no data exchanged over the wire.

Therefore, make sure that compression directives are compatible between client and server before looking into routing issues. Also read the next FAQ entry, as it may be another cause of a dead data link.

#### DNS

Last but not least: make sure that you're not experiencing a simple DNS issue. Try pinging a remote machine by IP address: if that works, then DNS is the culprit. This usually happens when your server, whatever the reason, doesn't push public DNS servers to clients.

There's a quick workaround: add a "DNS" module in your profile and add an explicit DNS server address. That should fix it.

##### 2.3.x

Enter "Network settings", set "DNS" to "Manual" and add an explicit DNS server address.

### The VPN fails with "Auth failed" or immediately disconnects with "Encryption failed"

This may happen when you rely on default OpenVPN encryption, which is normally Blowfish (BF-CBC). The algorithm, besides being unsupported by Passepartout, is also weak and therefore discouraged. In order to fix this issue, you must switch to AES encryption. Passepartout only supports AES, be it in CBC or GCM mode.

Set encryption explicitly in the server configuration, e.g.:

    cipher AES-128-CBC
    auth SHA1

and don't forget to update the client .ovpn as well with the **exact same parameters**.

If you want to leverage newer AES-GCM encryption, you could just use:

    ncp-ciphers AES-256-GCM
    # or
    ncp-ciphers AES-128-GCM

and the client wouldn't need to change a thing, because the algorithm will be enforced by the server no matter what.

### My provider returns "Auth failed" but my credentials are correct

Bear in mind that some providers require specific credentials for their direct OpenVPN servers. That's why Passepartout, in those cases, has a convenient link at the bottom of the OpenVPN "Credentials" screen ("Account" in 2.3.x), showing you where to find such credentials on your provider's website.

Regarding Mullvad in particular, remember to strip spaces from the username.

### My personal server returns "TLS failed"

This may happen with older ciphersuites when verifying peer against the CA. You should upgrade your server certificates to a more modern standard (e.g. RSA no less than 2048-bit).

### The configuration file lacks a required option (cipher)

When missing, OpenVPN implies a Blowfish cipher, which is severely obsolete and unsupported. Passepartout requires that you set an AES cipher instead. For that to work, you must update your OpenVPN server and client configuration to use AES by explicitly setting a cipher (e.g. `cipher AES-128-CBC`).

Recent servers might still be pushing a modern cipher option (normally AES-GCM), but Passepartout enforces an explicit client `cipher` to avoid [another subtle issue](#the-vpn-fails-with-auth-failed-or-immediately-disconnects-with-encryption-failed).

### The configuration file contains an unsupported option (external file)

Due to easier interoperability, the app does not support external files in the .ovpn main configuration. That's because more often than not, it may not make sense referring to relative paths in a mobile device environment. Think of the Mail app for example. The fix is straightforward though, say you have an external `ca` file:

    ca my-ca.crt

Just replace it with:

    <ca>
    ...
    content of my-ca.crt
    ...
    </ca>

The same applies to other settings like `cert`, `key`, `tls-auth` and `tls-crypt`. In the specific case of `tls-auth` with a key direction, like:

    tls-auth ta.key 1

Replace with:

    <tls-auth>
    ...
    content of ta.key
    ...
    </tls-auth>
    key-direction 1

### It seems that my traffic doesn't necessarily go through the VPN

Talking about OpenVPN, unless `redirect-gateway` is either:

- Explicitly added to the .ovpn configuration
- Pushed by the server

the default gateway is NOT changed. That is, your external IP won't be the VPN's IP. This is not the case for provider profiles, though, where the default gateway is always *enforced* to be the provider gateway to avoid unintended leaks.

Try [this website](https://www.iplocation.net/) to test your external IP before and after this change.

### I'd like to see my IP address in the app

The reason why Passepartout does not present any personal information in app is _privacy_. Obtaining one's IP address, regardless of being connected to a VPN or not, involves querying -and trusting- a third party service. Knowing such info is also of little use, given that most of the time you don't want to share your VPN IP address and therefore link your identity to it. However, this feature might be introduced later as a diagnostic tool.

### Mullvad ignores my custom DNS settings

It looks like Mullvad "hijacks" DNS on default endpoints, making custom DNS settings irrelevant. In order to do custom DNS with Mullvad, make sure to explicitly pick the "Custom DNS" preset, which will let you connect to the UDP:1400 and TCP:1401 endpoints. These endpoints do support custom DNS servers instead.

Until version 1.7.0 for iOS, you will have to do a manual "Refresh infrastructure" in order to access the new preset.

Read the [related report on GitHub](https://github.com/passepartoutvpn/api-source-mullvad/issues/1).

[icloud-opt-in]: https://www.reddit.com/r/passepartout/comments/16dyfp5/on_icloud_feature/
