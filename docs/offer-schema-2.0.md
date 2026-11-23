# Offer config schema 2.0

Introduced with **PC Optimum Offers Platform Release 8.1** (deployed 2026-11-17), which moved audience targeting to **Audience Registry v2**.

## Breaking change
| | Legacy (1.x) | Current (2.0) |
|---|---|---|
| Schema marker | `"offerSchema": "1.x"` | `"offerSchema": "2.0"` |
| Audience reference | `audience.segmentId: "SEG-48213"` | `audience.registryRef: "aud://pco/seg/48213"` |
| Registry version | not present | `audience.registryVersion: 2` |

Registry v2 does **not** resolve legacy `segmentId` values. A legacy reference is treated as an empty set and Offer Studio logs:

    AUD-REG-404  Audience reference not found in registry v2 - treated as empty set

The publish is still allowed and the offer shows **Published**, but it has 0 eligible members, 0 impressions, and does not appear in the PC Optimum app "Offers for You" feed. Budget pacing shows $0 spend.

## Migration
1. Set `offerSchema` to `"2.0"`.
2. Replace `audience.segmentId: "SEG-<n>"` with `audience.registryRef: "aud://pco/seg/<n>"` (the numeric part is unchanged).
3. Add `audience.registryVersion: 2`.
4. Republish in Offer Studio and confirm Audience Preview shows eligible members > 0.

## Example
```json
"audience": {
  "registryRef": "aud://pco/seg/48213",
  "registryVersion": 2,
  "segmentName": "Colgate Oral & Personal Care Households",
  "memberTargeting": "PERSONALIZED"
}
```
