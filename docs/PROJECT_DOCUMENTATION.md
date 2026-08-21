# Virtual Concept Technologies
# Project Development, Maintenance & Continuity Documentation

**Project:** Virtual Concept Technologies (VCT) Website  
**Production domain:** `virtualconcept.tech`  
**Repository:** `virtual-concept-technologies/virtual-concept-technologies`  
**Repository owner:** Virtual Concept Technologies GitHub organization  
**Primary branch:** `main`  
**Framework:** Astro  
**Astro version:** 7.2.4  
**Tailwind CSS:** 4.3.3  
**Node.js requirement:** >= 22.12.0  
**Hosting:** GitHub Pages  
**Deployment:** GitHub Actions  
**Website type:** Static, prerendered corporate/technology website  
**Current status:** Production  
**Document purpose:** Permanent technical, operational, maintenance, development, deployment, and continuity reference.

---

# 1. Purpose of This Document

This document is the permanent technical handover and continuity reference for the Virtual Concept Technologies website.

It exists so that a:

- product manager,
- developer,
- technical lead,
- designer,
- content editor,
- DevOps engineer,
- cybersecurity professional,
- AI coding agent,
- future maintainer,

can understand the project and continue development without needing to reconstruct the architecture from scratch or repeatedly ask the project owner where things are located.

The repository is the source of truth.

A future contributor should read this document before making substantial changes.

The goal is not merely to explain what the website looks like. The goal is to explain:

1. what the project is;
2. how it is structured;
3. where each responsibility lives;
4. how content flows through the application;
5. how the site is built;
6. how deployment works;
7. how the custom domain works;
8. how to make safe changes;
9. how to troubleshoot failures;
10. how to extend the project;
11. what should not be changed casually;
12. how an AI agent should reason about the repository.

---

# 2. Project Overview

Virtual Concept Technologies is a technology-focused corporate website.

The website communicates three primary areas of capability:

- Build
- Secure
- Enable

The site presents Virtual Concept Technologies as a provider of practical technology solutions spanning areas such as:

- artificial intelligence;
- digital solutions;
- cybersecurity;
- network security;
- technical training;
- AI skills;
- cybersecurity education;
- SOC-related training;
- software and SaaS concepts.

The website also contains:

- a corporate home page;
- an About page;
- Build service pages;
- Secure service pages;
- Enable service pages;
- a Products page;
- a Contact page.

The website is intentionally lightweight.

It is not a traditional backend application.

It does not currently depend on:

- a database;
- an application server;
- a server-side API;
- user authentication;
- a CMS;
- server-side rendering infrastructure.

The normal production process is:

    source code
        ↓
    Git repository
        ↓
    main branch
        ↓
    GitHub Actions
        ↓
    Astro build
        ↓
    dist/
        ↓
    GitHub Pages
        ↓
    virtualconcept.tech

---

# 3. Core Architectural Principle

## Repository is the source of truth

The Git repository is the authoritative source for the website.

Do not treat the GitHub Pages deployment as the place where permanent content or design changes should be made.

Permanent changes must be made in source code.

Correct:

    edit source
    test locally
    commit
    push
    GitHub Actions builds
    GitHub Pages deploys

Incorrect:

    change something only in a generated deployment
    assume the change is permanent

If a change cannot be reproduced from the repository, the project is not considered properly maintained.

---

# 4. Technology Stack

## 4.1 Astro

The website uses Astro.

Astro is responsible for:

- page routing;
- component rendering;
- static generation;
- page composition;
- dynamic route generation;
- build output.

The project currently uses Astro 7.2.4.

Astro pages use `.astro` files.

---

## 4.2 Tailwind CSS

The project uses Tailwind CSS 4.3.3.

Tailwind is integrated through the Vite plugin.

The global stylesheet contains:

    @import "tailwindcss";

Most visual styling is therefore implemented directly through Tailwind utility classes in Astro components and pages.

There is currently no traditional large custom CSS framework.

---

## 4.3 Node.js

The project requires:

    Node.js >= 22.12.0

GitHub Actions currently uses Node 22.

Local development should use a compatible Node 22 installation.

Do not downgrade the project to an older Node version without first checking Astro and dependency compatibility.

---

## 4.4 npm

Dependencies are managed through npm.

The standard dependency installation command is:

    npm ci

The project should retain its lockfile.

When dependencies are changed intentionally:

    npm install <package>

Then commit the resulting package manifest and lockfile changes.

For normal development from an existing checkout, prefer:

    npm ci

---

## 4.5 Git

Git is the project version-control system.

The primary branch is:

    main

The normal production workflow is based on commits pushed to `main`.

---

## 4.6 GitHub Actions

GitHub Actions builds and deploys the website.

The deployment workflow is:

    .github/workflows/deploy.yml

---

## 4.7 GitHub Pages

GitHub Pages hosts the generated static website.

The production custom domain is:

    virtualconcept.tech

The GitHub Pages deployment is configured to use a custom domain and HTTPS.

---

# 5. Repository Structure

The important repository structure is currently:

    .
    ├── .github/
    │   └── workflows/
    │       └── deploy.yml
    │
    ├── public/
    │
    ├── src/
    │   ├── components/
    │   │   ├── CapabilityCard.astro
    │   │   ├── Footer.astro
    │   │   ├── Header.astro
    │   │   └── SectionLabel.astro
    │   │
    │   ├── data/
    │   │   ├── build.ts
    │   │   ├── enable.ts
    │   │   └── secure.ts
    │   │
    │   ├── layouts/
    │   │   └── MainLayout.astro
    │   │
    │   ├── pages/
    │   │   ├── about/
    │   │   │   └── index.astro
    │   │   ├── build/
    │   │   │   ├── [slug].astro
    │   │   │   └── index.astro
    │   │   ├── contact/
    │   │   │   └── index.astro
    │   │   ├── enable/
    │   │   │   ├── [slug].astro
    │   │   │   └── index.astro
    │   │   ├── products/
    │   │   │   └── index.astro
    │   │   ├── secure/
    │   │   │   ├── [slug].astro
    │   │   │   └── index.astro
    │   │   └── index.astro
    │   │
    │   └── styles/
    │       └── global.css
    │
    ├── astro.config.mjs
    ├── package.json
    ├── package-lock.json
    ├── tsconfig.json
    └── docs/
        └── PROJECT_DOCUMENTATION.md

