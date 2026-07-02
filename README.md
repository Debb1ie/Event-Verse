# Eventverse

A social event discovery and management platform built as a single-file HTML/CSS/JavaScript application. Eventverse allows users to discover local and online events, RSVP, interact with a social feed, message other attendees, and create their own events.

---

## Table of Contents

- [Overview](#overview)
- [Pages and Features](#pages-and-features)
  - [Discover](#discover)
  - [Feed](#feed)
  - [My Events](#my-events)
  - [Messages](#messages)
- [UI Components](#ui-components)
  - [Navigation](#navigation)
  - [Event Cards](#event-cards)
  - [Modals](#modals)
  - [Toast Notifications](#toast-notifications)
  - [Map Section](#map-section)
  - [Stories Row](#stories-row)
  - [Sidebar](#sidebar)
- [Design System](#design-system)
  - [Color Palette](#color-palette)
  - [Typography](#typography)
  - [Spacing and Layout](#spacing-and-layout)
  - [Animations](#animations)
- [JavaScript Functionality](#javascript-functionality)
  - [Navigation System](#navigation-system)
  - [Event Filtering](#event-filtering)
  - [RSVP and Save Actions](#rsvp-and-save-actions)
  - [Messaging System](#messaging-system)
  - [Create Event Modal](#create-event-modal)
  - [Countdown Timer](#countdown-timer)
- [Responsive Design](#responsive-design)
- [File Structure](#file-structure)
- [Getting Started](#getting-started)
- [Customization Guide](#customization-guide)

---

## Overview

Eventverse is a dark-themed, modern single-page application (SPA) that simulates a full event social network. The entire application is contained within a single HTML file — no build tools, no dependencies, no server required. Open the file in any browser and it runs immediately.

The design language draws from contemporary product design: high contrast dark backgrounds, a lime-green accent color, glass morphism effects, noise textures, and tight typographic hierarchy using variable fonts loaded from Google Fonts.

---

## Pages and Features

The application is structured into four distinct pages. Navigation between pages is handled entirely in JavaScript by toggling CSS classes. Each page transition plays a subtle fade-and-slide animation.

### Discover

The landing page. It is divided into two main regions: a full-width hero section and a scrollable content area below it.

**Hero Section**

The hero occupies the full viewport width and is split into a two-column grid on desktop. The left column contains the main headline, a supporting paragraph, two call-to-action buttons, and a row of platform statistics. The right column shows a "Trending Now" list of three mini event cards, each clickable to open the event detail modal. On screens narrower than 960px, the right column is hidden.

The headline uses a large variable-size display font with an italicized word rendered in the accent color and a serif typeface to create typographic contrast. A live indicator badge above the headline shows a blinking red dot alongside the count of active events.

**Featured Banner**

Below the hero is a prominent banner card promoting a single featured event. It uses a purple-to-green gradient background and displays a countdown timer that ticks live in the browser. A "Get Tickets" button is included on the right side.

**Search and Filtering**

A full-width search input allows users to type and filter the events grid in real time. The search bar contains quick-filter chips for time-based filters: All, Today, Weekend, and Free.

Below the search bar is a row of category chips: All Events, Music, Tech, Art, Food, Fitness, Business, Community, and Online. Clicking a chip filters the events grid to show only matching events.

A tab row beneath the categories provides additional filtering contexts: All, Friends Going, Online Only, and Saved.

**Events Grid**

The main content area renders event cards in a responsive CSS grid. Cards are generated dynamically from a JavaScript data array. Each card shows a colored cover area, event title, date, location, attendee count, a type badge (Free, Paid, or Online), an RSVP button, and a save button.

**Map Section**

At the bottom of the Discover page is a decorative map panel. It shows a city grid background with animated pulsing pins representing event locations. The section is purely visual and does not integrate with a real mapping API.

---

### Feed

The Feed page is a social timeline, similar to a Twitter or LinkedIn feed oriented around events and their attendees.

**Stories Row**

A horizontally scrollable row of circular story thumbnails sits at the top. Stories have gradient ring borders. An "Add Story" item is included at the start of the row.

**Compose Box**

A text area with tool buttons (Tag Event, Photo, Location) allows users to draft posts. Clicking the Post button triggers a toast notification confirming the share.

**Post Cards**

The feed renders a list of post cards. Each post shows a user avatar, name, timestamp, and body text. Posts may include an attached event reference card — a bordered block with the event's name and date that links to the event detail modal. Each post has action buttons: Like, Comment, Going, and Share. The Like button turns red when toggled; Going turns green.

**Sidebar**

On desktop, a right-hand sidebar shows three secondary panels: People to Follow (with Follow buttons), Trending Tags (with event counts per tag), and Upcoming RSVPs (listing the user's next three events).

---

### My Events

A personal dashboard showing events the user is involved with. Four tabs organize the content:

- **Going** — Events the user has RSVP'd to attend. Defaults to showing cards from the main event data set that are marked as "going."
- **Saved** — Events bookmarked for later.
- **Hosting** — Events created by the user. Defaults to an empty state with a prompt to create a new event.
- **Past Events** — Historical events the user attended.

If a tab has no events, an empty-state prompt is displayed with a dashed border and a "Create Event" call-to-action.

---

### Messages

A full-height two-column chat interface. The left panel lists conversations with avatar, name, last message preview, timestamp, and unread badge. Clicking a conversation opens its chat thread in the right panel.

The chat area shows a scrollable message thread with alternating bubble styles: the other party's messages appear dark and left-aligned; the user's messages appear in the accent color and right-aligned. A text input and Send button at the bottom allow the user to type new messages, which are appended to the thread in real time.

---

## UI Components

### Navigation

A fixed top bar spans the full width. It contains the Eventverse logo (a pulsing dot and wordmark), page navigation links, a Notifications button with an unread dot, a Log In button, and a Create Event primary action button.

The active page's nav link receives a highlighted style. Clicking any nav link triggers the page navigation function.

### Event Cards

Event cards are the primary display unit for events. They follow a consistent structure:

- A cover area with a colored gradient background and a large faint label
- A gradient overlay fading to the card background
- Meta row: date on the left, attendee count on the right
- Title and location
- A footer row with a type badge, RSVP toggle button, and save toggle button

Hovering a card slightly lifts it with a box shadow. Clicking the card body (excluding the action buttons) opens the event detail modal.

### Modals

Two modal types are implemented:

**Create Event Modal** — A form with fields for event name, date, time, location, category chips, description, ticket type (Free, Paid, Invite Only), capacity, and visibility (Public, Friends Only, Private). A Submit button at the bottom triggers a toast and closes the modal.

**Event Detail Modal** — Shows the full event information: a large cover area, event title, host name, a four-cell metadata grid (Date, Time, Location, Capacity), a description, an attendee avatar stack with a count, and RSVP / Save action buttons.

Modals open with a backdrop blur overlay. Clicking outside the modal card closes it.

### Toast Notifications

A small pill-shaped notification appears at the bottom center of the viewport. It slides up and fades in, then disappears after two seconds. It is used to confirm user actions such as posting, RSVPing, saving, sending a message, and submitting a new event.

### Map Section

A decorative panel rendered entirely in CSS and SVG-like HTML. It displays a grid pattern, radial gradient lighting, and several absolutely-positioned pins at hardcoded coordinates. Each pin pulses with a keyframe animation. Three pin color variants correspond to the three accent colors.

### Stories Row

The story row uses `overflow-x: auto` with scrollbar hidden via CSS for a native swipe feel. Each story item consists of a gradient ring, an inner circle with initials or a plus icon, and a name label.

### Sidebar

Three stacked cards on the right side of the Feed page. Each card has a title and a list of items. People items have avatars, names, status lines, and a Follow button. Trend items have a faint ranking number, tag name, and event count. Upcoming RSVP items use a small colored dot, event name, and date.

---

## Design System

### Color Palette

All colors are defined as CSS custom properties on `:root` and referenced throughout the stylesheet. This makes global re-theming possible by editing a single block.

| Variable    | Value                    | Usage                                      |
|-------------|--------------------------|---------------------------------------------|
| `--bg`      | `#080a0f`                | Page background                            |
| `--bg2`     | `#0e1118`                | Secondary background (message sidebar)     |
| `--bg3`     | `#141820`                | Input fields, inner containers             |
| `--card`    | `#141820`                | Card backgrounds                           |
| `--border`  | `rgba(255,255,255,0.07)` | All borders and dividers                   |
| `--accent`  | `#c8f04a`                | Primary accent — buttons, dates, highlights |
| `--accent2` | `#ff6b6b`                | Secondary accent — likes, online badges    |
| `--accent3` | `#7c6aff`                | Tertiary accent — purple highlights        |
| `--text`    | `#f0f2f5`                | Primary text                               |
| `--muted`   | `#6b7280`                | Secondary text, labels, placeholders       |
| `--glass`   | `rgba(255,255,255,0.04)` | Hover fills on transparent elements        |

### Typography

Three typefaces are loaded from Google Fonts:

- **Clash Display** — A geometric display font used for headings, card titles, stat numbers, and the logo. Weights 400 through 700.
- **Instrument Serif** — An elegant serif used only for the italicized word in the hero headline to create editorial contrast.
- **DM Sans** — A clean optical-size sans-serif used for all body text, labels, buttons, and UI copy. Weights 300 through 600.

The base font size is 14–17px depending on context. Display sizes are set with `clamp()` in the hero to scale fluidly between viewport widths.

### Spacing and Layout

The application uses a 1280px max-width container with 40px horizontal padding (20px on mobile). The events grid uses `auto-fill` with a minimum column width of 290px, allowing natural reflow at any viewport width.

The Feed and Messages pages use explicit two-column CSS Grid layouts. The Feed sidebar is 320px wide; the Messages conversation list is 300px wide.

Vertical spacing between major sections uses a combination of fixed padding values (52px for section headers, 60px for bottom spacing) and grid gaps (18px for event cards, 28px for the feed layout).

### Animations

Four keyframe animations are defined globally:

- **pulse** — Scales and fades the logo dot, suggesting a live signal.
- **blink** — Fades the red live indicator dot in and out.
- **ping** — Expands and contracts the glow rings on map pins.
- **pageIn** — Translates and fades in a new page on navigation.

All interactive elements use `transition` on hover: cards lift with `translateY(-3px)`, primary buttons lift with `translateY(-1px)` and gain a colored box shadow, and links and chips shift color and background.

A fixed noise texture is layered over the entire page via a `body::before` pseudo-element using an inline SVG fractal noise filter, adding subtle film-grain texture without any external image files.

---

## JavaScript Functionality

All JavaScript is written inline at the bottom of the HTML file. No frameworks or external libraries are used.

### Navigation System

The `navigate(page)` function manages all page transitions. It removes the `active` class from all page containers and nav links, then adds it to the target page and the corresponding nav link. This produces an instant CSS-driven transition styled with the `pageIn` animation.

### Event Filtering

Event data is stored in a JavaScript array of objects. Each object includes a title, date string, location, category tag, attendee count, color palette string for the cover gradient, a badge type (free/paid/online), and boolean flags for saved and going states.

The `renderEvents(list)` function generates HTML strings from this array and injects them into the events grid container. Filtering functions — `filterEvents()` for text search, `filterCat(el, cat)` for category chips, and `setTimeFilter(el, filter)` for time chips — each call `renderEvents()` with a filtered subset of the data.

The tab switcher `setDiscoverTab(el, tab)` updates the active tab style but delegates display logic back to `renderEvents()`.

### RSVP and Save Actions

RSVP and Save are toggle actions on each event card. The `toggleRSVP(btn, id)` and `toggleSave(btn, id)` functions flip a boolean on the event object, update the button's CSS class, and show a toast notification confirming the action. Because the event data is the source of truth, re-rendering the grid reflects the current state.

### Messaging System

Conversation data is stored in a JavaScript array containing names, last messages, timestamps, unread counts, avatar colors, and a message thread array. The `renderConversations()` function builds the conversation list. Clicking a conversation calls `openConversation(id)`, which updates the chat header and renders the message thread.

The `sendMessage()` function reads the chat input, creates a new message object with the "me" flag, appends it to the active conversation's thread, re-renders the messages panel, and scrolls to the bottom. It then shows a toast and clears the input.

### Create Event Modal

`openCreateModal()` adds the `open` class to the modal overlay, making it visible. `closeCreateModal()` removes it. Clicking the overlay background also closes the modal. The `submitEvent()` function shows a toast and closes the modal; it does not persist data in this prototype.

The `toggleFormChip(el, group)` function implements single-select chip groups inside the form. It removes the active class from all chips in the group before applying it to the clicked chip.

### Countdown Timer

On page load, a `setInterval` runs every second and updates the `#cDays`, `#cHours`, and `#cMins` elements with a hardcoded future target date. The values are zero-padded to two digits.

---

## Responsive Design

A single breakpoint at 960px triggers layout changes via a `@media(max-width:960px)` block:

- Navigation padding reduces and the nav links row is hidden (only the right-side buttons remain).
- The hero switches from a two-column grid to a single column, and the hero right panel is hidden entirely.
- Container padding reduces from 40px to 20px.
- The Feed layout collapses from two columns to one column, and the sidebar disappears.
- The Messages layout collapses to single column and the conversation sidebar is hidden.
- My Events layout top padding reduces.

No JavaScript is involved in responsive behavior — all breakpoints are handled purely in CSS.

---

## File Structure

The entire application is a single self-contained file:

```
eventverse.html
  |-- <head>
  |     |-- Google Fonts import
  |     |-- <style> (all CSS, ~700 lines)
  |
  |-- <body>
        |-- <nav> (fixed top navigation)
        |-- #page-discover (Discover page)
        |-- #page-feed (Feed page)
        |-- #page-my-events (My Events page)
        |-- #page-messages (Messages page)
        |-- #createModal (Create Event modal)
        |-- #eventDetailModal (Event Detail modal)
        |-- .toast (Toast notification)
        |-- <script> (all JavaScript, inline)
```

---

## Getting Started

No installation, build step, or server is required.

1. Download or clone the repository.
2. Open `eventverse.html` in any modern web browser.
3. The application loads immediately.

For development, any text editor works. Because the file uses Google Fonts, a network connection is needed on first load to cache the fonts. After that, the file works fully offline.

---

## Customization Guide

**Changing the accent color** — Edit the `--accent` variable in `:root`. The lime green `#c8f04a` is used for buttons, dates, RSVP states, badges, and the logo dot. Changing this single variable updates all of them.

**Adding events** — Locate the `eventsData` array in the `<script>` block and add a new object following the existing structure. The grid, filtering, and modal system will pick it up automatically.

**Adding pages** — Create a new `<div id="page-newname" class="page">` block in the HTML body, add a nav link with `onclick="navigate('newname')"`, and the navigation system handles the rest.

**Changing fonts** — Replace the Google Fonts import URL in `<head>` and update the `font-family` references in the `:root` and style declarations. The three fonts map to: `'Clash Display'` for display text, `'Instrument Serif'` for decorative italic, and `'DM Sans'` for body text.

**Connecting real data** — Replace the static JavaScript data arrays with `fetch()` calls to a REST API. The render functions already accept data arrays as arguments, so the wiring is minimal.
