# Kayakomat booking desk

A dependency-free dashboard for operator login, booking retrieval, and client-side filtering.

Run it with any static server, for example:

```sh
python3 -m http.server 4173
```

Then open `http://localhost:4173`.

## API contract

The app calls `POST https://923vmokr87.execute-api.eu-central-1.amazonaws.com/production/authorization` with `{ email, password }`. It accepts the token as `token`, `accessToken`, `access_token`, `idToken`, or `id_token`; authentication errors are displayed to the user and never treated as a successful login.

After sign-in it calls `GET https://923vmokr87.execute-api.eu-central-1.amazonaws.com/production/admin/bookings?page=<page>&startTime=<YYYY-MM-DD>` with an `Authorization: <token>` header. Search, location, status, and end-date filters run in the browser; the start date is also sent to the API.

Set `window.KAYAKOMAT_BOOKINGS_ENDPOINT` or `window.KAYAKOMAT_AUTH_ENDPOINT` before loading `app.js` to override either endpoint. When the bookings API is unavailable, the interface presents clearly labelled demo data so the filtering flow remains usable.