The exact repository may contain additional generated or configuration files. The structure above describes the application source that is relevant to normal development and maintenance.

---

# 6. Configuration Files

## 6.1 package.json

`package.json` defines the project identity, Node requirement, scripts, and dependencies.

Current scripts:

    npm run dev
    npm run build
    npm run preview
    npm run astro

Meaning:

### npm run dev

Starts the local Astro development server.

Use this while actively developing.

### npm run build

Builds the production website.

This is the most important local validation command before pushing significant changes.

### npm run preview

Previews the generated production build locally.

### npm run astro

Provides direct access to the Astro CLI.

---

# 7. Astro Configuration

The Astro configuration file is:

    astro.config.mjs

Current architecture:

    import { defineConfig } from 'astro/config';
    import tailwindcss from '@tailwindcss/vite';

    export default defineConfig({
      vite: {
        plugins: [tailwindcss()]
      }
    });

The important architectural point is that Tailwind CSS is integrated through Vite.

Do not introduce a second incompatible Tailwind configuration mechanism without understanding the existing setup.

---

# 8. TypeScript Configuration

The TypeScript configuration is:

    tsconfig.json

It extends:

    astro/tsconfigs/strict

The project therefore uses Astro's strict configuration.

When adding TypeScript code, avoid disabling strictness merely to make an error disappear.

A type error should normally be investigated and corrected.

---

# 9. Global Styling

The global stylesheet is:

    src/styles/global.css

Current global stylesheet:

    @import "tailwindcss";

This means Tailwind is globally available to the project.

Most styling is intentionally kept close to the markup through Tailwind classes.

When changing the overall visual language:

1. inspect the existing page;
2. inspect global CSS;
3. inspect shared components;
4. determine whether the change is global or page-specific;
5. avoid introducing unnecessary custom CSS.

---

# 10. Main Layout

The main site shell is:

    src/layouts/MainLayout.astro

This is one of the most important files in the project.

It provides:

- global CSS import;
- Header;
- page title;
- meta description;
- robots metadata;
- Open Graph metadata;
- page content slot;
- Footer.

Every normal page should use `MainLayout`.

The layout accepts:

    title
    description

Default values exist for both.

A page-specific title and description should normally be supplied by the page itself.

Example conceptual structure:

    <MainLayout
      title="..."
      description="..."
    >
      page content
    </MainLayout>

Do not duplicate the entire HTML document structure inside individual pages unless there is a compelling architectural reason.

---

# 11. Metadata and SEO

The main metadata system lives in:

    src/layouts/MainLayout.astro

It currently provides:

- HTML language declaration;
- viewport metadata;
- page title;
- meta description;
- robots directive;
- Open Graph title;
- Open Graph description;
- Open Graph type;
- Open Graph site name.

Individual pages supply their own title and description.

When creating a new page:

1. use `MainLayout`;
2. provide a meaningful title;
3. provide a meaningful description;
4. ensure the title describes the actual page;
5. avoid duplicate generic metadata.

SEO improvements should be made centrally where appropriate.

---

# 12. Header

The shared header is:

    src/components/Header.astro

It contains:

- Virtual Concept Technologies branding;
- main navigation;
- Build link;
- Secure link;
- Enable link;
- Products link;
- Start a Project action;
- mobile navigation button.

The header is shared through `MainLayout`.

Therefore a navigation change should normally be made in:

    src/components/Header.astro

Do not duplicate navigation into individual pages.

---

# 13. Footer

The shared footer is:

    src/components/Footer.astro

It contains:

- company branding;
- short company description;
- Explore links;
- Connect links;
- About;
- Start a Project;
- company contact information;
- copyright;
- company positioning text.

Because it is shared, changing the footer once changes it throughout the website.

Contact information should be kept consistent between:

- Contact page;
- Footer;
- mail links;
- other public references.

Current company email is:

    info@virtualconcept.tech

Do not reintroduce the previous personal Gmail address into production website content unless explicitly required by the project owner.

---

# 14. Reusable Components

## 14.1 CapabilityCard.astro

Location:

    src/components/CapabilityCard.astro

This component exists for reusable capability/card presentation.

Before creating a new card component, check whether `CapabilityCard.astro` can already represent the required content.

Avoid unnecessary duplicate components.

---

## 14.2 SectionLabel.astro

Location:

    src/components/SectionLabel.astro

This provides reusable section-label presentation.

Use the existing component where appropriate instead of creating multiple versions of the same visual pattern.

---

# 15. Home Page

The home page is:

    src/pages/index.astro

Its route is:

    /

The home page communicates the overall Virtual Concept Technologies proposition.

It contains sections associated with the site's main capability model:

- Build;
- Secure;
- Enable;
- products/digital solutions;
- calls to action.

The home page is the highest-level presentation of the company.

When changing the home page, preserve the distinction between:

- company positioning;
- capability areas;
- individual service detail;
- calls to action.

Do not turn the homepage into a complete copy of every service page.

---

# 16. Build Section

The Build section is located at:

    src/pages/build/

It contains:

    src/pages/build/index.astro
    src/pages/build/[slug].astro

The index page is the Build overview.

The `[slug].astro` page is the dynamic detail route.

Build content data is maintained in:

    src/data/build.ts

This separation is intentional.

The data file represents the content/data layer.

The dynamic page represents the presentation layer.

A future developer should therefore inspect `src/data/build.ts` before creating a new Build detail page.

If the existing data-driven architecture supports the new content, add the content to the data layer rather than creating a disconnected one-off page.

---

# 17. Secure Section

The Secure section is located at:

    src/pages/secure/

It contains:

    src/pages/secure/index.astro
    src/pages/secure/[slug].astro

Secure content data is maintained in:

    src/data/secure.ts

The same architectural principle applies:

    data/secure.ts
        ↓
    secure/[slug].astro
        ↓
    generated detail page

Security-related content should remain professionally accurate and should not make unsupported security claims.

---

# 18. Enable Section

The Enable section is located at:

    src/pages/enable/

It contains:

    src/pages/enable/index.astro
    src/pages/enable/[slug].astro

Enable content data is maintained in:

    src/data/enable.ts

