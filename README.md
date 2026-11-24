# PathEx

An AI-powered Chrome extension that guides users step-by-step through complex web tasks and flags dark patterns before they commit.

## Proof of Concept
The proof of concept is a live demo on 3 real or mock sites in which a first-time user completes a goal using only PathEx's highlights. We will show the guide leading a user through the cancel flow, a red warning catching a pre-ticked add-on, and the final "You decide" stop. We will test it with a few classmates and measure time to finish, wrong clicks, and traps caught, with and without PathEx. If PathEx helps people finish faster and avoid traps on these flows, the same loop can extend to more sites and languages.

## MVP
In 24 hours we will build one complete guided loop: the user types or speaks a goal, PathEx reads the page, highlights the single next click with a short reason, and flags dark patterns such as fake timers, pre-ticked add-ons, and hidden fees. It stops at any payment or confirm step with a "You decide" message and a "3 things that can hurt you" summary of the terms. ElevenLabs reads each step aloud in English, Hindi, or Kannada. The MVP is tuned and tested on 3 fixed flows (cancel a subscription, complete a checkout, pay a bill). It never clicks for the user and stores nothing.

## Codebase & Architecture
The PathEx codebase will be a single TypeScript monorepo on GitHub with two parts:
- **Chrome Extension (Manifest V3):** A content script that reads the page's text and clickable elements and draws highlights and warnings, plus a React side panel for the user's goal, step list, and voice controls. Settings stay in `chrome.storage`.
- **AWS Lambda Proxy:** Receives the goal and page data, calls the LLM with a strict JSON prompt, and returns the next step and any traps so the API key never sits in the browser. No external database is used.

