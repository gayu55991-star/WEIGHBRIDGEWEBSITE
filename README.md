# Point Digi Scale Website

Production Next.js website for Point Digi Scale.

## Local setup

1. Run `npm install`.
2. Copy `.env.example` to `.env.local` and add the Firebase Web app settings.
3. Run `npm run dev`.
4. Open `http://localhost:3000`.

## Firebase setup

1. Create a Firebase project and register a Web app.
2. In Authentication → Sign-in method, enable Email/Password. Add `localhost` and your deployed domain to the authorized domains.
3. In Authentication → Users, create `gayathrishanmugam813@gmail.com` (primary admin) and `info@yesyestechnologies.com` (secondary admin) with strong passwords. On first sign-in, the website sends a verification email; verify it and sign in again. Do not put passwords in source code or environment files.
4. Create a Cloud Firestore database and publish `firestore.rules` in Firestore → Rules.
5. Copy `.env.example` to `.env.local` and fill in the Firebase Web app config from Project settings → General.
6. Restart the development server. On the first admin sign-in, the website seeds the default models and gallery content into empty collections.

Firestore rules allow everyone to view models and gallery content, while only the two listed admin accounts can add, edit, or delete those records. Visitors can enquire and share without signing in. Gallery images are uploaded directly to ImageKit from the admin photo form; the server issues short-lived upload credentials only to the two verified admin accounts.

## ImageKit setup

1. Create a free ImageKit account and copy the public key from its dashboard.
2. Set `NEXT_PUBLIC_IMAGEKIT_PUBLIC_KEY` in `.env.local`.
3. Add the ImageKit private key as `IMAGEKIT_PRIVATE_KEY` in `.env.local`. Keep it server-only; never use a `NEXT_PUBLIC_` prefix or commit the value.
4. Add the same variables to the deployment provider's environment settings, including the private key, then restart/redeploy.
5. The free ImageKit plan has fixed storage and bandwidth limits. Check current usage and plan limits in the ImageKit dashboard.

The site seeds its built-in models and gallery content the first time a verified admin signs in to empty collections. Existing Supabase data is not transferred automatically.

## Images

The website background uses `public/images/img.png` with a soft blur and light overlay. The homepage hero uses `home.png.jpeg`, and the Point Digi Scale logo is `logo.png`. The Certificates gallery uses `img1.png.jpeg`, `img2.png.jpeg`, and `img3.png.jpeg` in `public/images/`.

- `logo.jpg`
- `install-1.jpg`
- `install-2.jpg`
- `certificate-1.jpg`

## Vercel

Import the project in Vercel and set the required `NEXT_PUBLIC_FIREBASE_*` variables, `NEXT_PUBLIC_IMAGEKIT_PUBLIC_KEY`, and the server-only `IMAGEKIT_PRIVATE_KEY`. Add the deployed domain to Firebase Authentication's authorized domains.
