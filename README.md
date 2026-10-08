# travelya-privacy

Hosts the [TravelYa privacy policy](index.md) as a GitHub Pages site.

**Currently private on purpose.** GitHub Pages on the free plan only serves public
repositories, so the page goes live in two steps when TravelYa ships:

1. Repo → **Settings → General → Danger Zone → Change visibility → Public**
2. **Settings → Pages** → Deploy from a branch → `main` / `/ (root)` → Save

The public URL will then be: <https://lobicode.github.io/travelya-privacy/>

That URL goes into Play Console → App content → Privacy policy.

## Updating the policy

The source of truth is `docs/privacy-policy.md` in the private `travelya` repo.
After editing it there, mirror it here:

```bash
cp ../travelya/docs/privacy-policy.md index.md
git commit -am "Update privacy policy"
git push
```

If the policy changes materially, also bump the effective date at the top of the
document and re-check that the Play Console **Data safety** form still matches
(section 4 and 5 of the policy are what the form is derived from).
