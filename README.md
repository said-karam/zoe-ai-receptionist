# Zoé, AI receptionist for salons

> Proof of concept, not a commercial product. This repository is a write-up only; the source code is private.

## Problem

Small beauty and wellness salons in France miss calls and WhatsApp messages while they work. Every missed message can be a lost booking.

## What I built

An assistant that answers a salon's WhatsApp messages and phone calls in French, in the salon's name:

- quotes the salon's real prices and services, and never invents them
- offers free slots and takes booking requests that the owner confirms with one tap from a text message
- sends customers confirmations and reminders (the day before and 2 hours before)
- hands the conversation to a human when needed, and pauses when staff reply themselves
- a team console with the salon's agenda drawn like its paper appointment book, a test chat and conversation history

## Key decisions

- **I wrote the brief first.** A requirements document (cahier des charges) came before any code, and the code references its requirement IDs.
- **The business logic is ours, the AI is rented.** Bookings, availability and customer data live in our own system. The voice and text assistants call it as tools, so they share one source of truth and the AI provider can be swapped.
- **WhatsApp connects directly, not through the voice platform.** The voice platform's WhatsApp integration could not work with a number still used in the WhatsApp Business app. A direct connection fixed that, kept messages in EU storage and cost less per message.
- **EU data by design.** Database and files are hosted in the EU. The voice provider runs in zero-retention mode, and call transcripts are copied to our EU storage.
- **Tested before spending.** Unit tests for the booking engine, end-to-end checks with simulated services (no double booking, customer and salon isolation, outage fallback), and about 40 scripted acceptance conversations with automatic scoring.

## Stack

TypeScript, Cloudflare Workers, D1 and R2 (EU), Claude (text), ElevenLabs (voice), Twilio (numbers and SMS), Meta WhatsApp Cloud API.

## Status

Phase 0 demo, built and tested. Not offered to customers.

Built with AI-assisted development (Claude Code).
