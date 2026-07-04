# [BraNGen](https://brangen.veoplix.com)

BraNGen is a browser-based brand and name generator designed to create original, pronounceable, and stylistically varied wordmarks. It combines weighted phonetic patterns from several European languages with mood-based tuning, then wraps the results in a practical naming workflow: pronunciation preview, dictionary collision checking, favourites, custom entries, and quick external availability checks.

The project is implemented as a single static HTML page with embedded CSS and JavaScript. There is no backend, no build step, and no database. Everything runs in the browser.

## Purpose

BraNGen exists to help users quickly explore fresh naming ideas that sound plausible without feeling generic. It is especially suited to situations where a name needs to be:

- new rather than copied from an existing word
- easy to pronounce aloud
- adaptable to different tones or moods
- easy to review for branding, domain, and social handle potential

Typical use cases include:

- startup and product naming
- app, SaaS, and tool branding
- game factions, characters, worlds, and artifacts
- creative writing and worldbuilding
- side projects, studios, podcasts, and channels
- placeholder naming during design exploration

## What The Tool Does

BraNGen generates short invented names and presents each one as a rich result card. Every card includes:

- the generated name
- a segmented pronunciation hint
- a style tag showing the language family or mixed style used
- a syllable count
- a mood indicator
- an English dictionary check result
- text-to-speech buttons for multiple languages
- one-click search, domain, and social profile shortcuts
- a favourite toggle

In addition to automatic generation, the tool lets users create and store manual custom names and manage a browser-saved favourites list.

## Core Features

### 1. Automatic Name Generation

The main Generate view produces batches of names immediately on load and continues generating more as the user scrolls.

- initial batch size: 7 names
- infinite scroll batch size: 5 names
- available name lengths: 2 to 4 syllables
- supported generation moods: `neutral`, `happy`, `scary`, `scifi`, `fantasy`, `funny`

Each generated result receives a unique ID and is treated as a standalone naming candidate.

### 2. Multilingual Phonetic Engine

BraNGen blends weighted sound patterns inspired by these language sets:

- English
- Polish
- Spanish
- German
- French
- Italian
- Portuguese
- Mixed mode, which can combine syllables across the supported sets

For each language, the generator defines:

- onset consonants and consonant clusters
- vowel nuclei
- syllable endings
- probabilities for vowel starts and closed syllables

This makes the output feel varied while still tending toward pronounceable structures instead of random character strings.

### 3. Mood-Based Output Shaping

The mood selector changes the probability weights used during generation. It does not simply relabel the result; it actively biases which sounds are more likely to appear.

The implemented moods aim for these effects:

- `neutral`: balanced default output
- `happy`: softer, brighter, lighter-sounding names
- `scary`: harsher, darker, more guttural names
- `scifi`: sharper, more synthetic or futuristic names
- `fantasy`: flowing, archaic, mystical names
- `funny`: bouncy, whimsical, playful names

Mood affects:

- consonant selection
- vowel selection
- ending selection
- in some cases, the chance of open versus closed syllables

### 4. Pronunciation Preview

Every result includes a pronunciation string rendered with dot-separated syllable chunks, for example in a pattern like `/ka·ren/`.

This is a guide rather than a strict phonetic transcription. Its role is to make the generated structure readable at a glance and help users judge whether a name sounds natural.

### 5. Native Text-to-Speech Playback

Each result card includes speech buttons for:

- English
- Polish
- Spanish
- German
- French
- Italian
- Portuguese

BraNGen uses the browser Web Speech API and attempts to pick a locally available voice for the selected language when possible. This is useful for quickly hearing how a candidate may sound across languages and accents.

For the most reliable speech synthesis behavior and voice availability, BraNGen works best in Google Chrome.

### 6. Real-Time English Dictionary Check

For every generated or custom name, the tool queries `dictionaryapi.dev` to determine whether the word already exists in the English dictionary.

Possible outcomes:

- if no entry is found, the name is presented as an original candidate
- if a real English word is found, the card shows that fact and displays the first available definition

This helps users avoid accidental collisions with common English words when they want a more distinctive brand or fictional name.

### 7. Custom Name Creation

The Custom view allows manual entry of names.

Current custom-entry behavior:

- trims leading and trailing whitespace
- collapses repeated spaces to single spaces
- capitalizes the first character
- derives a simple pronunciation display from the typed value
- estimates syllable count by vowel-group matching
- stores the entry locally in the browser

Custom names are displayed using the same result-card interface as generated names, including pronunciation, dictionary check, favourite toggle, speech buttons, and external shortcuts.

### 8. Favourites Saved In The Browser

Any generated or custom name can be added to favourites by clicking the heart icon.

Favourites behavior:

- saved in `localStorage`
- persist between browser sessions on the same browser profile
- can be removed by toggling the heart again
- are shown in a dedicated Favourite view

BraNGen uses these storage keys:

- `brangen-favorites-v1`
- `brangen-custom-words-v1`

No cloud sync is implemented.

### 9. Quick Branding Research Links

Each result card includes shortcuts for rapid follow-up checks:

- Google search for the candidate name
- Namecheap `.com` registration results page
- YouTube handle page
- Facebook profile/username page
- X handle page
- Instagram handle page
- TikTok handle page

These shortcuts do not verify availability directly inside BraNGen. They open the corresponding external pages so the user can inspect conflicts or claimability.

### 10. One-Click Copy

