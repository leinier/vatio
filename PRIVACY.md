---
title: Privacy Policy
permalink: /privacy/
---

# Vatio — Privacy Policy

_Last updated: 8 September 2026_

## Short version

Vatio does not collect anything about you, and nothing is shared with anyone.

By default everything stays on your device. There are two exceptions, and this
page explains both: notifications that arrive while the app is closed need a
small service that watches your meter while your device sleeps, and on iPhone
that same service also relays the app's own requests when your network cannot
reach Shelly. On iPhone the service is required for notifications to work at
all; on Mac it is optional and only used if you ask for an alert history.

## On your device

Everything is kept inside the app's own container:

- **Your Shelly session.** When you sign in, Shelly's cloud returns an access
  token. The app never sees your Shelly password: you type it on Shelly's own
  page, in a window the system provides. Signing out removes the token.
- **Your settings.** The electricity tariff, the day your billing period starts,
  the names you give each phase and the alerts you define. These are things you
  type; by themselves they never leave your device.

To show your consumption, the app talks to the Shelly cloud (`*.shelly.cloud`)
over HTTPS, reading the devices in your own account. It never controls or
reconfigures anything.

## Your home network

When the Shelly cloud cannot be reached, the app can read the meter directly
over your own network, so you can still see whether the power is on. macOS and
iOS ask your permission the first time.

It looks only for the Shelly service (`_shelly._tcp`) and speaks only to a meter
that answers as yours. It does not scan your network, does not list what else is
connected, and nothing read this way leaves your device.

## Between your own devices

If you use Vatio on more than one device with the same iCloud account, your
tariff, your alert rules, your phase names and your billing day travel between
them through Apple's iCloud key-value storage, so you do not have to type them
twice.

Your Shelly session and the service credential are deliberately left out: they
belong to each device, and copying them would break both.

## The watching service

A device that is asleep cannot notice that your power went out. iOS suspends
apps as a matter of course, and a Mac is closed or off much of the time. So a
small service runs in the cloud — on Cloudflare Workers — and checks your meter
every minute.

On iPhone it is what makes notifications possible, and it also acts as a relay:
some mobile networks cannot reach Shelly's cloud at all, so the app asks the
service instead and the service asks Shelly. On Mac none of this applies unless
you ask for it: the app warns you on its own while it is open, and the service
only adds a history of what happened while the Mac was not.

For that, the service stores, per account:

- **A Shelly session** (an access token and its refresh token), used only to
  read the consumption of your devices.
- **Your alert thresholds**, the outage warnings you enabled, the phase names,
  the phases you leave out of the totals and the day your billing period
  starts — everything it needs to warn you about the same figures the app shows.
- **The time zone and the language of your device**, so a warning arrives in
  your language and says the hour you read on your own clock rather than the
  server's.
- **A push identifier**, which is what Apple needs to deliver a notification. It
  says nothing about you and is discarded as soon as Apple reports the app is no
  longer installed.
- **A credential it issues to each of your devices**, so they can read their own
  alerts and nobody else's. Only a hash of it is kept.
- **A copy of the last status your meter reported** — the same readings the app
  shows — kept so the app can be answered without asking Shelly twice, and
  replaced every time a new one arrives.
- **Today's and this period's consumption in kWh**, refreshed every few minutes,
  for alerts about how much you have used.
- **The last hundred warnings it sent you**, which is the alert history you see
  in the app. Each one holds the reading that triggered it and when.
- **A short record of when the meter was unreachable**, so a brief hiccup is not
  reported as a power cut. It holds times and whether the meter answered, never
  readings.

It does not store your name, your email or your location, and it keeps no
archive of your consumption beyond what is listed above.

Notifications are delivered through Apple's Push Notification service, which is
what carries them to your device.

## What we never do

- We do not sell, share or hand over your data to anybody.
- We do not use analytics, crash reporting, advertising or tracking of any kind.
- We do not build a profile of you or of your home.

## Removing your data

Sign out in the app. That erases, on the device, your Shelly session and the
credential the service issued; your tariff and your alert thresholds stay, since
they are your own work and you will want them if you come back.

It also tells the service to forget that device. When the last of your devices
signs out, everything belonging to your account is deleted there: the session,
the settings, the cached readings, the consumption figures, the warning history
and the record of what your meter was doing. Nothing is kept for later.

Deleting the app without signing out first leaves that data in the service. If
that is your case, write to the address below and it will be removed.

## How long it is kept

Only while you use the app. There is no archive: the warning history is capped
at the last hundred, the readings and the consumption figures are overwritten
each time, and signing out on your last device removes the rest.

## Contact

Questions about this policy: leinieralvarez@gmail.com

## About Shelly

Vatio is an independent application. It is not affiliated with, endorsed by or
sponsored by Shelly or Allterco Robotics.