This section is focused on enabling people and organizations through practical technology capabilities, training, AI skills, cybersecurity education, and related areas.

As with Build and Secure, inspect the data file before modifying the route architecture.

---

# 19. Dynamic `[slug]` Routes

The following routes use dynamic slugs:

    /build/[slug]
    /secure/[slug]
    /enable/[slug]

These pages should not be treated as independent unrelated pages.

They are part of a data-driven route architecture.

When adding a new capability:

1. inspect the relevant data file;
2. understand its object structure;
3. add the new service using the established structure;
4. ensure the slug is unique;
5. confirm the dynamic route can render it;
6. run a production build;
7. verify the resulting route.

Do not create duplicate route implementations unless the current data model cannot support the new requirement.

---

# 20. Products Page

The Products page is:

    src/pages/products/index.astro

Route:

    /products/

This page presents VCT products/SaaS-related positioning.

The Products page exists in the repository even though the primary header/navigation was intentionally simplified during the site's finishing work.

Before removing or restoring Products navigation, understand the current information architecture and business requirement.

Do not delete `src/pages/products/index.astro` merely because the Products link is not currently prominent in navigation.

A route can remain available without being part of the main navigation.

---

# 21. About Page

The About page is:

    src/pages/about/index.astro

Route:

    /about/

The About page has intentionally been designed around the company and the person behind it.

The page should not simply reproduce a full CV.

Its purpose is storytelling and professional positioning.

The intended structure is:

1. Virtual Concept Technologies context;
2. Enyinnaya Omeruah introduction;
3. professional identity;
4. relationship between professional experience and VCT;
5. areas of expertise;
6. professional journey;
7. appropriate personal/professional narrative;
8. LinkedIn call-to-action.

The page should communicate credibility without becoming an unnecessarily long CV document.

If the professional background changes, update the biography in a narrative manner.

Do not automatically paste a complete CV into the About page.

The reference style for the biography is an editorial "people/profile" style rather than a conventional résumé.

---

# 22. Contact Page

The Contact page is:

    src/pages/contact/index.astro

Route:

    /contact/

Its purpose is to provide a clear way for visitors to start a project or conversation with Virtual Concept Technologies.

The page contains contact-related information and a project/contact form interface.

The email destination should use:

    info@virtualconcept.tech

When changing contact information, search the entire source tree for old email addresses.

Useful command:

    grep -Rni "gmail.com" src public docs 2>/dev/null

A contact update is incomplete if the old address remains elsewhere in production-facing source.

---

# 23. Contact Form

The current website is a static site.

Therefore, the contact form must not be assumed to have a server-side submission system simply because an HTML form exists.

Before changing the form behavior, determine exactly how the current form submits information.

If a future implementation requires:

- database storage;
- email API;
- CRM integration;
- server-side validation;
- spam protection;
- authentication;

that represents an architectural expansion.

Do not introduce backend infrastructure casually.

Any new external service should be documented in this file after implementation.

---

# 24. Public Assets and Favicon

The `public/` directory contains static assets served directly by the generated website.

The previous Astro favicon assets were removed during the site's finishing work.

Current maintenance rule:

- do not reintroduce the default Astro favicon;
- if a VCT favicon is introduced later, it should be an intentional branded asset;
- update the layout/head configuration as necessary;
- verify the browser tab after deployment.

If a favicon is added, document:

1. filename;
2. format;
3. source;
4. dimensions;
5. where it is referenced;
6. whether it is generated or manually maintained.

---

# 25. Navigation Rules

The primary navigation is maintained in:

    src/components/Header.astro

The footer navigation is maintained in:

    src/components/Footer.astro

When adding a new top-level section:

1. determine whether it belongs in primary navigation;
2. update Header;
3. consider Footer;
4. create or verify the route;
5. update documentation;
6. test desktop navigation;
7. test mobile navigation;
8. verify production links.

Do not add navigation links to nonexistent routes.

Do not leave dead navigation links after removing a page.

---

# 26. Design System

The current design language is intentionally clean and professional.

Common visual characteristics include:

- white backgrounds;
- slate/dark typography;
- blue accent color;
- subtle borders;
- rounded cards;
- restrained shadows;
- generous spacing;
- responsive layouts;
- professional technology/corporate presentation.

The site should feel:

- credible;
- modern;
- technical;
- clean;
- practical;
- trustworthy.

Avoid introducing visual styles that conflict with the established language without a deliberate design decision.

---

# 27. Responsive Design

The site uses Tailwind responsive utility classes.

Typical responsive breakpoints appear directly in markup.

When changing layouts:

- test mobile;
- test tablet-sized layouts;
- test desktop;
- verify text wrapping;
- verify navigation;
- verify cards;
- verify buttons;
- verify spacing.

Do not assume a layout that looks correct at desktop width is automatically correct on mobile.

---

# 28. Content Architecture

The project separates reusable presentation from structured content in several places.

Important principle:

    shared UI → components/
    page structure → pages/
    service data → data/
    global shell → layouts/
    global styling → styles/

Do not place all content into one enormous file.

Do not create a new abstraction merely because two lines of markup look similar.

Use existing abstractions first.

---

# 29. How to Add a New Build Service

Suppose a new Build capability needs to be added.

Recommended process:

1. Open:

       src/data/build.ts

2. Understand the existing object structure.

3. Add the new service using the existing fields.

4. Give it a unique slug.

5. Confirm `src/pages/build/[slug].astro` can render the data.

6. Run:

       npm run build

7. Inspect generated routes.

8. Test the overview page.

9. Test the new detail URL.

10. Commit the change.

Do not immediately create a new page file if the existing dynamic architecture already supports the requirement.

---

# 30. How to Add a New Secure Service

Use the same process with:

    src/data/secure.ts

and:

    src/pages/secure/[slug].astro

Do not bypass the existing data-driven architecture without a documented reason.

---

# 31. How to Add a New Enable Service

Use:

    src/data/enable.ts

and:

    src/pages/enable/[slug].astro

Again, preserve the existing data-to-route architecture.

---

# 32. How to Add a New Top-Level Page

For a new top-level page:

    src/pages/example/index.astro

The resulting route will normally be:

    /example/

The page should:

1. import `MainLayout`;
2. define an appropriate title;
3. define an appropriate description;
4. use the established visual system;
5. include semantic headings;
6. work responsively;
7. be added to navigation only if required;
8. be tested locally;
9. be included in documentation if it changes the architecture.

