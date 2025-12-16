# 🧠 AI Call Center

An intelligent, automated phone system powered by Twilio's Voice API that conducts interactive voice conversations, collects user information through natural speech recognition, and provides a beautiful real-time dashboard for monitoring and managing calls.

![Node.js](https://img.shields.io/badge/Node.js-18.x-green)
![Express](https://img.shields.io/badge/Express-5.1.0-blue)
![Twilio](https://img.shields.io/badge/Twilio-5.8.0-red)
![License](https://img.shields.io/badge/License-ISC-yellow)

## 📋 Table of Contents

- [Features](#-features)
- [Demo](#-demo)
- [Technology Stack](#-technology-stack)
- [Prerequisites](#-prerequisites)
- [Installation](#-installation)
- [Configuration](#-configuration)
- [Usage](#-usage)
- [API Endpoints](#-api-endpoints)
- [Project Structure](#-project-structure)
- [How It Works](#-how-it-works)
- [Deployment](#-deployment)
- [Contributing](#-contributing)
- [License](#-license)

## ✨ Features

- 🎤 **Advanced Voice Recognition** - Captures caller responses using Twilio's enhanced speech-to-text
- 📊 **Real-time Dashboard** - Monitor calls with live statistics and auto-refresh
- 💾 **Automated Data Collection** - Gathers name, email, age, location, and introduction
- 📅 **Date Filtering** - Filter and analyze calls by specific dates
- 🔄 **Auto-refresh** - Dashboard updates every 20 seconds automatically
- 📱 **Fully Responsive** - Works seamlessly on desktop, tablet, and mobile
- 🎯 **Conversational Flow** - Natural, guided conversation with callers
- 📈 **Statistics Dashboard** - Track total calls, server status, and complete profiles
- 🔐 **Secure** - Environment-based configuration for sensitive credentials
- 🚀 **Production Ready** - Optimized for deployment on cloud platforms

## 🎬 Demo

Visit the [About Page](http://localhost:5500/about) for detailed information about features and functionality.

## 🛠️ Technology Stack

- **Backend:** Node.js, Express.js
- **Voice API:** Twilio Voice & TwiML
- **Frontend:** HTML5, CSS3, Vanilla JavaScript
- **Data Storage:** JSON file-based storage
- **Deployment:** Render, Heroku, AWS, or any Node.js hosting

## 📦 Prerequisites

Before you begin, ensure you have the following installed:

- [Node.js](https://nodejs.org/) (v18.x or higher)
- [npm](https://www.npmjs.com/) (comes with Node.js)
- A [Twilio Account](https://www.twilio.com/try-twilio) with:
  - Account SID
  - Auth Token
  - A Twilio phone number with voice capabilities
  - A verified phone number for testing

## 🚀 Installation

1. **Clone the repository**
   ```bash
   git clone https://github.com/yourusername/ai-call-center.git
   cd ai-call-center
   ```

2. **Install dependencies**
   ```bash
   npm install
   ```

3. **Create environment file**
   ```bash
   # Create .env file in the root directory
   touch .env
   ```

4. **Configure environment variables** (see [Configuration](#-configuration))

5. **Start the server**
   ```bash
   npm start
   ```

6. **Access the dashboard**
   ```
   Open http://localhost:5500 in your browser
   ```

## ⚙️ Configuration

Create a `.env` file in the root directory with the following variables:

```env
# Twilio Credentials
TWILIO_ACCOUNT_SID=your_account_sid_here
TWILIO_AUTH_TOKEN=your_auth_token_here
TWILIO_PHONE_NUMBER=+1234567890
TEST_PHONE_NUMBER=+1234567890

# Server Configuration
PORT=5500
BASE_URL=https://your-app-url.com

# For local development with ngrok
# BASE_URL=https://your-ngrok-url.ngrok.io
```

### Getting Twilio Credentials

1. Sign up at [Twilio](https://www.twilio.com/try-twilio)
2. Get your Account SID and Auth Token from the [Twilio Console](https://console.twilio.com/)
3. Purchase or get a free trial phone number with voice capabilities
4. Verify your personal phone number for testing

### Local Development with ngrok

For local testing, use [ngrok](https://ngrok.com/) to expose your local server:

```bash
# Install ngrok
npm install -g ngrok

# Start your server
npm start

# In another terminal, expose port 5500
ngrok http 5500

# Copy the HTTPS URL and set it as BASE_URL in .env
```

## 📖 Usage

### Starting the Server

```bash
npm start
```

The server will start on `http://localhost:5500` (or your configured PORT).

### Making Test Calls

1. Open the dashboard at `http://localhost:5500`
2. Click the "📞 Make Test Call" button
3. Answer the call and follow the voice prompts
4. Your responses will be recorded and displayed in the dashboard

### Viewing Call Logs

- **All Calls:** View all calls in the main dashboard table
- **Filter by Date:** Use the date picker to filter calls by specific dates
- **Refresh:** Click "🔄 Refresh Data" or wait for auto-refresh (20s)

### Dashboard Statistics

- **Total Calls:** Number of calls processed
- **Server Status:** Real-time connectivity indicator
- **Last Call:** Time since the most recent call
- **Complete Profiles:** Calls with all information collected

## 🔌 API Endpoints

### `GET /`
Serves the main dashboard interface.

**Response:** HTML page

---

### `GET /about`
Serves the about page with detailed application information.

**Response:** HTML page

---

### `POST /voice`
Handles incoming voice calls and processes speech input.

**Request Body:**
- `CallSid` - Unique call identifier
- `SpeechResult` - Transcribed speech from caller
- `Digits` - DTMF input (if any)
- `From` - Caller's phone number

**Response:** TwiML XML for voice instructions

---

### `GET /logs`
Returns all call logs with statistics.

**Response:**
```json
{
  "success": true,
  "totalCalls": 10,
  "calls": [
    {
      "from": "+1234567890",
      "name": "John Doe",
      "email": "john@example.com",
      "age": "30",
      "location": "New York, USA",
      "introduction": "I'm a software developer...",
      "time": "2024-01-15T10:30:00.000Z",
      "callSid": "CAxxxxx"
    }
  ],
  "timestamp": "2024-01-15T10:35:00.000Z"
}
```

---

### `POST /call-me`
Initiates a test call to the configured phone number.

**Request Body (optional):**
```json
{
  "to": "+1234567890"
}
```

**Response:**
```json
{
  "success": true,
  "callSid": "CAxxxxx"
}
```

---

### `GET /test`
Health check endpoint.

**Response:**
```json
{
  "message": "Server is working!",
  "timestamp": "2024-01-15T10:30:00.000Z"
}
```

## 📁 Project Structure

```
ai-call-center/
├── public/
│   ├── dashboard.html      # Main dashboard interface
│   └── about.html          # About page with documentation
├── ai_call_center_server.js # Express server and API routes
├── logs.json               # Call logs storage (auto-generated)
├── package.json            # Project dependencies
├── .env                    # Environment variables (create this)
├── .gitignore             # Git ignore rules
└── README.md              # This file
```

## 🔄 How It Works

### 1. Call Flow

```
Incoming Call → Twilio → /voice endpoint → TwiML Response
                                ↓
                        Speech Recognition
                                ↓
                        Data Collection
                                ↓
                        Store in logs.json
                                ↓
                        Display in Dashboard
```

### 2. Conversation Steps

1. **Name Collection**
   - Prompt: "Hello! Please say your full name after the beep."
   - Stores: Caller's full name

2. **Email Collection**
   - Prompt: "Now please tell your email address clearly."
   - Stores: Email address (as spoken)

3. **Age Collection**
   - Prompt: "Great! Now please tell me your age clearly."
   - Stores: Age

4. **Location Collection**
   - Prompt: "Perfect! Now please say your city and state or country clearly."
   - Stores: Geographic location

5. **Introduction**
   - Prompt: "Finally, give a short introduction about yourself."
   - Stores: Personal introduction

6. **Completion**
   - Confirms information received
   - Simulates transfer to human agent
   - Ends call gracefully

### 3. Data Storage

All call data is stored in `logs.json` with the following structure:

```json
[
  {
    "from": "+1234567890",
    "name": "John Doe",
    "email": "john at example dot com",
    "age": "30",
    "location": "New York USA",
    "introduction": "I'm a software developer interested in AI",
    "time": "2024-01-15T10:30:00.000Z",
    "callSid": "CAxxxxx"
  }
]
```

## 🚀 Deployment

### Deploy to Render

1. Push your code to GitHub
2. Create a new Web Service on [Render](https://render.com/)
3. Connect your GitHub repository
4. Set environment variables in Render dashboard
5. Deploy!

### Deploy to Heroku

```bash
# Login to Heroku
heroku login

# Create new app
heroku create your-app-name

# Set environment variables
heroku config:set TWILIO_ACCOUNT_SID=your_sid
heroku config:set TWILIO_AUTH_TOKEN=your_token
heroku config:set TWILIO_PHONE_NUMBER=+1234567890
heroku config:set TEST_PHONE_NUMBER=+1234567890
heroku config:set BASE_URL=https://your-app-name.herokuapp.com

# Deploy
git push heroku main
```

### Configure Twilio Webhook

After deployment, configure your Twilio phone number:

1. Go to [Twilio Console](https://console.twilio.com/)
2. Navigate to Phone Numbers → Manage → Active Numbers
3. Select your phone number
4. Under "Voice & Fax", set:
   - **A CALL COMES IN:** Webhook
   - **URL:** `https://your-app-url.com/voice`
   - **HTTP:** POST
5. Save configuration

## 🎯 Use Cases

- **Customer Support** - Automated information gathering before agent transfer
- **Lead Generation** - Collect prospect details via phone
- **Surveys** - Conduct automated phone surveys
- **Appointment Scheduling** - Gather customer information
- **Event Registration** - Collect attendee details
- **Market Research** - Phone-based data collection

## 🔮 Future Enhancements

- [ ] CRM integration (Salesforce, HubSpot)
- [ ] Email notifications for new calls
- [ ] Call recording and playback
- [ ] Multi-language support
- [ ] Advanced analytics and reporting
- [ ] SMS follow-up automation
- [ ] AI sentiment analysis
- [ ] Database integration (MongoDB, PostgreSQL)
- [ ] User authentication
- [ ] Export data to CSV/Excel

## 🤝 Contributing

Contributions are welcome! Please follow these steps:

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit your changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

## 📝 License

This project is licensed under the ISC License.

## 🙏 Acknowledgments

- [Twilio](https://www.twilio.com/) for their amazing Voice API
- [Express.js](https://expressjs.com/) for the web framework
- [Node.js](https://nodejs.org/) community

## 📧 Support

For issues, questions, or suggestions:
- Open an issue on GitHub
- Check the [About Page](/about) for detailed documentation

## 🌟 Show Your Support

Give a ⭐️ if this project helped you!

---

**Built with ❤️ using Node.js and Twilio**
