# Vatio — Privacy Policy

_Last updated: 5 September 2026_

## Short version

Vatio does not collect anything about you, and nothing is shared with anyone.

By default everything stays on your device. Notifications that arrive while the
app is closed are the one exception: they need a small service that watches your
meter while your device sleeps, and this page explains exactly what that service
holds and why. On iPhone that service is required for notifications to work at
all; on Mac it is optional and only used if you ask for an alert history.

## On your device

Everything is kept inside the app's own container:

- **Your Shelly session.** When you sign in, Shelly's cloud returns an access
  token. The app never sees your Shelly password: you type it on Shelly's own
  page. Signing out removes the token.
- **Your settings.** The electricity tariff and the alerts you define. These are
  numbers you type; they never leave your Mac.

To show your consumption, the app talks only to the Shelly cloud
(`*.shelly.cloud`) over HTTPS, reading the devices in your own account. It never
controls or reconfigures anything.

## The watching service

A device that is asleep cannot notice that your power went out. iOS suspends
apps as a matter of course, and a Mac is closed or off much of the time. So a
small service runs in the cloud and checks your meter once a minute.

On iPhone it is what makes notifications possible. On Mac it is optional: the
app warns you on its own while it is open, and the service only adds a history
of what happened while the Mac was not.

For that, the service stores:

- **A Shelly session** (an access token and its refresh token), used only to
  read the consumption of your devices.
- **The alert thresholds** you configured, so it knows when to warn you.
- **The time zone of your device**, so a warning can say the hour you read on
  your own clock rather than the server's.
- **A push identifier**, which is what Apple needs to deliver a notification. It
  says nothing about you and is discarded as soon as Apple reports the app is no
  longer installed.
- **A credential it issues to each of your devices**, so they can read their own
  alerts and nobody else's. Only a hash of it is kept.
- **The last hundred warnings it sent you**, which is the alert history you see
  in the app. Each one holds the reading that triggered it and when.

It does not store your name, your email or your location, and it keeps no record
of your consumption beyond the last reading and those warnings.

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
the thresholds, the warning history and the record of what your meter was doing.
Nothing is kept for later.

Deleting the app without signing out first leaves that data in the service. If
that is your case, write to the address below and it will be removed.

## How long it is kept

Only while you use the app. There is no archive: the warning history is capped
at the last hundred, the readings are overwritten each time, and signing out on
your last device removes the rest.

## Contact

Questions about this policy: leinieralvarez@gmail.com

## About Shelly

Vatio is an independent application. It is not affiliated with, endorsed by or
sponsored by Shelly or Allterco Robotics.
