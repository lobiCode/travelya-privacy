# TravelYa Privacy Policy

**Effective date: 10 October 2026**

TravelYa is an offline-first trip planner for Android. It works without an account, has no
analytics, no advertising, and no servers operated by the developer. Your trips, places, photos and
notes are stored in the app's database **on your device** and never leave it unless a feature you
use explicitly sends a request to a third-party service, as described below.

_"The developer" means the individual who publishes TravelYa on Google Play
([contact](#contact-and-data-protection-requests))._

## 1. The short version

- TravelYa has **no accounts, no analytics, no ads and no tracking**. The developer does not
  operate any backend server and cannot see your trips, your searches or your location.
- Trips, waypoints, photos, checklists, visited history and settings are stored **only on your
  device**.
- Your **precise location** is used on-device to show you on the map and for navigation. It is
  never sent to the developer.
- When you use the **AI assistant**, your request and the relevant trip content are sent **directly
  from your phone to the AI provider you chose and configured** (z.ai, Google Gemini or OpenAI)
  using **your own API key**. The developer never sees the key or the request.
- **Place search** uses the free Photon geocoder (operated by Komoot) and map tiles come from
  OpenFreeMap; offline map data is downloaded from Geofabrik (OpenStreetMap data). Place images and
  descriptions are fetched from Wikipedia/Wikimedia.
- Nothing reaches the developer unless **you choose to email** feedback or an AI-content report
  from the app (section 6).
- You can delete everything at any time: delete trips in the app, remove API keys in settings, or
  uninstall the app.

## 2. Data stored only on your device

The following is kept in the app's local database and files, on your phone:

- Trips, their categories and places (names, descriptions, addresses, coordinates, opening hours,
  countries), checklists, AI-generated guides, and your visited-places history.
- Photos you attach to a place, and downloaded offline map regions.
- App settings: theme, language, and AI settings (chosen provider, model, output language).
- **Your AI API keys**, stored using Android's encrypted storage (Keystore-backed
  `EncryptedSharedPreferences`). They are only read to authenticate the requests you initiate and
  are never logged, exported or sent anywhere except to the provider they belong to.

None of this is transmitted by the app. Two platform caveats:

- **Android backup:** the app allows Android's automatic device backup. If you use it, Android may
  include your trips, places, checklists, visited history and settings in the backup of your Google
  account, or copy them in a direct phone-to-phone transfer. **Your AI API keys are never included**
  in either. Cloud backups also leave out offline maps, routing data, photos and attached documents
  (a direct transfer keeps photos and documents). Backup is a device feature you control in Android
  settings; the developer cannot access it.
- **Exported trip files (`.travelya`):** exporting or sharing a trip creates a file containing that
  trip's content. It goes only where you send it. Photos picked from your gallery are embedded for
  same-device restores; images originally downloaded from Wikimedia are represented by their public
  URL.

## 3. Location data

TravelYa requests the following location permissions:

- **Precise / approximate location** (`ACCESS_FINE_LOCATION`, `ACCESS_COARSE_LOCATION`): to show
  your position on the map, plan routes from where you are, and improve place-search results.
- **Foreground service** (types `location` and `dataSync`): the notification-visible service for
  navigation and for long-running AI trip-plan generation and map downloads.

TravelYa does **not** request background location access. A navigation session is started by you
while the app is open and runs as a foreground service with a clearly labelled ongoing
notification, so it keeps following your position when you switch apps or turn the screen off.
Location is only tracked while such a session is active and stops when you end it. When the map is
on screen, location updates stop shortly after you leave it or put the app in the background.

Your GPS position is **processed on your device only**. It is never transmitted to the developer
and is not shared with any advertising or analytics network. Coordinates of places (not your live
position) can leave the device as part of the features described in sections 4 and 5 — for example
a place you search for, or the content of a trip you ask the AI about.

You can deny or revoke any location permission in Android settings at any time; the features that
need it will degrade gracefully (search, map centre, navigation), while everything else keeps
working.

## 4. AI assistant — what is sent, and to whom

The AI features (trip planning, guides, place suggestions, chat about a trip) call **large language
model APIs directly from your phone**. There is no default provider: you pick one in settings and
enter **your own API key**. The supported providers are:

| Provider | Endpoint | Key from |
|---|---|---|
| z.ai (GLM Coding Plan) | `api.z.ai/api/coding/paas/v4` | z.ai |
| z.ai (pay-as-you-go) | `api.z.ai/api/paas/v4` | z.ai |
| Google Gemini | `generativelanguage.googleapis.com` | Google AI Studio |
| OpenAI | `api.openai.com` | OpenAI |

When you use an AI feature, the app sends to **that provider only**:

- your request (e.g. the destination, dates, interests or question you typed), and
- the trip content needed to answer it (trip, category and place names, descriptions, addresses,
  coordinates), and
- your API key, as the authentication header for that request.

If **web search** is enabled (it is on by default and can be turned off in settings), the provider
additionally runs web searches for you — through z.ai's Web Search service, Google Search
grounding (Gemini), or OpenAI's hosted web search, depending on the provider.

These requests are made over HTTPS, are billed to your own provider account, and are processed by
the provider under **their** privacy policy (links in section 9). The developer has no access to
your keys, your requests or the responses. Note that AI content can be inaccurate — verify
important details before you travel.

## 5. Other network requests

| Service | Operated by | What is sent | When |
|---|---|---|---|
| Photon geocoder (`photon.komoot.io`) | Komoot | The place name you search for, and optionally the coordinates of the map/trip area to rank results; or coordinates for a reverse lookup (finding an address for a point) | Place search, adding a place, fixing a wrong address, resolving a location shared into TravelYa |
| OpenFreeMap (`tiles.openfreemap.org`) | OpenFreeMap | Requests for the map tiles you view (tile coordinates; your IP is visible to any tile server) | Viewing the online map |
| Geofabrik (`download.geofabrik.de`) | Geofabrik | Download of the country/region file you pick | Downloading offline maps |
| Wikipedia / Wikimedia (`en.wikipedia.org`, `upload.wikimedia.org`) | Wikimedia Foundation | The title of the place an image/description is fetched for | Fetching place images and summaries |
| Link redirect resolution (`maps.app.goo.gl`) | Google | When you share a location link (e.g. from Google Maps) into TravelYa, the app opens the link to resolve it to coordinates | Resolving a shared location |

Requests to these services identify the app (name, version and a contact address) in their
User-Agent header, as their usage policies ask; they contain nothing about you.

None of these services receives your trips, your API keys or your name. Opening a place in Google
Maps or another external app hands over only what is in the link you tap.

## 6. Feedback and AI-content reports

Settings › About offers **Send feedback**, and every AI answer and AI screen has **Report AI
content**. Both open **your own email app** with a message addressed to the developer; nothing is
sent unless you press send there. Such an email contains:

- what you write, and for an AI-content report the reason you picked and the reported AI text;
- the app version, Android version and app language, to help reproduce problems;
- your email address and name as your email provider sends them.

The developer uses these emails only to answer you, fix problems and act on reported content, and
deletes them once they are no longer needed (at the latest two years after the last message).
You can ask for an email to be deleted at any time.

## 7. Permissions overview

| Permission | Why |
|---|---|
| Precise / approximate location | Show you on the map, routes from your position, better search results |
| Foreground service (location, data sync) | Navigation; AI plan generation and map downloads with a visible notification |
| Internet / network state | The requests described in sections 4 and 5 |
| Notifications | Progress of navigation, downloads and AI generation |

## 8. Data retention and deletion

- **On your device:** data is kept until you delete it. Delete individual trips in the app, remove
  API keys in AI settings, or delete downloaded offline maps. Uninstalling TravelYa removes all app
  data (unless it exists in an exported `.travelya` file or an Android backup you made).
- **At AI providers:** requests are handled under the provider's retention terms, controlled from
  your account with them. TravelYa cannot delete data held by providers.
- **Emails you send** (section 6) are kept only as long as needed to handle them.
- Apart from those emails, the developer keeps no user data, because none is ever sent to the
  developer.

## 9. Third-party privacy policies

- z.ai: <https://docs.z.ai/legal-agreement/privacy-policy>
- Google (Gemini API, Play services, backups): <https://policies.google.com/privacy>
- OpenAI: <https://openai.com/policies/privacy-policy>
- Komoot (Photon): <https://www.komoot.com/privacy>
- OpenFreeMap: <https://openfreemap.org/privacy/>
- Geofabrik: <https://www.geofabrik.de/geofabrik/imprint.html>
- Wikimedia Foundation: <https://foundation.wikimedia.org/wiki/Policy:Privacy_policy>

## 10. Children

TravelYa is not directed at children under 13, and we do not knowingly collect personal
information from children.

## 11. Changes to this policy

If the policy changes, the new version will be published at this URL with a new effective date.
Material changes will additionally be noted in app update notes.

## 12. Contact and data-protection requests

TravelYa stores your data only on your own device, so in almost every case you can exercise your
data rights directly in the app or by uninstalling it. For anything else, contact:

- Email: <travelya.app@gmail.com>
- Developer: Uroš Slana

Apart from emails you chose to send (section 6), no data reaches the developer, so requests that
concern data held by AI providers (section 4) must be directed to those providers through your
account with them.

Terms of use (liability, AI content, navigation): <https://lobicode.github.io/travelya-privacy/terms/>
