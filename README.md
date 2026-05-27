# Calendify
<a id="readme-top"></a>
<!-- PROJECT LOGO -->
<br />
<div align="center">
  <a href="https://github.com/tonyb650/calendify-app">
    <img src="./public/web-app-manifest-512x512.png" alt="Logo" width="80" height="80">
  </a>

  <h3 align="center">Calendify</h3>

  <p align="center">
    A full-stack calendar management app built with Next.js — scheduling, authentication, guest access, and experimental AI-assisted time-slot prediction in one workflow.
    <br />
  </p>
</div>


<!-- TABLE OF CONTENTS -->
<details>
  <summary>Table of Contents</summary>
  <ol>
    <li>
      <a href="#about-the-project">About The Project</a>
      <ul>
        <li><a href="#built-with">Built With</a></li>
      </ul>
    </li>
    <li>
      <a href="#getting-started">Getting Started</a>
      <ul>
        <li><a href="#prerequisites">Prerequisites</a></li>
        <li><a href="#installation">Installation</a></li>
      </ul>
    </li>
    <li><a href="#usage">Usage</a></li>
    <li><a href="#roadmap">Roadmap</a></li>
    <li><a href="#license">License</a></li>
    <li><a href="#contact">Contact</a></li>
    <li><a href="#acknowledgments">Acknowledgments</a></li>
  </ol>
</details>



<!-- ABOUT THE PROJECT -->
## About The Project

![Landing Page Screen Shot][landing-screenshot]

