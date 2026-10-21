# travelya-privacy

Hosts the [TravelYa privacy policy](index.md) as a GitHub Pages site.

**Currently private on purpose.** GitHub Pages on the free plan only serves public
repositories, so the page goes live in two steps when TravelYa ships:

1. Repo → **Settings → General → Danger Zone → Change visibility → Public**
2. **Settings → Pages** → Deploy from a branch → `main` / `/ (root)` → Save

The public URL will then be: <https://lobicode.github.io/travelya-privacy/>
(terms of use at <https://lobicode.github.io/travelya-privacy/terms/>)

The privacy policy URL goes into Play Console → App content → Privacy policy.

## Updating the documents

The sources of truth are `docs/privacy-policy.md` and `docs/terms-of-use.md` in the private
`travelya` repo. After editing them there, mirror both here:

```bash
cp ../travelya/docs/privacy-policy.md index.md
{ printf -- '---\npermalink: /terms/\n---\n\n'; cat ../travelya/docs/terms-of-use.md; } > terms.md
git commit -am "Update legal documents"
git push
```

If the policy changes materially, also bump the effective date at the top of the
document and re-check that the Play Console **Data safety** form still matches
(section 4 and 5 of the policy are what the form is derived from).

## Help & tutorials page

`help/index.html` is a hand-written page (no Jekyll front matter, so it is served as-is) at
<https://lobicode.github.io/travelya-privacy/help/>, opened from the app (Settings → Help &
tutorials, and the empty trip list). Colors and radii are the app's Trail tokens.

To add a video, copy one `<a class="video">` block and change its link, thumbnail, duration, chip,
title and text. Store the thumbnail next to the page (`help/<name>.jpg`, 960×540) rather than
loading it from YouTube, so the page makes no third-party requests:

```bash
curl -o help/<name>.jpg https://i.ytimg.com/vi/<video-id>/maxresdefault.jpg
```

The page is content only: changing it never needs an app release.
