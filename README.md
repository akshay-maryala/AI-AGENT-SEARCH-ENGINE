# AI-AGENT-SEARCH-ENGINE
AI-powered search engine using NLP, machine learning, and web scraping for precise, contextual, and adaptive information retrieval. Open-source and customizable.

## WebUI Overview
- **Built on Gradio**: Supports most `browser-use` functionalities.
- **User-Friendly**: Enables easy interaction with the browser agent.
- **Expanded LLM Support**: Integrated with Google, OpenAI, Azure OpenAI, Anthropic, DeepSeek, Ollama, and more models.
- **Custom Browser Support**: Allows using your own browser without re-login or authentication issues.
- **Persistent Browser Sessions**: Keeps browser open between AI tasks for better session tracking.




### Snapshots
- **Agent Interface Screenshot**
- ![image](https://github.com/user-attachments/assets/9d59a6c2-4b7f-4165-8ee8-ca14d9f60180)

- **Command Prompt Screenshot**
- ![image](https://github.com/user-attachments/assets/744265f9-d7df-49d0-b000-a9f29e10f9f5)

- **Result Screenshot**
- ![image](https://github.com/user-attachments/assets/237f4564-56a3-40a1-8e56-85498e654f0d)


---

## Installation Guide
### Prerequisites
- Python 3.11 or higher
- Git (for cloning the repository)

### Option 1: Local Installation
#### Step 1: Clone the Repository
```bash
git clone https://github.com/browser-use/web-ui.git
cd web-ui
```
#### Step 2: Set Up Python Environment
We recommend using `uv` for managing the Python environment.

Using `uv` (Recommended):
```bash
uv venv --python 3.11
```
Activate the virtual environment:
```bash
# Windows (Command Prompt)
.venv\Scripts\activate

# Windows (PowerShell)
.\.venv\Scripts\Activate.ps1

# macOS/Linux
source .venv/bin/activate
```
#### Step 3: Install Dependencies
```bash
uv pip install -r requirements.txt
```
#### Step 4: Install Playwright
```bash
playwright install
```
#### Step 5: Configure Environment
```bash
# Windows (Command Prompt)
copy .env.example .env

# macOS/Linux/Windows (PowerShell)
cp .env.example .env
```
Open `.env` in your preferred text editor and add API keys and other settings.

---

### Option 2: Docker Installation
#### Prerequisites
- Docker and Docker Compose installed
- Docker Desktop (For Windows/macOS)
- Docker Engine and Docker Compose (For Linux)

#### Installation Steps
1. Clone the repository:
   ```bash
   git clone https://github.com/browser-use/web-ui.git
   cd web-ui
   ```
2. Create and configure environment file:
   ```bash
   copy .env.example .env  # Windows (Command Prompt)
   cp .env.example .env     # macOS/Linux/Windows (PowerShell)
   ```
   Edit `.env` and add API keys.
3. Run with Docker:
   ```bash
   docker compose up --build
   ```
4. To keep the browser open between AI tasks:
   ```bash
   CHROME_PERSISTENT_SESSION=true docker compose up --build
   ```
5. **Access the Application**:
   - **Web Interface**: Open `http://localhost:7788` in your browser.
   - **VNC Viewer** (to watch browser interactions): Open `http://localhost:6080/vnc.html`
   - **Default VNC password**: `youvncpassword` (can be changed in `.env` file).

---

## Usage
### Local Setup
Run the WebUI after installation:
```bash
python webui.py --ip 127.0.0.1 --port 7788
```

### WebUI Options
- `--ip`: The IP address to bind (default: `127.0.0.1`).
- `--port`: The port for WebUI (default: `7788`).
- `--theme`: Set UI theme (`Ocean` is default).
- `--dark-mode`: Enables dark mode.

### Available Themes
- **Default**: Balanced design.
- **Soft**: Muted colors.
- **Monochrome**: Grayscale.
- **Glass**: Semi-transparent.
- **Origin**: Retro-inspired.
- **Citrus**: Bright colors.
- **Ocean (default)**: Calm blue theme.

### Access WebUI
Open your browser and visit:
```
http://127.0.0.1:7788
```

---

## Using Your Own Browser (Optional)
Set `CHROME_PATH` to the browser executable path and `CHROME_USER_DATA` to the user data directory:

**Windows:**
```bash
CHROME_PATH="C:\Program Files\Google\Chrome\Application\chrome.exe"
CHROME_USER_DATA="C:\Users\YourUsername\AppData\Local\Google\Chrome\User Data"
```
(Note: Replace `YourUsername` with your actual Windows username.)

**Mac:**
```bash
CHROME_PATH="/Applications/Google Chrome.app/Contents/MacOS/Google Chrome"
CHROME_USER_DATA="/Users/YourUsername/Library/Application Support/Google/Chrome"
```

Close all Chrome windows and open WebUI in another browser (Firefox or Edge).

---

## Keep Browser Open (Optional)
Set in `.env`:
```bash
CHROME_PERSISTENT_SESSION=true
```

---

## Docker Setup
### Environment Variables
Configuration is done via `.env` file.

#### LLM API Keys
```bash
OPENAI_API_KEY=your_key_here
ANTHROPIC_API_KEY=your_key_here
GOOGLE_API_KEY=your_key_here
```

#### Browser Settings
```bash
CHROME_PERSISTENT_SESSION=true   # Keep browser open between tasks
RESOLUTION=1920x1080x24         # Screen resolution format: WIDTHxHEIGHTxDEPTH
RESOLUTION_WIDTH=1920           # Width in pixels
RESOLUTION_HEIGHT=1080          # Height in pixels
```

#### VNC Settings
```bash
VNC_PASSWORD=your_vnc_password  # Default: "vncpassword"
```

---

## Platform Support
- Supports both **AMD64** and **ARM64** architectures.
- **ARM64 (Apple Silicon Macs)** automatically uses the appropriate image.

### Browser Persistence Modes
#### Default Mode (`CHROME_PERSISTENT_SESSION=false`)
- Browser opens and closes with each AI task.
- Clean state for each interaction.
- Lower resource usage.

#### Persistent Mode (`CHROME_PERSISTENT_SESSION=true`)
- Browser remains open between AI tasks.
- Maintains history and session state.
- Allows reviewing previous interactions.

### Viewing Browser Interactions
- Open **noVNC viewer** at `http://localhost:6080/vnc.html`.
- Enter the **VNC password** (`vncpassword` or your custom password).
- Direct VNC access is available on **port 5900** (mapped to **5901** in the container).

### Container Management
```bash
# Start with persistent browser
CHROME_PERSISTENT_SESSION=true docker compose up -d

# Start with default mode (browser closes after tasks)
docker compose up -d

# View logs
docker compose logs -f

# Stop the container
docker compose down
```

