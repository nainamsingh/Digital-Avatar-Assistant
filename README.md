# Azure Digital Avatar - Real-time Text-to-Speech Avatar

Create interactive digital avatars powered by Azure Speech Services and OpenAI. This application demonstrates real-time avatar synthesis with speech-to-text, text-to-speech, and chat capabilities.

## Quick Start

1. **Clone and install dependencies**
   ```bash
   git clone <your-repo-url>
   cd digital-avatar
   pip install -r requirements.txt
   ```

2. **Set up your environment variables** (see [Configuration](#configuration))

3. **Run the application**
   ```bash
   python -m flask run -h 0.0.0.0 -p 5000
   ```

4. **Open your browser** and navigate to:
   - Basic Avatar: `http://localhost:5000/basic`
   - Chat Avatar: `http://localhost:5000/chat`
   - React Frontend: `http://localhost:5000/map`

## Table of Contents

- [Prerequisites](#prerequisites)
- [Configuration](#configuration)
- [Applications](#applications)
  - [Basic Avatar App](#basic-avatar-app)
  - [Chat Avatar App](#chat-avatar-app)
  - [React Frontend](#react-frontend)
- [Troubleshooting](#troubleshooting)
- [Advanced Configuration](#advanced-configuration)

## Prerequisites

- **Python 3.7+** installed on your system
- **Azure Speech Services** resource with API key
- **Azure OpenAI** resource (for chat functionality)
- **Modern web browser** with microphone access
- **Flask** and other dependencies (installed via requirements.txt)

Follow the [Azure Text-to-Speech quickstart](https://docs.microsoft.com/azure/cognitive-services/speech-service/get-started-text-to-speech) to set up your Azure environment.

## Configuration

### Required Environment Variables

Create these environment variables before running the application:

```bash
# Azure Speech Services
export SPEECH_REGION="eastus2"                    # Your Azure Speech resource region
export SPEECH_KEY="your_speech_api_key"           # Your Azure Speech API key

# Azure OpenAI (for chat functionality)
export AZURE_OPENAI_ENDPOINT="https://your-resource.openai.azure.com/"
export AZURE_OPENAI_API_KEY="your_openai_api_key"
export AZURE_OPENAI_DEPLOYMENT_NAME="gpt-35-turbo"
```

### Optional Environment Variables

```bash
# Private Endpoint (optional)
export SPEECH_PRIVATE_ENDPOINT="https://my-speech-service.cognitiveservices.azure.com"
export SPEECH_RESOURCE_URL="/subscriptions/.../providers/Microsoft.CognitiveServices/accounts/..."
export USER_ASSIGNED_MANAGED_IDENTITY_CLIENT_ID="your_client_id"

# Azure Cognitive Search (for constrained chat)
export COGNITIVE_SEARCH_ENDPOINT="https://your-search.search.windows.net/"
export COGNITIVE_SEARCH_API_KEY="your_search_api_key"
export COGNITIVE_SEARCH_INDEX_NAME="your_index_name"

# Custom ICE Server (optional)
export ICE_SERVER_URL="your_ice_server_url"
export ICE_SERVER_URL_REMOTE="your_remote_ice_server_url"
export ICE_SERVER_USERNAME="your_ice_username"
export ICE_SERVER_PASSWORD="your_ice_password"
```

## Applications

### Basic Avatar App

**What it does**: Simple text-to-speech avatar that speaks any text you provide.

**How to use**:
1. Navigate to `http://localhost:5000/basic`
2. Configure your avatar settings:
   - **TTS Voice**: Choose from [available voices](https://docs.microsoft.com/azure/cognitive-services/speech-service/language-support#text-to-speech)
   - **Avatar Character**: Default is 'lisa', customize as needed
   - **Background**: Set color or image URL
3. Click **Start Session** to initialize the avatar
4. Type text and click **Speak** to make the avatar talk
5. Click **Stop Session** when finished

**Features**:
- Real-time avatar synthesis
- Customizable backgrounds and characters
- Transparent background support
- Video cropping options
- Custom and personal voice support

### Chat Avatar App

**What it does**: Interactive chat experience combining speech recognition, OpenAI chat, and avatar responses.

**How to use**:
1. Navigate to `http://localhost:5000/chat`
2. Configure chat settings:
   - **System Prompt**: Set the AI's personality/context
   - **STT Locale**: Choose speech recognition language
   - **Conversation Mode**: Continuous or single-utterance
3. Configure avatar settings (same as Basic App)
4. Click **Open Avatar Session**
5. Click **Start Microphone** and begin speaking
6. The avatar will respond with both text and speech

**Features**:
- Voice-to-voice conversation
- Azure OpenAI integration
- Chat history display
- Custom data integration via Azure Cognitive Search
- Interrupt and control options
- Text input as alternative to speech

### React Frontend

**What it does**: Modern React-based interface for the avatar system.

**How to use**:
1. **Set up React development environment**:
   ```bash
   cd frontend
   npm install
   npm run dev
   ```
2. **Start the Flask backend** (in separate terminal):
   ```bash
   python -m flask run -h 0.0.0.0 -p 5000
   ```
3. Navigate to `http://localhost:5000/map`

## Troubleshooting

### Common Issues

**Avatar not appearing**
- Verify your `SPEECH_KEY` and `SPEECH_REGION` are correct
- Check browser console for WebRTC errors
- Ensure your network allows WebRTC connections

**Microphone not working**
- Allow microphone permissions in your browser
- Check if microphone is being used by other applications
- Try different browsers (Chrome/Edge recommended)

**Chat responses not working**
- Verify Azure OpenAI credentials are correct
- Check that your deployment name matches `AZURE_OPENAI_DEPLOYMENT_NAME`
- Ensure your OpenAI resource has sufficient quota

**Connection timeouts**
- Check your network firewall settings
- If using private endpoints, verify network configuration
- Try without custom ICE server settings first

### Getting Help

If you encounter issues:
1. Check the browser developer console for error messages
2. Verify all environment variables are set correctly
3. Test with the Basic App before trying Chat App
4. Ensure your Azure resources are properly configured and have available quota

## Advanced Configuration

### Custom Avatars
- Set `Custom Avatar` checkbox for personalized characters
- Configure `Avatar Style` for different poses/expressions
- Use `Avatar Character` field to specify custom avatar IDs

### Background Customization
- **Solid Color**: Use hex color codes (e.g., #FF0000)
- **Image Background**: Provide publicly accessible image URLs
- **Transparent**: Enable for green-screen effect with custom compositing

### Voice Customization
- **Custom Voice**: Use `Custom Voice Deployment ID` for trained voices
- **Personal Voice**: Use `Personal Voice Speaker Profile ID` for cloned voices
- **Multi-language**: Specify multiple locales for STT recognition

### Performance Optimization
- **Auto Reconnect**: Automatically handles connection drops
- **Local Video for Idle**: Uses local video files during idle periods
- **Video Crop**: Reduces bandwidth by cropping avatar video

## Additional Resources

- [Azure Speech Services Documentation](https://docs.microsoft.com/azure/cognitive-services/speech-service/)
- [Azure OpenAI Documentation](https://docs.microsoft.com/azure/cognitive-services/openai/)
- [Available TTS Voices](https://docs.microsoft.com/azure/cognitive-services/speech-service/language-support#text-to-speech)
- [STT Language Support](https://docs.microsoft.com/azure/cognitive-services/speech-service/language-support#speech-to-text)
