# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

シンプル低周波発振器 (Simple Low-Frequency Oscillator) — a single-file static web app for physics and acoustics experiments. The entire application lives in `teisyuha_buturikiso.html` with no build process, no dependencies to install, and no backend.

## Running the App

Open `teisyuha_buturikiso.html` directly in any modern browser. No server required.

## Architecture

Everything is in one file (`teisyuha_buturikiso.html`), structured as:

- **CSS** (lines 11–80): Styles for digit display, buttons, slider, and responsive breakpoints.
- **HTML** (lines 82–160): Bootstrap 5 grid layout — frequency digit display, 6-column button grid (up/down per digit position), range slider, and play/stop toggle.
- **JavaScript** (lines 165–309): Vanilla JS with Web Audio API.

### Audio Engine

Uses the Web Audio API: `OscillatorNode` (sine wave) → `GainNode` → audio destination. The oscillator is recreated on each frequency change while playing (Web Audio nodes are not reusable after `stop()`).

### Frequency Control

Frequency state is a single float (`frequency`, default 50.0 Hz, range 1.0–20,000.0 Hz). Two control surfaces stay in sync:

- **Digit buttons**: 6 columns for digit positions (10,000s → 0.1s). `changeFrequency(position, delta)` modifies by 10^position.
- **Slider**: maps the same range (1.0–20,000.0).

`updateFrequencyDisplay()` formats the number as `"XXXXX.X Hz"` and distributes digits to individual `<span>` elements.

## External Resources (CDN)

- Bootstrap 5.3.2
- Bootstrap Icons 1.11.1

No local copies — changes to UI components depend on CDN availability.

## Language

README and UI labels are in Japanese. Keep UI text and comments in Japanese when modifying the HTML.
