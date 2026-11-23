# pc-optimum-offer-config

Config-as-code for brand-funded **PC Optimum** offers published through Offer Studio on the Loblaw **Offers Platform**.

- `offers/` - one JSON per brand campaign (offerSchema, audience, rewards, funding, schedule)
- `docs/offer-schema-2.0.md` - the current contract (Offers Platform Release 8.1 / Audience Registry v2)

## Known issue (Release 8.1, Nov 17 2026)
Offer configs still on the legacy contract (`offerSchema: "1.x"`, `audience.segmentId`) are published without error but resolve to an **empty audience** - 0 eligible members, 0 impressions (publish log warning **AUD-REG-404**). Migrate to `offerSchema: "2.0"` with `audience.registryRef` + `audience.registryVersion: 2` and republish. See `docs/offer-schema-2.0.md`.

Status of campaign files: see each file's `offerSchema` value (`2.0` = migrated).