---

# 33. Local Development

From the repository root:

    cd /workspaces/virtual-concept-technologies

Install dependencies:

    npm ci

Start development:

    npm run dev

Astro will provide a local development URL.

If the development server is already running and browser preview produces a stale or broken route, stop the development server and restart it.

HMR errors do not necessarily mean the production build is broken.

For a reliable production-style check:

    npm run build

Then:

    npm run preview

---

# 34. Local Build Validation

Before pushing substantial changes, run:

    npm run build

A successful build is one of the most important validation steps.

If the build fails:

1. read the first meaningful error;
2. identify the file;
3. inspect the surrounding code;
4. correct the underlying issue;
5. run the build again.

Do not repeatedly push failing builds hoping GitHub Actions will fix them.

---

# 35. Git Workflow

Before editing:

    git status

After editing:

    git status

Review changes:

    git diff

Stage only intended files:

    git add <file>

Commit with a meaningful message:

    git commit -m "Describe the change"

Push:

    git push origin main

Then verify:

    git status

Expected clean state:

    nothing to commit, working tree clean

---

# 36. Safe Change Procedure

Every meaningful website change should follow:

    1. Inspect
    2. Plan
    3. Edit
    4. Build
    5. Review diff
    6. Commit
    7. Push
    8. Verify Actions
    9. Verify production

Do not combine unrelated changes into one unclear commit when they can reasonably be separated.

---

# 37. Git Diff Is Mandatory for Significant Changes

Before committing a substantial modification:

    git diff

Look specifically for:

- accidental deletion;
- duplicated content;
- old email addresses;
- broken links;
- accidental placeholder text;
- malformed Astro syntax;
- unintended navigation changes;
- duplicated sections;
- incomplete heredoc output;
- unexpected files.

A clean build does not guarantee that the content is correct.

---

# 38. GitHub Actions Deployment

The deployment workflow is:

    .github/workflows/deploy.yml

The workflow is triggered by:

    push:
      branches:
        - main

It can also be triggered manually through:

    workflow_dispatch

The workflow has two jobs:

    build
    deploy

---

# 39. Build Job

The build job runs on:

    ubuntu-latest

It:

1. checks out the repository;
2. installs Node 22;
3. enables npm caching;
4. runs `npm ci`;
5. runs `npm run build`;
6. configures GitHub Pages;
7. uploads the `dist` directory as the Pages artifact.

The artifact path is:

    ./dist

This is the generated static website.

---

# 40. Deploy Job

The deploy job waits for the build job.

It uses the GitHub Pages deployment action.

The deployment environment is:

    github-pages

The deployment URL is obtained from the deployment step.

If the build job fails, the deployment job does not proceed.

---

# 41. GitHub Actions Permissions

The workflow requires:

    contents: read
    pages: write
    id-token: write

These permissions are necessary for the Pages deployment architecture.

Do not remove them casually.

If deployment architecture changes, review the permissions against the official GitHub Pages deployment requirements.

---

# 42. Workflow Concurrency

The workflow uses:

    group: pages
    cancel-in-progress: true

This means a newer Pages deployment can supersede an older in-progress deployment.

This is intentional and helps prevent unnecessary competing deployments.

---

# 43. Deployment Verification

After pushing to `main`:

    gh run list --repo virtual-concept-technologies/virtual-concept-technologies --limit 5

A successful run should show a successful status.

If a run fails:

    gh run view <RUN_ID> --repo virtual-concept-technologies/virtual-concept-technologies --log-failed

Use the failed step to identify the cause.

Do not assume a failed deployment is a DNS problem.

First determine whether:

- dependency installation failed;
- Astro compilation failed;
- TypeScript failed;
- a page failed;
- artifact generation failed;
- Pages deployment failed.

---

# 44. GitHub Pages Configuration

The Pages configuration is associated with the repository's Pages settings.

The production custom domain is:

    virtualconcept.tech

The site is configured for HTTPS.

The GitHub Pages API can be inspected with:

    gh api repos/virtual-concept-technologies/virtual-concept-technologies/pages

Important fields include:

- `cname`;
- `build_type`;
- `source`;
- `protected_domain_state`;
- `https_certificate`;
- `https_enforced`.

---

# 45. Custom Domain

The custom domain is:

    virtualconcept.tech

The domain has been verified.

The Pages configuration reports the custom domain as the site's CNAME.

The production site has successfully returned HTTP 200 over HTTPS.

A previous certificate transition showed a state indicating that DNS had changed and GitHub was requesting a new certificate.

That state can occur during certificate provisioning or renewal.

Do not repeatedly change DNS records merely because the Pages API temporarily reports a certificate transition state.

If:

    curl -I https://virtualconcept.tech/

returns:

    HTTP/2 200

the production site is serving successfully.

---

# 46. HTTPS

HTTPS is enforced for the production site.

The primary production URL should therefore use HTTPS.

Do not disable HTTPS merely to resolve a temporary certificate provisioning issue.

Certificate state should be checked through GitHub Pages when troubleshooting.

---

# 47. www Domain

The `www` hostname has previously resolved toward GitHub Pages infrastructure but experienced a certificate mismatch while the apex custom domain was correctly serving.

The canonical production domain is:

    virtualconcept.tech

If `www.virtualconcept.tech` is required in the future, configure it deliberately.

A future maintainer should verify:

1. DNS;
2. GitHub Pages custom-domain configuration;
3. certificate coverage;
4. redirect behavior;
5. canonical URL behavior.

Do not assume that adding a DNS record alone completes `www` configuration.

---

# 48. DNS Troubleshooting

If the site stops resolving:

1. check the domain's DNS records;
2. check GitHub Pages custom-domain configuration;
3. check certificate status;
4. test DNS resolution;
5. test HTTP;
6. test HTTPS.

Useful commands:

    getent hosts virtualconcept.tech

and:

    curl -I https://virtualconcept.tech/

If DNS has changed recently, certificate provisioning may take time.

Do not make repeated DNS changes without understanding the current record configuration.

---

# 49. Production Verification

After a successful deployment, verify:

    curl -I https://virtualconcept.tech/

A healthy response should normally include:

    HTTP/2 200

