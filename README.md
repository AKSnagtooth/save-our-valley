# Save Our Valley — landing page

Static site, no build step. `index.html` + `support.js` + `image-slot.js`.
Deploys from `main` on Vercel (project: save-our-valley).

## Backend (Supabase project: save-our-valley, ref gialgfuhvzxcdrcwjrqn)
- Edge Function `send-letter` receives the form, stores the letter in `public.letters`, sends via Resend, posts a Lead event to Meta CAPI.
- Tables: `letters`, `alert_subscribers`, `settings` (recipients + test_mode).
- Function secrets to set in Dashboard → Edge Functions → Secrets:
  RESEND_API_KEY, FROM_EMAIL, TURNSTILE_SECRET, META_PIXEL_ID, META_CAPI_TOKEN, IP_SALT, ALLOWED_ORIGINS

## Go-live switch
`test_mode` in `settings` is `true`: letters go only to the sender. Flip to `false` to deliver to officials:
  update settings set value='false' where key='test_mode';

## Weekly readout
  select * from daily_summary(7);
