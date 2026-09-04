# Vatio — Privacy Policy

_Last updated: 4 September 2026_

## Short version

Vatio does not collect anything about you, and nothing is shared with anyone.
The macOS app keeps everything on your Mac. The iPhone app needs one thing more
—a small service that watches your meter while your phone sleeps— and this page
explains exactly what that service holds and why.

## The macOS app

Everything stays on your Mac, inside the app's sandbox container:

- **Your Shelly session.** When you sign in, Shelly's cloud returns an access
  token. The app never sees your Shelly password: you type it on Shelly's own
  page. Signing out removes the token.
- **Your settings.** The electricity tariff and the alerts you define. These are
  numbers you type; they never leave your Mac.

The app talks only to the Shelly cloud (`*.shelly.cloud`) over HTTPS, to read
the devices in your own account.

## The iPhone app

iOS suspends apps when they are not in front of you, so an app alone cannot
notice that your power went out. To make those alerts work, a small service runs
in the cloud and checks your meter every minute.

For that to be possible, the service stores:

- **A Shelly session of its own** (an access token and its refresh token), used
  only to read the consumption of your devices. It cannot control or reconfigure
  anything.
- **The alert thresholds** you configured, to know when to warn you.
- **A push identifier for your device**, which is what Apple needs to deliver a
  notification. It says nothing about you and is deleted as soon as Apple
  reports that the app is no longer installed.

That service does not store your name, your email, your location or your usage
history. It keeps only the last reading, and only to tell whether something has
just changed.

## What we never do

- We do not sell, share or hand over your data to anybody.
- We do not use analytics, crash reporting, advertising or tracking of any kind.
- We do not build a profile of you or of your home.

## Removing your data

Sign out in the app and the stored session is deleted, on your device and in the
watching service. Delete the app and Apple stops delivering notifications; the
push identifier is then discarded automatically.

## Contact

Questions about this policy: leinieralvarez@gmail.com

## About Shelly

Vatio is an independent application. It is not affiliated with, endorsed by or
sponsored by Shelly or Allterco Robotics.