Then test important routes in a browser:

    /
    /about/
    /build/
    /secure/
    /enable/
    /products/
    /contact/

Also test at least one dynamic detail route from each of:

    /build/<slug>/
    /secure/<slug>/
    /enable/<slug>/

using the actual currently defined slugs.

---

# 50. Browser Cache Considerations

The website is served through GitHub Pages and CDN infrastructure.

Therefore, after a deployment:

- browser caching may temporarily show an older version;
- CDN caching may affect immediate visual verification;
- a hard refresh can help;
- checking the response headers can help distinguish deployment problems from caching.

Do not immediately revert a deployment solely because one browser still displays old content.

First verify the deployed HTML and GitHub Actions result.

---

# 51. Error: Astro HMR / Router

During local development an error such as:

    Failed to update routes via HMR:
    TypeError: undefined is not a function

may occur.

This is a development-server/HMR issue unless a production build also fails.

Recommended response:

1. stop the dev server;
2. restart it;
3. run `npm run build`;
4. if the build succeeds, inspect the browser again;
5. if the build fails, fix the actual build error.

Do not treat HMR output alone as proof that production deployment is broken.

---

# 52. Error: Codespaces Browser 404

A GitHub Codespaces preview URL can return HTTP 404 even when the production website works.

First determine whether:

- Astro dev server is running;
- the expected port is exposed;
- the browser is using the current forwarded port;
- the local development server is listening on the expected interface;
- the route exists.

Do not confuse a Codespaces preview URL with the production GitHub Pages URL.

The production source of truth remains the deployed website.

---

# 53. Error: GitHub Actions Failure

If:

    gh run list

shows a failed workflow:

1. obtain the run ID;
2. inspect the failed logs;
3. identify the first meaningful failure;
4. reproduce locally where possible;
5. fix the source;
6. run `npm run build`;
7. commit;
8. push.

Useful command:

    gh run view <RUN_ID> --repo virtual-concept-technologies/virtual-concept-technologies --log-failed

---

# 54. Dependency Maintenance

Do not upgrade Astro, Tailwind, Node, or other dependencies simply because a newer version exists.

Before an upgrade:

1. determine why the upgrade is needed;
2. inspect breaking changes;
3. update dependencies;
4. run npm installation;
5. run the production build;
6. inspect warnings;
7. test all major routes;
8. inspect the Git diff;
9. deploy only after validation.

Dependency upgrades should preferably be isolated from unrelated content/design changes.

---

# 55. Adding External Services

The current architecture is intentionally simple.

If future work introduces:

- email services;
- analytics;
- CRM;
- payment systems;
- databases;
- authentication;
- APIs;
- cloud functions;
- external forms;
- monitoring;

the new dependency must be documented.

At minimum document:

- service name;
- purpose;
- environment variables;
- credentials location;
- development behavior;
- production behavior;
- failure behavior;
- ownership;
- renewal requirements;
- security implications.

Never commit secrets into the repository.

---

# 56. Secrets

Never put any of the following into source code:

- passwords;
- API keys;
- private tokens;
- secret credentials;
- private certificates;
- access tokens.

Use appropriate secret-management facilities if the project later requires secrets.

The current static website should not need secrets for ordinary page rendering.

---

# 57. Security Maintenance

The website itself is static, which reduces the attack surface compared with a traditional server application.

Nevertheless, maintain:

- dependency security;
- external-link safety;
- form security;
- third-party integration security;
- GitHub Actions permissions;
- repository access controls;
- domain security;
- HTTPS.

Do not add JavaScript or third-party libraries merely for convenience when the requirement can be fulfilled with existing HTML/Astro capabilities.

---

# 58. Content Maintenance

When changing company copy:

1. identify the page responsible;
2. update only the relevant content;
3. preserve semantic structure;
4. preserve SEO metadata;
5. check desktop and mobile presentation;
6. build;
7. review;
8. deploy.

Avoid changing architecture for a copy-only update.

---

# 59. Biography Maintenance

The About page should evolve as a professional biography, not as a pasted CV.

When professional information changes:

- update the narrative;
- update relevant expertise;
- update professional journey where appropriate;
- maintain factual accuracy;
- avoid unnecessary repetition;
- keep the page focused on the relationship between professional experience and Virtual Concept Technologies.

The LinkedIn profile is an important external professional reference.

Keep its link correct if the profile URL changes.

---

# 60. Product Content Maintenance

Products and SaaS content should accurately represent the current maturity of each product.

Do not present:

- prototypes as finished products;
- planned functionality as existing functionality;
- concepts as commercially deployed systems.

Use language such as:

- concept;
- in development;
- prototype;
- beta;
- available;
- production;

only when it accurately reflects the product's actual status.

---

# 61. Accessibility

When modifying pages:

- use semantic headings;
- maintain logical heading order;
- provide meaningful link text;
- provide accessible labels for buttons;
- preserve keyboard usability;
- ensure sufficient color contrast;
- avoid relying solely on color;
- maintain useful mobile layouts.

Do not remove accessibility attributes from shared components without a clear reason.

---

# 62. Performance

The current architecture is favorable for performance because the site is statically generated.

When improving performance:

- avoid unnecessary JavaScript;
- optimize large images;
- avoid unnecessary dependencies;
- avoid large client-side frameworks;
- preserve static generation where possible;
- keep pages focused.

Do not introduce a client-side application architecture simply to implement a small interactive feature.

---

# 63. AI Coding Agent Instructions

Any AI coding agent working on this repository must follow these rules.

## Rule 1: Inspect before editing

Before changing a file, inspect it.

Do not guess its contents.

---

## Rule 2: Follow the existing architecture

Use:

    components/
    data/
    layouts/
    pages/
    styles/

according to their existing responsibilities.

Do not introduce unnecessary architecture.

---

## Rule 3: Search before changing global content

For a company-wide change such as an email address, search the repository.

Example:

    grep -Rni "old-address" src public docs 2>/dev/null

---

## Rule 4: Do not duplicate existing abstractions

Before creating a component, inspect:

    src/components/

Before creating a new service route, inspect:

    src/data/
    src/pages/build/
    src/pages/secure/
    src/pages/enable/

---

## Rule 5: Do not overwrite files blindly

Never use a large heredoc replacement unless the complete intended file content is known and intentionally being replaced.

