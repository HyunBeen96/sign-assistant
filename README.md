# 🤟 Sign Language Assistant
> **Real-time Bidirectional Sign Language Translation System**

<div align="center">

![Python](https://img.shields.io/badge/python-v3.8+-blue.svg)
![PyQt5](https://img.shields.io/badge/PyQt5-5.15+-green.svg)
![OpenCV](https://img.shields.io/badge/OpenCV-4.8+-red.svg)
![License](https://img.shields.io/badge/license-MIT-yellow.svg)
![Status](https://img.shields.io/badge/status-Active-success.svg)

[**📺 Demo Video**](#demo) • [**📖 Documentation**](#documentation) • [**🚀 Quick Start**](#quick-start) • [**🤝 Contributing**](#contributing)

</div>

---

## 📌 Overview

농인과 청인 간의 소통 장벽을 해소하기 위한 **실시간 양방향 번역 시스템**입니다. 
최신 AI 기술을 활용하여 수어를 음성으로, 음성을 텍스트로 실시간 변환합니다.

### ✨ Key Features

<table>
<tr>
<td width="50%">

#### 🎥 **수어 → 음성/텍스트**
- YOLO 기반 실시간 수어 인식
- 시퀀스 단어 자동 조합
- 자연스러운 문장 생성 (GPT)
- TTS 음성 출력

</td>
<td width="50%">

#### 🎤 **음성 → 텍스트**
- Google Cloud STT 활용
- 실시간 음성 인식
- 노이즈 필터링
- 다국어 지원 가능

</td>
</tr>
</table>

### 🎯 Project Goals

<div align="center">

| 구분 | 목표 | 진행상황 |
|:---:|:---|:---:|
| **기술적 목표** | 수어 인식 정확도 90% 이상 | 🟡 진행중 |
| | 응답 시간 2초 이내 | ✅ 달성 |
| | 8시간 연속 사용 | 🔄 계획중 |
| **사회적 목표** | 농인-청인 소통 장벽 해소 | 🟢 진행중 |
| | 일상 생활 접근성 향상 | 🟢 진행중 |

</div>

---

## 🏗️ System Architecture

### High-Level Design

```mermaid
graph TB
    subgraph "User Interface Layer"
        A[Camera Input] 
        B[Microphone Input]
        C[Display Output]
        D[Speaker Output]
    end
    
    subgraph "Processing Layer"
        E[Sign Language Detector<br/>YOLO Model]
        F[Speech Recognition<br/>Google Cloud STT]
        G[Sentence Generator<br/>OpenAI GPT]
        H[Text-to-Speech<br/>Google Cloud TTS]
    end
    
    subgraph "Core Module Layer"
        I[Sequence Manager]
        J[Translation Controller]
        K[Cache Manager]
    end
    
    A --> E --> I --> G
    B --> F --> J
    G --> H --> D
    G --> C
    F --> C
```

### 📁 Project Structure

```
sign-assistant/
│
├── 📄 main.py                    # Entry point
├── 📋 requirements.txt           # Dependencies
├── 🔐 .env.example              # Environment variables template  
│
├── 📦 modules/                  # Core modules
│   ├── 🎮 app_controller.py    # Application controller
│   ├── ⚙️ config.py            # Configuration
│   │
│   ├── 🖼️ ui/                  # User Interface
│   │   ├── main_window.py      # Main window
│   │   └── components.py       # UI components
│   │
│   ├── 🧠 core/                # Core functionality
│   │   ├── sequence_manager.py # Sequence management
│   │   ├── sign_detector.py    # Sign language detection
│   │   ├── camera_handler.py   # Camera processing
│   │   └── workers.py          # Background workers
│   │
│   └── 🗣️ translation/         # Translation modules
│       ├── main_translator.py  # Main translator
│       ├── sentence_generator.py # Sentence generation
│       ├── tts_module.py       # Text-to-Speech
│       └── stt_module.py       # Speech-to-Text
│
├── 🤖 models/                   # AI models
│   └── best_1.pt               # YOLO model

├── 📦 model_train
│   └── model.py
│
└── 📊 logs/                     # Application logs
```

---

## 🚀 Quick Start

### Prerequisites

<details>
<summary><b>System Requirements</b></summary>

- **OS**: Windows 10+, macOS 10.14+, Ubuntu 20.04+
- **Python**: 3.8 or higher
- **RAM**: Minimum 4GB (8GB recommended)
- **Storage**: 2GB free space
- **Camera**: USB webcam or built-in camera
- **Microphone**: Required for speech recognition

</details>

<details>
<summary><b>API Keys Required</b></summary>

1. **OpenAI API Key** - [Get it here](https://platform.openai.com/api-keys)
2. **Google Cloud Credentials** - [Setup guide](https://cloud.google.com/docs/authentication)
   - Enable Text-to-Speech API
   - Enable Speech-to-Text API

</details>

### Installation

#### 1️⃣ Clone the repository
```bash
git clone https://github.com/HyunBeen96/sign-assistant.git
cd sign-assistant
```

#### 2️⃣ Create virtual environment
```bash
# Windows
python -m venv venv
venv\Scripts\activate

# macOS/Linux
python3 -m venv venv
source venv/bin/activate
```

#### 3️⃣ Install dependencies
```bash
# Install required packages
pip install -r requirements.txt

# For macOS users (install portaudio first)
brew install portaudio

# For Ubuntu users
sudo apt-get install portaudio19-dev python3-pyaudio
```

#### 4️⃣ Configure environment
```bash
# Copy example environment file
cp .env.example .env

# Edit .env file with your API keys
# OPENAI_API_KEY=your_openai_api_key
# GOOGLE_APPLICATION_CREDENTIALS=path/to/google-credentials.json
```

#### 5️⃣ Download YOLO model
```bash
# Create models directory
mkdir models

# Download the model (링크 제공 예정)
# Place best_1.pt in models/ directory
```

---

## 💻 Usage

### Basic Usage

```bash
# Run the application
python main.py

# Run with options
python main.py --debug              # Debug mode
python main.py --no-camera          # Without camera
python main.py --log-level DEBUG    # Detailed logging
```

### Features Guide

<details>
<summary><b>🤟 Sign Language Mode</b></summary>

1. Click **"수어하기"** button to start
2. Position yourself in the green guide box
3. Perform sign language gestures
4. System recognizes and accumulates words
5. Click **"수어 그만하기"** to generate sentence
6. Generated sentence will be spoken via TTS

**Supported Gestures:**
- Single words: 학교, 병원, 아프다, 가다, 나, 빨리, 구조
- Sequence words: 구급차(3 steps), 쓰러지다(2 steps), 사람(2 steps)
- Special: 리셋 (delete last word)

</details>

<details>
<summary><b>🎤 Speech Mode</b></summary>

1. Click **"말하기"** button to start recording
2. Speak clearly into the microphone
3. Click **"말 그만하기"** to stop and convert
4. Recognized text appears on screen

</details>

### 📸 Screenshots

<div align="center">
<table>
<tr>
<td align="center">
<img src="[스크린샷 위치]" width="400"/>
<br><b>Main Interface</b>
</td>
<td align="center">
<img src="[스크린샷 위치]" width="400"/>
<br><b>Sign Language Detection</b>
</td>
</tr>
<tr>
<td align="center">
<img src="[스크린샷 위치]" width="400"/>
<br><b>Speech Recognition</b>
</td>
<td align="center">
<img src="[스크린샷 위치]" width="400"/>
<br><b>Translation Result</b>
</td>
</tr>
</table>
</div>

---

## 🎥 Demo

<div align="center">

### 📺 Video Demonstration

[![Demo Video](https://img.youtube.com/vi/[YouTube_ID]/maxresdefault.jpg)](https://www.youtube.com/watch?v=[YouTube_ID])

*Click to watch the demo video*

### 🎬 Usage Scenarios

| Scenario | Description | Status |
|:---:|:---|:---:|
| 🏥 **Hospital** | Patient-Doctor communication | ✅ Tested |
| 🏪 **Store** | Customer service interaction | ✅ Tested |
| 🏛️ **Government Office** | Civil service assistance | 🔄 Testing |
| 🚌 **Public Transport** | Travel assistance | 📋 Planned |

</div>

---

## 🔧 Development

### Project Status

<div align="center">

| Module | Progress | Description |
|:---|:---:|:---|
| **Sign Detection** | ![90%](https://progress-bar.dev/90) | YOLO model trained |
| **Sequence Management** | ![100%](https://progress-bar.dev/100) | Complete |
| **Sentence Generation** | ![85%](https://progress-bar.dev/85) | GPT integration |
| **TTS/STT** | ![95%](https://progress-bar.dev/95) | Google Cloud APIs |
| **UI/UX** | ![80%](https://progress-bar.dev/80) | PyQt5 interface |

</div>

### Tech Stack

<div align="center">

| Category | Technologies |
|:---:|:---|
| **Language** | ![Python](https://img.shields.io/badge/Python-3776AB?style=flat&logo=python&logoColor=white) |
| **UI Framework** | ![Qt](https://img.shields.io/badge/PyQt5-41CD52?style=flat&logo=qt&logoColor=white) |
| **AI/ML** | ![YOLO](https://img.shields.io/badge/YOLO-00FFFF?style=flat&logo=yolo&logoColor=black) ![OpenAI](https://img.shields.io/badge/OpenAI-412991?style=flat&logo=openai&logoColor=white) |
| **Cloud Services** | ![Google Cloud](https://img.shields.io/badge/Google_Cloud-4285F4?style=flat&logo=google-cloud&logoColor=white) |
| **Computer Vision** | ![OpenCV](https://img.shields.io/badge/OpenCV-5C3EE8?style=flat&logo=opencv&logoColor=white) |

</div>

### Running Tests

```bash
# Run all tests
pytest

# Run with coverage
pytest --cov=modules tests/

# Run specific test
pytest tests/test_sequence_manager.py
```

### Code Style

```bash
# Format code
black modules/

# Check code style
flake8 modules/

# Type checking
mypy modules/
```

---

## 📊 Performance

### Benchmarks

| Metric | Target | Current | Status |
|:---|:---:|:---:|:---:|
| **Sign Recognition Accuracy** | 90% | 87% | 🟡 |
| **Response Time** | <2s | 1.5s | ✅ |
| **Memory Usage** | <500MB | 420MB | ✅ |
| **FPS (Camera)** | 30fps | 25fps | 🟡 |
| **TTS Latency** | <500ms | 300ms | ✅ |

### Optimization Tips

- Use GPU acceleration for YOLO model
- Enable caching for frequently used translations
- Adjust camera resolution based on performance
- Use lightweight TTS voices for faster response

---

## 🤝 Contributing

우리는 모든 기여를 환영합니다! 

### How to Contribute

1. Fork the repository
2. Create your feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit your changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

### Development Setup

```bash
# Clone your fork
git clone https://github.com/your-username/sign-assistant.git

# Install development dependencies
pip install -r requirements-dev.txt

# Run in development mode
python main.py --debug
```

---

## 📝 Documentation

- [📖 User Manual](docs/USER_MANUAL.md)
- [🔧 API Documentation](docs/API.md)
- [🏗️ Architecture Guide](docs/ARCHITECTURE.md)
- [🚀 Deployment Guide](docs/DEPLOYMENT.md)

---

## 🐛 Troubleshooting

<details>
<summary><b>Common Issues</b></summary>

### Camera not detected
```bash
# Check camera availability
python -c "import cv2; print(cv2.VideoCapture(0).isOpened())"
```

### PyAudio installation failed
```bash
# Windows
pip install pipwin
pipwin install pyaudio

# macOS
brew install portaudio
pip install pyaudio

# Linux
sudo apt-get install portaudio19-dev
pip install pyaudio
```

### Google Cloud authentication error
```bash
# Set environment variable
export GOOGLE_APPLICATION_CREDENTIALS="path/to/credentials.json"
```

</details>

---

## 📜 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

---

## 👥 Team

<div align="center">

| Role | Name | GitHub | Contact |
|:---:|:---:|:---:|:---:|
| **Project Lead** | HyunBeen | [@HyunBeen96](https://github.com/HyunBeen96) | [email] |
| **AI/ML Developer** | - | - | - |
| **UI/UX Developer** | - | - | - |
| **Backend Developer** | - | - | - |

</div>

---

## 🙏 Acknowledgments

- [Ultralytics](https://github.com/ultralytics/ultralytics) for YOLO implementation
- [OpenAI](https://openai.com/) for GPT API
- [Google Cloud](https://cloud.google.com/) for TTS/STT services
- Korean Sign Language Dataset providers
- All contributors and testers

---

## 📮 Contact

- **Project Issues**: [GitHub Issues](https://github.com/HyunBeen96/sign-assistant/issues)
- **Email**: your-email@example.com
- **Project Link**: [https://github.com/HyunBeen96/sign-assistant](https://github.com/HyunBeen96/sign-assistant)

---

<div align="center">

### 🌟 Star History

[![Star History Chart](https://api.star-history.com/svg?repos=HyunBeen96/sign-assistant&type=Date)](https://star-history.com/#HyunBeen96/sign-assistant&Date)

**If you find this project useful, please consider giving it a star ⭐**

<br>

Made with ❤️ by Sign Language Assistant Team

</div>
