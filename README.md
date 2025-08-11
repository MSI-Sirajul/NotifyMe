<body>
  <div class="container">
    <h1>NotifyMe — Release Notes</h1>
    <p class="muted">Version: <strong>15.5.4</strong> • Release date: <strong>11/08/2025</strong></p><section>
  <h2>Overview</h2>
  <p>
    FullStop is an all-in-one mobile utility that: captures and processes system notifications, reads and rates incoming SMS, forwards selected notifications/SMS to Telegram (and other targets), and identifies phone activity (foreground app / screen events) for contextual workflows.
  </p>
  <p class="muted">Short: notification handling + SMS processing + forwarding + phone activity identification — packed into one app.</p>
</section>

<section>
  <h2>Key Features</h2>
  <ul>
    <li><strong>Notification Read & Forward</strong> — capture system notifications, filter, redact, and forward to Telegram/chat targets.</li>
    <li><strong>SMS Read, Rate & Forward</strong> — read incoming SMS, apply rating rules (spam/important/auto-tag), and forward to configured channels.</li>
    <li><strong>Phone Activity Identification</strong> — detect active app, screen on/off, call states to tag context with forwarded messages.</li>
    <li><strong>Telegram Integration</strong> — direct Telegram Bot API support; forward to single or multiple chat IDs or channels.
    </li>
    <li><strong>Multi-target Forwarding</strong> — Telegram + HTTP webhook endpoints + optional email/S3 (placeholders).</li>
    <li><strong>Rule Engine</strong> — customizable rules for filtering, masking PII, auto-forward, or suppressing alerts.
    <li><strong>Local Log & Audit</strong> — local message logs, with export option (CSV/JSON).</li>
  </ul>
</section>

<section>
  <h2>Installation & Upgrade</h2>
  <ol>
    <li>Download the APK: <code>FullStop-v{{VERSION}}.apk</code></li>
    <li>Enable <span class="kbd">Install unknown apps</span> for your package installer if required.</li>
    <li>Install/Upgrade — existing settings are preserved on in-place upgrade. If you face permission issues, uninstall then reinstall.</li>
  </ol>
</section>

<section>
  <h2>Permissions Required</h2>
  <ul>
    <li><strong>Notification access</strong> — to read and capture notifications.</li>
    <li><strong>SMS receive & read</strong> — to detect and process SMS (Android SMS permissions).</li>
    <li><strong>Foreground service</strong> — to reliably track phone activity and keep the app alive.</li>
    <li><strong>Network access</strong> — to forward messages to Telegram / webhooks.</li>
    <li><strong>Optional storage</strong> — to export logs (CSV/JSON).</li>
  </ul>
</section>

<section>
  <h2>Configuration — required placeholders</h2>
  <p>Below are the key configuration placeholders you must fill before using forwarding features. Replace <code>{{...}}</code> tokens with real values.</p>

  <div class="placeholder">
    <strong>Telegram settings</strong>
    <ul>
      <li><code>TELEGRAM_BOT_TOKEN:</code> <em>e.g.</em> <code>8462399272:AAGqOZLNh6bnuIVEdEUXtpF0b7MPXh4pMwk</code></li>
      <li><code>DEFAULT_CHAT_ID:</code> <em>e.g.</em> <code>8030227425</code></li>
      <li><code>ADDITIONAL_CHAT_IDS:</code> comma-separated list, <code>8030227425,5185579644</code></li>
    </ul>
  </div>

  <div class="placeholder" style="margin-top:10px">
    <strong>Webhook / HTTP targets</strong>
    <ul>
      <li><code>WEBHOOK_URL_1:</code> <code>{{WEBHOOK_URL_1}}</code></li>
      <li>Optional auth header: <code>WEBHOOK_AUTH_HEADER={{WEBHOOK_AUTH_HEADER}}</code></li>
    </ul>
  </div>

  <div class="placeholder" style="margin-top:10px">
    <strong>Forwarding rules & privacy</strong>
    <ul>
      <li>PII mask template: <code>{{PII_MASK}}</code> (example: <code>***MASKED***</code>).</li>
      <li>Phone activity tag: set to <code>ON/OFF</code> to append active-app context.</li>
    </ul>
  </div>

  <p class="muted">Note: For Telegram bot setup, follow the standard BotFather flow to create a bot and obtain the bot token. Use the bot token above to send messages programmatically.</p>
</section>

<section>
  <h2>Sample Telegram POST (curl)</h2>
  <pre>

curl -s -X POST "[https://api.telegram.org/bot8462399272:AAGqOZLNh6bnuIVEdEUXtpF0b7MPXh4pMwk/sendMessage](https://api.telegram.org/bot%7B%78462399272:AAGqOZLNh6bnuIVEdEUXtpF0b7MPXh4pMwk%7D%7D/sendMessage)" 
-d chat_id="8462399272" "5185579644"
-d text="New notification from NotifyMe: {{MESSAGE_PREVIEW}}" </pre>

<p class="muted">Replace tokens with real values. The app can call this automatically when forwarding rules match.</p>
</section>

<section>
  <h2>Changelog (high level)</h2>
  <ul>
    <li><strong>v{{VERSION}}</strong> — Unified release: Notification routing + SMS rating/forwarding + phone activity identification + multi-target forwarding + export logs.</li>
    <li>Improved rule engine and PII masking.</li>
    <li>Performance: reduced battery impact via optimized foreground service scheduling.</li>
  </ul>
</section>

<section>
  <h2>Known Issues & Limitations</h2>
  <ul>
    <li>Android OEM battery optimizations may stop the foreground service on some devices — ask user to whitelist the app in device power settings.</li>
    <li>SMS reading requires explicit permission on recent Android versions; user must accept at runtime.</li>
    <li>Telegram rate limits — forwarding a very high volume of messages may be throttled by Telegram APIs.</li>
  </ul>
</section>

<section>
  <h2>Security & Privacy</h2>
  <p>
    By default, FullStop will <strong>not</strong> forward messages containing configured sensitive patterns (PII). Configure the <code>PII_MASK</code> and rule engine to redact phone numbers or other secrets. Stored logs are local; enable encrypted backups at your own risk.
  </p>
</section>

<section>
  <h2>How to Customize Copy (examples)</h2>
  <pre>

// Toggle phone activity tagging PHONE_ACTIVITY_TAGGING=ON

// Set PII mask PII_MASK=REDACTED

// Default targets TELEGRAM_BOT_TOKEN="{{TELEGRAM_BOT_TOKEN}}" DEFAULT_CHAT_ID="{{TELEGRAM_CHAT_ID}}" WEBHOOK_URL_1="{{WEBHOOK_URL_1}}" </pre> </section>

<section>
  <h2>Support & Contact</h2>
  <p>If you find bugs or want new features, please report to <code>{{SUPPORT_EMAIL}}</code> or open an issue at <code>{{ISSUE_TRACKER_URL}}</code>.</p>
</section>

<section>
  <h2>License</h2>
  <p>© {{YEAR}} FullStop — include your license here (MIT / Apache-2.0 / Proprietary).</p>
</section>

<footer style="margin-top:18px" class="muted">
  <small>Generated: <code>{{RELEASE_DATE}}</code> • Template engine: smackdown/html-markdown • Edit placeholders before publishing.</small>
</footer>

  </div>

## Telegram Credentials: 
BOT_Token:  
Notify Me:`8462399272:AAGqOZLNh6bnuIVEdEUXtpF0b7MPXh4pMwk`  
Chat ID:  
NotifyMe `8030227425`  
MSI `5185579644`


