# Claude-Code-Setup-with-gemini
Free claude code setup with gemini

Free Claude Code Setup with Google Gemini
A complete setup guide for configuring Claude Code with Gemini models using claude-code and claude-code-router.

1. Prerequisites
Verify Node.js Installation
Open PowerShell and run:

node --version
If the version is 18.x or higher, you’re good to continue.
If not, download and install the latest LTS release:
https://nodejs.org

2. Generate Your Google API Key
Visit: https://aistudio.google.com
Select Get API Key
Click Create API Key
AIzaSy...............
3. Install Required CLI Tools
Open PowerShell (Run as Administrator):

npm install -g @anthropic-ai/claude-code @musistudio/claude-code-router
This installs both Claude Code and the router globally.

4. Create Required Configuration Directories
Run the following in a normal PowerShell window:

mkdir $HOME/.claude-code-router
mkdir $HOME/.claude
5. Create the Router Configuration File
Since Windows does not support cat << EOF syntax, create the configuration file using Notepad:

notepad $HOME/.claude-code-router/config.json
Paste the following JSON configuration exactly as shown:

{
  "LOG": true,
  "LOG_LEVEL": "info",
  "HOST": "127.0.0.1",
  "PORT": 3456,
  "API_TIMEOUT_MS": 600000,
  "Providers": [
    {
      "name": "gemini",
      "api_base_url": "https://generativelanguage.googleapis.com/v1beta/models/",
      "api_key": "$GOOGLE_API_KEY",
      "models": [
        "gemini-2.5-flash",
        "gemini-2.0-flash"
      ],
      "transformer": {
        "use": ["gemini"]
      }
    }
  ],
  "Router": {
    "default": "gemini,gemini-2.5-flash",
    "background": "gemini,gemini-2.5-flash",
    "think": "gemini,gemini-2.5-flash",
    "longContext": "gemini,gemini-2.5-flash",
    "longContextThreshold": 60000
  }
}
Save and close Notepad once done.

6. Configure Your Environment Variable (API Key)
Run PowerShell as Administrator:

[System.Environment]::SetEnvironmentVariable('GOOGLE_API_KEY', 'YOUR_API_KEY_HERE', 'User')
Verify the Key
Close PowerShell → open a new window → run:

echo $env:GOOGLE_API_KEY
If the key appears, the environment variable is configured correctly.

7. Validate Installation
Run the following commands:

claude --version
ccr version
echo $env:GOOGLE_API_KEY
If all commands return output without errors, the setup is successful.

Start the Router (Terminal 1)
ccr start
Wait until you see:

✔ Service started successfully
Use Claude Code (Terminal 2)
Navigate to your project:

cd your-project-folder
ccr code
9. Quick Test
Run:

ccr code
Then type:

hi
If Claude responds, your Claude Code + Gemini setup is fully operational.
