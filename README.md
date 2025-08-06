# CSRF Generator

A simple Python tool with a lightweight GUI for generating CSRF (Cross-Site Request Forgery) exploit forms from raw HTTP POST requests.

---

## What is this?

This tool lets you paste a **full raw HTTP POST request** (including headers and body), parses it, and produces a clean, ready-to-use **auto-submitting HTML form** that exploits CSRF vulnerabilities.

---

## Why?

- Quickly create CSRF PoCs without manual HTML crafting  
- Works entirely offline with zero dependencies except Python’s built-in Tkinter  
- Perfect for pentesters, red teamers, or security researchers  
- Easy to add to your Red Team toolkit

---

## Requirements

- Python 3 (tested on Python 3.8+)  
- Tkinter GUI (usually bundled with Python on Linux distros)

---

## Installation

1. Clone this repo or download the `csrf_generator.py` script:

   ```bash
   git clone https://github.com/yourusername/csrf-generator.git
   cd csrf-generator
   python csrf-generator.py
