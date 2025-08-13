# Xiaohongshu Auto-Reply Bot

This project is a Python-based bot that automatically replies to new messages on Xiaohongshu (RED). It uses the Playwright library to automate web browser interactions.

## Features

-   Logs into a Xiaohongshu account.
-   Periodically checks for new, unread messages.
-   Sends a pre-defined, static reply to each new message.

## How to Use

### 1. Installation

First, clone this repository and install the necessary dependencies.

```bash
git clone <repository_url>
cd <repository_directory>
pip install -r requirements.txt
```
Also, you need to install the browser binaries for Playwright:
```bash
playwright install
```

### 2. Configuration

Open the `xiaohongshu_bot/main.py` file and update the configuration section at the top:

-   **Credentials**: Replace `"YOUR_USERNAME"` and `"YOUR_PASSWORD"` with your Xiaohongshu login credentials. For better security, it is highly recommended to load these from environment variables instead of hardcoding them.

### 3. Finding CSS Selectors

This is the most important step to make the bot work. The bot uses CSS selectors to find elements on the page (like buttons and input fields). These selectors can change when Xiaohongshu updates its website. You need to find the current selectors and update them in the `main.py` script.

**How to find a selector:**

1.  Open Xiaohongshu in your web browser (e.g., Chrome).
2.  Open the Developer Tools (usually by pressing `F12` or right-clicking and selecting "Inspect").
3.  Use the "Elements" panel to inspect the HTML structure of the page.
4.  Use the element selector tool (usually an icon of a mouse cursor in a box) to click on the element you're interested in (e.g., the login button).
5.  The corresponding HTML element will be highlighted in the Elements panel.
6.  Right-click on the highlighted element and choose "Copy" > "Copy selector".
7.  Paste this selector string into the appropriate placeholder in the `main.py` script.

**You will need to find selectors for the following elements:**

-   **Login Process** (in the `login` function):
    -   The button to open the login form (if there is one).
    -   The username/phone number input field.
    -   The password input field.
    -   The final "submit" or "login" button.
-   **Message Detection** (in the `check_for_new_messages` function):
    -   The icon or button on the main page to navigate to the messages/chat section.
    -   The selector for unread conversations. This is often a list item `<li>` or a `<div>` with a specific class like `unread`.
-   **Replying to Messages** (in `handle_new_messages` and `send_reply`):
    -   The element representing a single conversation to click on.
    -   The selector for the last message in a conversation to extract its text.
    -   The message input text area.
    -   The "send" button.

Replace the placeholder strings like `'selector_for_login_prompt'` in the code with the selectors you find.

### 4. Running the Bot

Once the configuration and selectors are set, you can run the bot:

```bash
python xiaohongshu_bot/main.py
```

The script will launch a browser window so you can monitor its activity.

## Disclaimer

Using automated bots may be against the terms of service of Xiaohongshu. Use this bot at your own risk. The developers of this bot are not responsible for any consequences, including account suspension or termination.
