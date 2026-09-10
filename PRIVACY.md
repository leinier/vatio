---
title: Privacy Policy
permalink: /privacy/
---

# Vatio — Privacy Policy

_Last updated: 10 September 2026_

## Short version

Vatio does not collect anything about you, and nothing is shared with anyone.

By default everything stays on your device. There are three exceptions, and this
page explains all of them: notifications that arrive while the app is closed need
a small service that watches your meter while your device sleeps; on iPhone that
same service also relays the app's own requests when your network cannot reach
Shelly; and your meter can send its readings to us directly, which is the only
case where we keep a history of your consumption.

If you use Vatio without a Shelly account, the third one is off until you turn
it on, and the app explains what it means before asking. If you sign in with a
Shelly account, Vatio sets it up for you the first time you open it at home,
because in that case your readings already travel to a cloud and this only
changes which one; the app says on its screen that your meter is sending to
Vatio, and one button undoes it and erases what was stored.

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

It does not store your name, your email or your location, and beyond what is
listed above it keeps no archive of your consumption — unless the readings
described in the next section are turned on, which is the one part of Vatio that
does.

Notifications are delivered through Apple's Push Notification service, which is
what carries them to your device.

## Readings sent straight to Vatio

This is the only part of Vatio that keeps a history of what your home consumes.
It exists because the manufacturer's cloud groups consumption by the hour and
publishes it late, so the figure for today can run up to an hour behind what
your meter already knows.

The app configures your own meter — on your own network, and only there — to use
the outbound connection built into the device, pointing it at our service. With
a Shelly account that happens by itself the first time you open Vatio at home;
without one it never happens unless you ask, because that mode promises nothing
leaves your house and turning this on quietly would make that a lie.

From then on the meter itself sends what it measures, without passing through
the manufacturer. Your meter has a single such connection: if it was already
sending somewhere else, the app tells you where and asks before taking it over.

What is stored, per meter:

- **One row per minute**, with the energy each of the three phases used in that
  minute, and the energy returned to the grid if you generate. This is the
  history you see in the app, and it is kept for as long as you use it.
- **The last reading it sent**, which is what the app shows as "now": power,
  current, voltage, power factor and frequency per phase, and the meter's own
  temperature.
- **Daily totals**, brought once from the Shelly cloud when this is set up, so
  your history does not start on the day it was turned on. Shelly gives day by
  day up to sixty days back; that is what is taken.
- **The credential we issued**, which is what your meter sends with every
  message, and which meter it belongs to.

Nothing else. No name, no email, no address, no location. The service knows a
meter, its numbers and nothing about who owns it — a meter never heard of your
Shelly account.

The readings are stored on Cloudflare, each meter in its own store, and are
never shared, sold or handed to anybody.

## What we never do

- We do not sell, share or hand over your data to anybody.
- We do not use analytics, crash reporting, advertising or tracking of any kind.
- We do not build a profile of you or of your home.

## Removing your data

There are two separate things you can remove, and they are separate on purpose.

**Signing out** ("Disconnect account") clears that device: your Shelly session
and the credentials the services issued. Your tariff and your alert thresholds
stay, since they are your own work and you will want them if you come back. It
also tells the watching service to forget that device; when the last of your
devices signs out, everything belonging to your account is deleted there — the
session, the settings, the cached readings, the consumption figures, the warning
history and the record of what your meter was doing.

Signing out on one device does **not** delete your consumption history. Many
people use Vatio on a phone and a computer, and taking the app off one of them
says nothing about the other: that history belongs to the meter, not to the
device you happened to press a button on.

**Deleting your data** ("Delete my data from Vatio", in Settings) is the one
that erases it: every minute stored, every daily total, and the credential. It
also tells your meter to stop sending, over the same connection it uses to send.
This reaches every device you use, and the app says so before doing it.

## How long it is kept

Your consumption history is kept while you are using it, and **deleted after
ninety days in which no device of yours has read it** — at which point your
meter is also told to stop sending. Any reading from any of your devices starts
that clock over, so having the app in two places does not shorten it.

That rule exists because uninstalling an app tells nobody. Neither iOS nor macOS
notifies a server when you remove an app, so a promise that depended on you
pressing a button first would be a promise we could not keep. This one does not
depend on you remembering anything.

Everything else has no archive at all: the warning history is capped at the last
hundred, the readings and the consumption figures are overwritten each time, and
signing out on your last device removes the rest.

## Contact

Questions about this policy: leinieralvarez@gmail.com

## About Shelly

Vatio is an independent application. It is not affiliated with, endorsed by or
sponsored by Shelly or Allterco Robotics.