Prefer targeted editing for normal maintenance.

---

## Rule 6: Never leave placeholders

Do not leave:

    TODO

or:

    [DOCUMENTATION CONTENT]

or:

    lorem ipsum

or incomplete generated sections in production files.

---

## Rule 7: Build before declaring completion

Run:

    npm run build

before considering a substantial code change complete.

---

## Rule 8: Review the diff

Run:

    git diff

before committing.

---

## Rule 9: Verify deployment

After pushing:

    gh run list --repo virtual-concept-technologies/virtual-concept-technologies --limit 5

Then verify production.

---

## Rule 10: Do not ask irrelevant questions

A future AI agent should first inspect:

- repository structure;
- relevant page;
- relevant component;
- relevant data file;
- package configuration;
- deployment workflow;
- existing documentation.

Only ask the project owner when required information genuinely does not exist in the repository or documentation.

---

# 64. AI Agent Decision Tree

When asked to modify the website:

### If the request concerns global navigation

Inspect:

    src/components/Header.astro
    src/components/Footer.astro

### If the request concerns page shell or SEO

Inspect:

    src/layouts/MainLayout.astro

### If the request concerns global styling

Inspect:

    src/styles/global.css
    astro.config.mjs

### If the request concerns Build services

Inspect:

    src/data/build.ts
    src/pages/build/index.astro
    src/pages/build/[slug].astro

### If the request concerns Secure services

Inspect:

    src/data/secure.ts
    src/pages/secure/index.astro
    src/pages/secure/[slug].astro

### If the request concerns Enable services

Inspect:

    src/data/enable.ts
    src/pages/enable/index.astro
    src/pages/enable/[slug].astro

### If the request concerns the company biography

Inspect:

    src/pages/about/index.astro

### If the request concerns contact information

Inspect:

    src/pages/contact/index.astro
    src/components/Footer.astro

### If the request concerns deployment

Inspect:

    .github/workflows/deploy.yml

### If the request concerns dependencies

Inspect:

    package.json
    package-lock.json

### If the request concerns DNS or HTTPS

Inspect GitHub Pages configuration and DNS rather than modifying Astro source code.

---

# 65. What Not to Change Casually

Do not casually change:

- Node major version;
- Astro version;
- Tailwind version;
- GitHub Actions workflow;
- Pages permissions;
- deployment artifact path;
- custom domain;
- HTTPS settings;
- route architecture;
- dynamic slug architecture;
- shared layout;
- navigation structure;
- package dependencies.

These are infrastructure or architectural concerns.

A visual change should not accidentally become an infrastructure change.

---

# 66. What Can Normally Be Changed Safely

Normal low-risk changes include:

- page copy;
- headings;
- descriptions;
- service descriptions;
- biography wording;
- button labels;
- footer wording;
- contact information;
- service data;
- minor Tailwind styling adjustments.

Even low-risk changes should still be built and reviewed.

---

# 67. Adding a New Dependency

Before adding a dependency ask:

1. Is it actually necessary?
2. Can Astro solve the problem?
3. Can existing browser APIs solve it?
4. Can existing Tailwind/Astro functionality solve it?
5. What does it add to bundle size?
6. Does it introduce a security concern?
7. Does it require maintenance?
8. Does it work with Node 22?
9. Does it work with the current Astro version?

If the dependency is justified:

    npm install <package>

Then:

    npm run build

Review:

    git diff package.json package-lock.json

---

# 68. Testing Checklist

Before production deployment, check:

## Build

    npm run build

must succeed.

## Routes

Verify:

    /
    /about/
    /build/
    /secure/
    /enable/
    /products/
    /contact/

Also verify representative dynamic routes.

## Navigation

Verify:

- Build;
- Secure;
- Enable;
- relevant active calls-to-action;
- About;
- Contact.

## Contact

Verify:

- email;
- contact links;
- form;
- project categories.

## About

Verify:

- company story;
- Enyinnaya biography;
- professional positioning;
- LinkedIn button.

## Branding

Verify:

- Virtual Concept Technologies;
- no obsolete personal email;
- no default Astro favicon;
- no accidental placeholder content.

## Responsive

Verify:

- mobile;
- tablet;
- desktop.

---

# 69. Production Deployment Checklist

Before pushing:

    git status
    git diff
    npm run build

Then:

    git add <intended files>
    git commit -m "Describe change"
    git push origin main

Then:

    gh run list --repo virtual-concept-technologies/virtual-concept-technologies --limit 5

Wait for the latest run to succeed.

Then verify production.

---

# 70. Rollback Procedure

If a deployment introduces a serious problem:

1. identify the last known good commit;
2. inspect Git history;
3. determine whether a revert is appropriate;
4. revert the problematic commit;
5. build locally;
6. push the corrective commit;
7. verify GitHub Actions;
8. verify production.

Useful commands:

    git log --oneline --decorate -20

and:

    git show <COMMIT>

A rollback should normally be performed through Git history rather than manually editing the deployed GitHub Pages artifact.

---

# 71. Recovery From a Broken Working Tree

If local changes are accidental and have not been committed:

First inspect:

    git status

Then inspect:

    git diff

If a specific unwanted file needs to be restored:

    git restore <file>

Do not use broad destructive Git commands unless you understand exactly what will be discarded.

---

# 72. Documentation Maintenance

This document must evolve with the project.

Update it when:

- architecture changes;
- dependencies materially change;
- deployment changes;
- DNS changes;
- a backend is introduced;
- an external service is introduced;
- a new major route is introduced;
- a new integration is introduced;
- authentication is introduced;
- product architecture changes.

Do not update documentation merely to describe routine text edits.

---

# 73. Documentation Location

This document lives at:

    docs/PROJECT_DOCUMENTATION.md

It belongs in the repository.

It should remain version controlled.

It should be updated through normal Git commits.

---

# 74. Documentation Quality Standard

A future maintainer should be able to answer these questions from the repository and this document:

- What is this project?
- Where is the source?
- What framework does it use?
- What Node version is required?
- How do I start it?
- How do I build it?
- Where is navigation?
- Where is the global layout?
- Where is the footer?
- Where are service definitions?
- How do dynamic routes work?
- Where is the About page?
- Where is contact information?
- How does deployment work?
- What triggers deployment?
- Where does GitHub Pages get its artifact?
- What is the production domain?
- How is HTTPS configured?
- How do I inspect a failed deployment?
- How do I add a new service?
- How do I add a new page?
- How do I update the biography?
- How do I update the email address?
- How do I safely modify the site?
- How does an AI agent know where to begin?