> **Collaboration:** Calendify is a joint project by **[Tony Brierly](https://linkedin.com/in/tony-brierly)** and **[Will Channing](https://www.linkedin.com/in/willchanning/)**.

Calendify is a full-stack calendar management app that combines scheduling, authentication, guest access, and account preferences into a single workflow. It pairs a polished calendar UI with a complete auth system (credentials + OAuth, email verification, and password reset) and supports a guest user flow for quick, no-signup access.

It also serves as a platform to experiment with AI-assisted scheduling: an experimental prediction action loads a TensorFlow.js model to suggest time slots. The companion training repo for that model lives at [calendify-ai](https://github.com/tonyb650/calendify-ai).

Core features include:
* User authentication with email/password and OAuth (GitHub, Google), email verification, and password reset
* Guest user flow with an authenticated cron endpoint that cleans up stale guest accounts
* Protected calendar area at `/calendar` with day, week, and month views
* Event data persisted in PostgreSQL via Prisma, with `Event` and `Part` (time-segment) models
* User preferences (`earliest` and `latest`) that feed scheduling logic
* Experimental TensorFlow.js prediction action for suggested time slots

<p align="right">(<a href="#readme-top">back to top</a>)</p>

### Built With
[![NextJS][Next.js]][NextJS-url]\
[![React][React.com]][React-url]\
[![TypeScript][TypeScript.com]][TypeScript-url]\
[![TailwindCSS][TailwindCSS.com]][Tailwind-url]\
[![Prisma][Prisma.com]][Prisma-url]\
[![PostgreSQL][PostgreSQL.com]][PostgreSQL-url]\
[![NextAuth][NextAuth.com]][NextAuth-url]\
[![TensorFlow][TensorFlow.com]][TensorFlow-url]


<p align="right">(<a href="#readme-top">back to top</a>)</p>



<!-- GETTING STARTED -->
## Getting Started

**NOTE**: *This is a personal project, but it is freely available if any part of it is useful to you.* To get a local copy up and running, follow these steps:

### Prerequisites

Node and NPM are required.
  ```sh
  npm install npm@latest -g
  ```

A reachable PostgreSQL database is also required.

### Installation
1. Clone the repo
   ```sh
   git clone https://github.com/tonyb650/calendify-app.git
   ```
2. Install packages with `npm`
   ```sh
   cd calendify-app && npm install
   ```
3. Create a `.env` file in the project root and populate the following variables:
   ```env
   DATABASE_URL="postgresql://USER:PASSWORD@HOST:PORT/DB_NAME?schema=public"

   AUTH_URL="http://localhost:3000"

   GITHUB_CLIENT_ID=""
   GITHUB_CLIENT_SECRET=""

   GOOGLE_CLIENT_ID=""
   GOOGLE_CLIENT_SECRET=""

   RESEND_API_KEY=""

   CRON_SECRET="replace-with-a-long-random-secret"
   ```
   - `DATABASE_URL` is required by Prisma.
   - `AUTH_URL` is used when generating verification/reset email links.
   - `CRON_SECRET` is required to authorize calls to `GET /api/cron`.
4. Change git remote url to avoid accidental pushes to base project
   ```sh
   git remote set-url origin github_username/repo_name
   git remote -v # confirm the changes
   ```
5. Prepare the database
   ```sh
   npx prisma migrate dev
   ```
   `prisma generate` also runs automatically during `postinstall`.
6. Run the application
   ```sh
   npm run dev
   ```
   Open [http://localhost:3000](http://localhost:3000).

<p align="right">(<a href="#readme-top">back to top</a>)</p>



<!-- USAGE EXAMPLES -->
## Usage

After signing in (or continuing as a guest), users land on the protected calendar area at `/calendar`, where events can be browsed in day, week, or month views and new events can be scheduled inline.

#### Register / Login

![Register Screen Shot][register-screenshot]

#### Daily View

![Daily View Screen Shot][daily-screenshot]

#### Weekly View

![Weekly View Screen Shot][weekly-screenshot]

#### Creating a New Event

![New Event Screen Shot][new-event-screenshot]

### Available Scripts

- `npm run dev` - Start the development server
- `npm run build` - Build for production
- `npm run start` - Start the production server
- `npm run lint` - Run ESLint

### Cron Cleanup Endpoint

- Endpoint: `GET /api/cron`
- Auth: `Authorization: Bearer <CRON_SECRET>`
- Purpose: Deletes guest users older than the configured cutoff in server logic.

Example:
```sh
curl -H "Authorization: Bearer $CRON_SECRET" http://localhost:3000/api/cron
```

### Deployment Notes

- The repository includes `vercel.json`, so Vercel deployment is expected.
- Set all required environment variables in your deployment platform.
- Ensure PostgreSQL is reachable from the deployment environment.
- If using the prediction feature in production, host the TensorFlow model files under `/public/models`.

<p align="right">(<a href="#readme-top">back to top</a>)</p>



<!-- ROADMAP -->
## Roadmap

- [ ] Harden the experimental TensorFlow.js prediction action for production use
- [ ] Expand scheduling logic around user preferences (`earliest` / `latest`)
- [ ] Additional calendar views and event-type customization
- [ ] Improved guest-to-registered-user conversion flow

<p align="right">(<a href="#readme-top">back to top</a>)</p>



<!-- LICENSE -->
## License

Distributed under the Unlicense License. See `LICENSE.txt` for more information.

<p align="right">(<a href="#readme-top">back to top</a>)</p>



<!-- CONTACT -->
## Contact

Calendify is built and maintained by:

**Tony Brierly**

[![LinkedIn][linkedin-shield]][linkedin-url]

**Will Channing**

[![LinkedIn][linkedin-shield]][will-linkedin-url]

Companion AI training repo: [calendify-ai](https://github.com/tonyb650/calendify-ai)

<p align="right">(<a href="#readme-top">back to top</a>)</p>



<!-- ACKNOWLEDGMENTS -->
## Acknowledgments

* [Next.js Documentation](https://nextjs.org/docs)
* [Auth.js (NextAuth v5) Documentation](https://authjs.dev/)
* [Prisma Documentation](https://www.prisma.io/docs)
* [FullCalendar](https://fullcalendar.io/)
* [shadcn/ui](https://ui.shadcn.com/)
* [Radix UI](https://www.radix-ui.com/)
* [Resend](https://resend.com/)
* [TensorFlow.js](https://www.tensorflow.org/js)
* [Best Readme Template](https://github.com/othneildrew/Best-README-Template)
* [Choose an Open Source License](https://choosealicense.com)
* [Img Shields](https://shields.io)

<p align="right">(<a href="#readme-top">back to top</a>)</p>



<!-- MARKDOWN LINKS & IMAGES -->
<!-- https://www.markdownguide.org/basic-syntax/#reference-style-links -->

[landing-screenshot]: README-assets/calendify_landing_screenshot.png
[register-screenshot]: README-assets/calendify_register_screenshot.png
[daily-screenshot]: README-assets/calendify_daily_screenshot.png
[weekly-screenshot]: README-assets/calendify_weekly_screenshot.png
[new-event-screenshot]: README-assets/calendify_new_event_screenshot.png

[linkedin-shield]: https://img.shields.io/badge/-LinkedIn-black.svg?style=for-the-badge&logo=linkedin&colorB=555
[linkedin-url]: https://linkedin.com/in/tony-brierly
[will-linkedin-url]: https://www.linkedin.com/in/willchanning/

[Next.js]: https://img.shields.io/badge/Nextjs-000000?style=for-the-badge&logo=next.js&logoColor=ffffff
[Nextjs-url]: https://nextjs.org/

[React.com]: https://img.shields.io/badge/react-%2320232a.svg?style=for-the-badge&logo=react&logoColor=%2361DAFB
[React-url]: https://react.dev/

[TypeScript.com]: https://img.shields.io/badge/TypeScript-3178c6?style=for-the-badge&logo=typescript&logoColor=ffffff
[TypeScript-url]: https://www.typescriptlang.org/

[TailwindCSS.com]: https://img.shields.io/badge/tailwindcss-041f30?style=for-the-badge&logo=tailwindcss&logoColor=00bcff
[Tailwind-url]: https://tailwindcss.com

[Prisma.com]: https://img.shields.io/badge/Prisma-2d3748?style=for-the-badge&logo=prisma&logoColor=ffffff
[Prisma-url]: https://www.prisma.io/

[PostgreSQL.com]: https://img.shields.io/badge/PostgreSQL-316192?style=for-the-badge&logo=postgresql&logoColor=ffffff
[PostgreSQL-url]: https://www.postgresql.org/

[NextAuth.com]: https://img.shields.io/badge/NextAuth.js-000000?style=for-the-badge&logo=nextdotjs&logoColor=ffffff
[NextAuth-url]: https://authjs.dev/

[TensorFlow.com]: https://img.shields.io/badge/TensorFlow.js-ff6f00?style=for-the-badge&logo=tensorflow&logoColor=ffffff
[TensorFlow-url]: https://www.tensorflow.org/js