Clicking the generated name copies it to the clipboard and briefly replaces the visible label with `Copied!`.

This makes it easy to collect promising candidates during review.

## Interface Overview

BraNGen is organized into three views.

### Generate

The main exploration workspace.

- choose length with a 2 to 4 syllable slider
- choose mood with six mood buttons
- receive an initial batch automatically
- keep scrolling to load more candidates

### Custom

Manual entry and storage.

- type a custom name
- press Create or hit Enter
- review the result with the same tooling as generated entries
- optionally delete custom entries later

### Favourite

Shortlist management.

- view saved favourites
- replay pronunciation
- run the same external checks
- remove entries from favourites when no longer needed

## How The Generator Works

BraNGen is not using an AI model or a dictionary-based word splicer. It uses handcrafted weighted phonetic rules.

At a high level, generation works like this:

1. Pick a style from one of the supported languages or from a mixed mode.
2. For each syllable, decide whether it starts with a consonant cluster or a vowel.
3. Choose a vowel nucleus using weighted probabilities.
4. Optionally add a syllable ending depending on language-specific coda probabilities.
5. Apply mood multipliers to shift sound selection.
6. Enforce a few validity rules to avoid awkward combinations.
7. Join the syllables, remove triple-letter artifacts, and capitalize the result.

### Built-In Validity Rules

The implementation includes some safeguards to keep output more pronounceable, for example:

- avoids awkward `qu` plus incompatible vowel combinations
- avoids problematic `y` and `j` vowel sequences such as `jyi`
- reduces unnatural word-initial `y` vowels in English, Polish, and German contexts
- strips triple repeated letters during cleanup

These rules do not guarantee perfect phonology, but they noticeably improve output quality compared with unrestricted random assembly.

## When BraNGen Is Most Useful

BraNGen is strongest when the goal is exploration rather than final legal clearance. It is useful early in the naming process when the user wants a large volume of pronounceable ideas with a chosen tone.

It is a good fit when you want to:

- discover novel-sounding names fast
- explore several naming moods without rewriting prompts or rules
- build a shortlist before deeper trademark or SEO review
- test whether a coined name sounds plausible in several European-language contexts
- compare machine-generated ideas with your own manual custom names

## Project Structure

The repository for BraNGen is intentionally minimal:

- `index.html`: the full application, including layout, styling, and logic
- `LICENSE`: project license

There is no package manifest, no bundler config, and no backend service.

## Running The Project

Because BraNGen is a static client-side app, setup is simple.

### Option 1: Use The Hosted Project Page

Open the live project page:

[`https://brangen.veoplix.com`](https://brangen.veoplix.com)

This is the fastest way to use BraNGen with no local setup.

For the best speech synthesis experience, Google Chrome is recommended.

### Option 2: Open Directly

Open `index.html` in a modern browser.

### Option 3: Serve Locally

For more predictable browser behavior, serve the folder with a small local web server.

Examples:

```powershell
cd brangen
python -m http.server 8000
```

Then open `http://localhost:8000`.

Using a local server can help avoid browser restrictions around clipboard access, speech synthesis behavior, or local file handling differences.

## Dependencies And External Services

BraNGen has no package-managed dependencies, but it does rely on external browser-loaded assets and services:

- Tailwind CSS CDN
- Font Awesome CDN
- Google Fonts for `Space Grotesk`
- browser `speechSynthesis` support
- browser `localStorage` support
- `dictionaryapi.dev` for English word lookup

External links used for follow-up checks include:

- Google Search
- Namecheap
- YouTube
- Facebook
- X
- Instagram
- TikTok

If any of these external services are unavailable, the core generator still works, but related features may degrade.

## Privacy And Data Handling

BraNGen is primarily local-first in behavior.

What stays local:

- generated results in the current session view
- saved favourites in browser `localStorage`
- saved custom words in browser `localStorage`
- speech playback handled by the browser

What leaves the browser:

- dictionary lookup requests sent to `dictionaryapi.dev`
- external searches and handle/domain checks opened on third-party sites

There is no dedicated BraNGen backend collecting or storing user data in the current implementation.

## Limitations

BraNGen is practical, but it should be understood as an ideation tool rather than a full naming clearance platform.

- It does not perform trademark checks.
- It does not guarantee domain or social handle availability.
- Its dictionary test is English-only.
- It does not score names for SEO, memorability, or legal risk.
- It relies on browser support for speech synthesis, clipboard access, and `localStorage`.
- It relies on third-party network access for dictionary lookups and external shortcut destinations.
- Pronunciation hints are heuristic and not IPA-grade phonetic transcriptions.
- Generated names are weighted-random outputs, so quality varies by run and personal taste.

## Why BraNGen Is Distinctive

BraNGen is not just a random word generator. Its value comes from the combination of:

- handcrafted multilingual phonetic weighting
- mood-driven sound shaping
- immediate pronounceability review
- built-in originality check against English dictionary entries
- practical brand research shortcuts
- a lightweight, zero-backend browser implementation

That makes it well-suited for fast creative iteration, especially when users want names that feel invented but still speak naturally.

## Summary

BraNGen is a compact naming workbench for generating original-sounding names with controlled tone and strong usability. It helps users go from raw invention to shortlist review inside a single page: generate, listen, check, save, compare, and investigate further.

If your goal is to discover pronounceable new names for brands, products, fictional settings, or creative projects, BraNGen is built exactly for that stage of the process.