If these questions cannot be answered, this document should be improved.

---

# 75. Current Project Baseline

The current known baseline is:

    Framework:
        Astro 7.2.4

    Styling:
        Tailwind CSS 4.3.3

    Node:
        >= 22.12.0

    Build:
        npm run build

    Development:
        npm run dev

    Preview:
        npm run preview

    Hosting:
        GitHub Pages

    Deployment:
        GitHub Actions

    Production branch:
        main

    Production domain:
        virtualconcept.tech

    Primary layout:
        src/layouts/MainLayout.astro

    Header:
        src/components/Header.astro

    Footer:
        src/components/Footer.astro

    Global CSS:
        src/styles/global.css

    Build data:
        src/data/build.ts

    Secure data:
        src/data/secure.ts

    Enable data:
        src/data/enable.ts

    Deployment workflow:
        .github/workflows/deploy.yml

---

# 76. Current Business Information Architecture

The website should be understood as four layers.

## Layer 1 — Company

Virtual Concept Technologies.

This is the organizational identity.

## Layer 2 — Capabilities

    Build
    Secure
    Enable

These are the primary capability categories.

## Layer 3 — Services

Individual service/capability pages are represented through the relevant data files and dynamic slug routes.

## Layer 4 — Conversion

Visitors can move toward:

    Start a Project
    Contact
    LinkedIn
    relevant service information

Future development should preserve this information hierarchy unless a deliberate business strategy changes it.

---

# 77. Product Manager Guidance

A product manager should distinguish between:

### Content request

Example:

    "Change the About page wording."

Usually affects:

    src/pages/about/index.astro

### Service request

Example:

    "Add a new cybersecurity service."

Usually affects:

    src/data/secure.ts

and possibly the overview page.

### Navigation request

Example:

    "Add a new item to the top navigation."

Affects:

    src/components/Header.astro

### Infrastructure request

Example:

    "Change the production domain."

This is not simply an Astro page edit.

It requires GitHub Pages and DNS consideration.

### Platform request

Example:

    "Add user accounts."

This is an architectural change and requires a design review before implementation.

---

# 78. Developer Guidance

A developer should begin work by:

    cd /workspaces/virtual-concept-technologies
    git status
    git pull origin main

Then inspect the relevant files.

Before committing:

    npm run build
    git diff
    git status

After pushing:

    gh run list --repo virtual-concept-technologies/virtual-concept-technologies --limit 5

---

# 79. AI Agent Handover Protocol

An AI agent receiving a request should use this sequence:

### Step 1

Read:

    docs/PROJECT_DOCUMENTATION.md

### Step 2

Run:

    git status

### Step 3

Inspect the relevant files.

### Step 4

Search for existing implementations before creating new ones.

### Step 5

Make the smallest architectural change that satisfies the requirement.

### Step 6

Run:

    npm run build

### Step 7

Review:

    git diff

### Step 8

Report exactly what changed.

### Step 9

Commit only intended files.

### Step 10

Push only when authorized/required.

### Step 11

Verify GitHub Actions.

### Step 12

Verify production.

An AI agent should not ask the owner basic repository questions that can be answered by inspection.

---

# 80. Continuous Improvement Strategy

Future improvements should be prioritized in this order:

## 1. Correctness

The website must work.

## 2. Security

Dependencies, integrations, forms, domain, and deployment must remain secure.

## 3. Performance

Keep the static architecture lightweight.

## 4. Accessibility

Ensure the website remains usable by a broad audience.

## 5. SEO

Improve metadata, semantic structure, discoverability, and sharing.

## 6. Content

Improve clarity and business communication.

## 7. UX

Improve navigation, conversion, and user journeys.

## 8. Visual refinement

Improve design without sacrificing clarity.

## 9. New functionality

Only introduce new functionality when there is a clear business or user need.

---

# 81. Future Architectural Expansion

If the website eventually requires:

- user dashboards;
- authentication;
- subscriptions;
- payments;
- customer portals;
- persistent user data;
- interactive laboratories;
- account management;
- API-driven applications;

do not attempt to force these features into the current static architecture without analysis.

The current website should remain the lightweight corporate/public layer unless the product strategy explicitly changes.

A future architecture may involve separate applications or services while retaining this website as the public corporate site.

---

# 82. Change Classification

Every proposed change should be classified before implementation.

### Class A — Content

Low architectural risk.

Examples:

- text;
- headings;
- descriptions;
- biography;
- contact details.

### Class B — Presentation

Moderate risk.

Examples:

- spacing;
- typography;
- colors;
- layout;
- cards.

### Class C — Navigation

Moderate risk.

Examples:

- adding/removing links;
- changing information architecture.

### Class D — Application Architecture

High risk.

Examples:

- changing routing;
- introducing client-side applications;
- changing data architecture.

### Class E — Infrastructure

High risk.

Examples:

- GitHub Actions;
- Pages;
- DNS;
- Node version;
- deployment architecture.

### Class F — Security

High risk.

Examples:

- authentication;
- secrets;
- APIs;
- forms;
- external integrations.

High-risk changes require greater validation and documentation.

---

# 83. Final Continuity Rules

The following rules are permanent project principles unless intentionally superseded.

1. The Git repository is the source of truth.

2. `main` is the production branch.

3. Production deployment is handled by GitHub Actions.

4. GitHub Pages serves the generated static site.

5. The production domain is `virtualconcept.tech`.

6. Astro is the website framework.

7. Tailwind CSS is the primary styling system.

8. `MainLayout.astro` is the shared page shell.

9. `Header.astro` owns primary navigation.

10. `Footer.astro` owns shared footer content.

11. Build, Secure, and Enable service content should use their existing data-driven architecture.

12. The About page should remain a professional narrative, not a pasted full CV.

13. Contact information must remain consistent throughout the site.

14. The default Astro favicon must not be reintroduced unintentionally.

15. Do not introduce unnecessary dependencies.

16. Do not introduce backend architecture without an explicit requirement.

17. Never commit secrets.

18. Build before deploying.

19. Review the Git diff before committing.

20. Verify GitHub Actions after deployment.

21. Verify the production website after deployment.

22. Update this documentation when architecture or operational behavior changes.

23. Prefer small, understandable changes over unnecessary rewrites.

24. Future AI agents must inspect the existing implementation before asking questions or creating new architecture.

25. If an existing component, data model, route, or layout already solves the problem, use it.

26. Never replace a complete project file with partial or placeholder content.

27. Never consider a task complete merely because the code was edited; validate the build and the deployed result.

---

# 84. Definition of Done

A website change is considered complete only when:

    [ ] Requirement understood
    [ ] Relevant source files inspected
    [ ] Existing architecture reused where appropriate
    [ ] Change implemented
    [ ] No obsolete content remains
    [ ] npm run build succeeds
    [ ] git diff reviewed
    [ ] Intended files committed
    [ ] main updated
    [ ] GitHub Actions succeeds
    [ ] Production website verified
    [ ] Documentation updated if architecture changed

This is the project's operational definition of done.

---

# 85. Final Statement

Virtual Concept Technologies is currently implemented as a deliberately lightweight Astro static website deployed through GitHub Pages.

The architecture is intentionally straightforward:

    Astro
      +
    Tailwind CSS
      +
    Git
      +
    GitHub Actions
      +
    GitHub Pages
      +
    virtualconcept.tech

The project should remain simple unless a genuine business or technical requirement justifies additional complexity.

The most important maintenance principle is:

**Understand the existing architecture before changing it.**

The second is:

**Keep the repository, deployment process, and documentation synchronized.**

The third is:

**Every future developer or AI agent should be able to continue the project from this document without depending on undocumented knowledge held by one person.**

This document is therefore part of the project itself, not an optional note.

---

# 86. Project Continuity Ledger

This section preserves the practical project context needed to continue development across future sessions, developers, or AI-assisted development environments.

It complements Git history and the rest of this documentation. It does not replace the repository as the source of truth.

## 86.1 Current Operational State

The current project is:

- **Project:** Virtual Concept Technologies website
- **Production domain:** `virtualconcept.tech`
- **Repository:** `virtual-concept-technologies/virtual-concept-technologies`
- **Primary branch:** `main`
- **Framework:** Astro
- **Styling:** Tailwind CSS
- **Runtime requirement:** Node.js 22.12.0 or newer
- **Hosting:** GitHub Pages
- **Deployment:** GitHub Actions
- **Development environment:** GitHub Codespaces
- **Site architecture:** Static/prerendered
- **Database:** None
- **Traditional application server:** None

The repository is the authoritative source of the website.

## 86.2 Current Website Areas

The current site contains:

- Home
- About
- Build
- Secure
- Enable
- Products
- Contact

The Build, Secure, and Enable sections use data-driven service structures and dynamic `[slug]` routes.

The About page contains the company presentation and the profile of Enyinnaya Omeruah.

The About profile currently includes the optimized WebP headshot:

`public/enyinnaya-omeruah.webp`

The global header includes responsive desktop and mobile navigation.

The mobile navigation uses an accessible menu button with open/close state handling.

## 86.3 Current Deployment Flow

The production flow is:

    GitHub repository
          |
          v
      main branch
          |
          v
    GitHub Actions
          |
          v
       npm ci
          |
          v
     npm run build
          |
          v
      GitHub Pages
          |
          v
    virtualconcept.tech

Production changes should be represented in Git before they are considered permanent.

## 86.4 Future AI Session Starting Procedure

When an AI agent begins work on this project after a previous session, it must not rely on conversational memory alone.

It should first inspect the current repository.

Minimum inspection:

    git status
    git log --oneline -10
    git branch --show-current

Then inspect the relevant source files and this documentation before making changes.

The current repository state takes precedence over remembered conversation context.

## 86.5 Continuity Rules

Future AI agents should:

1. Understand the existing architecture before changing it.
2. Inspect relevant files before editing.
3. Preserve existing patterns where practical.
4. Make the smallest change that satisfies the request.
5. Avoid unrelated refactoring.
6. Avoid unnecessary dependencies.
7. Avoid changing working infrastructure without a genuine reason.
8. Treat explicit scope restrictions as hard requirements.
9. Run `git diff --check` after changes.
10. Run `npm run build` for website code changes.
11. Review the resulting Git diff before committing.
12. Verify deployment when a change has been pushed to production.
13. Update this documentation when important architectural or operational knowledge changes.

## 86.6 Maintaining Accuracy

This ledger must describe the repository that actually exists.

If the architecture, deployment process, navigation, technology stack, assets, development workflow, or other important project characteristics change, this documentation should be updated accordingly.

Documentation must never claim that an implementation exists when it does not exist in the repository.

## 86.7 Conversation Continuity

Previous AI conversations may contain useful reasoning, decisions, preferences, and implementation history, but conversations are not the authoritative project record.

When previous conversational context is unavailable, the AI agent should reconstruct the project from:

1. Current repository files
2. Git history
3. Project documentation
4. Deployment configuration
5. Existing implementation patterns

The agent must not invent missing history.

If the repository does not provide sufficient evidence for an important decision, uncertainty should be identified explicitly rather than replaced with an assumption.

## 86.8 Change Discipline

When the maintainer requests a narrowly scoped change, only that change should be made unless another modification is technically necessary.

In particular, do not casually:

- redesign existing pages;
- rewrite working components;
- alter unrelated content;
- introduce new frameworks;
- change deployment architecture;
- modify domain configuration;
- replace working solutions with different implementations;
- reorganize the repository without a clear reason.

The project should evolve deliberately.

## 86.9 Session Handover Standard

A significant development session should leave enough evidence for another developer or AI agent to determine:

- what was changed;
- why it was changed;
- which files were affected;
- whether validation passed;
- whether deployment occurred;
- whether anything remains unfinished.

Git commits provide the detailed historical record.

This documentation provides the durable operational context.

## 86.10 Continuity Objective

The long-term objective is that a future developer or AI agent can enter the repository after an extended period, read this documentation, inspect the current implementation, and continue the project safely without depending on undocumented personal memory.

The repository, Git history, and documentation should therefore remain synchronized.

This continuity mechanism should improve over time without becoming unnecessarily complex.
